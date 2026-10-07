
---

## Оглавление

- [[#1. Назначение middleware и модель конвейера|1. Назначение middleware и модель конвейера]]
- [[#2. `IApplicationBuilder`: построение конвейера|2. IApplicationBuilder: построение конвейера]]
- [[#3. Middleware в отдельном классе: `UseMiddleware<T>`|3. Middleware в отдельном классе: UseMiddleware<T>]]
- [[#4. Middleware через `IMiddleware`|4. Middleware через IMiddleware]]
- [[#5. Ветвление: `Map`, `MapWhen`, `UseWhen`|5. Ветвление: Map, MapWhen, UseWhen]]
- [[#6. Порядок middleware|6. Порядок middleware]]

---

# 1. Назначение middleware и модель конвейера

**Middleware** — компонент конвейера обработки HTTP-запроса. Он получает `HttpContext`, выполняет свою работу и решает, передавать ли управление следующему компоненту.

Middleware используются для задач, возникающих при обработке запросов: логирования, обработки исключений, аутентификации, изменения заголовков и других действий. Каждый компонент может выполнять код **до и после следующих компонентов**.

<div style="text-align: center;">

<img src="Pasted image 20261007062851.png" style="max-width: 300; width: 100%;">

</div>

---

### `RequestDelegate`

Обработка запроса представляется делегатом `RequestDelegate`:

```cs
public delegate Task RequestDelegate(HttpContext context);
```

---

### Передача управления через `next`

Компонент, продолжающий конвейер, получает делегат следующего компонента — обычно он называется `next`:

```cs
app.Use(async (context, next) =>
{
    // Работа до следующих компонентов

    await next(context);

    // Работа после следующих компонентов
});
```

`next` здесь — `RequestDelegate`.

`next(context)` запускает следующий компонент. Если тот тоже вызывает свой `next`, выполнение идёт дальше по цепочке.

**`await next(context)` ожидает завершения всей вызванной части конвейера**, после чего текущий middleware продолжает выполнение. Это обычные вложенные вызовы: следующий компонент сам не запускается, если текущий его не вызвал.

Компоненты работают с одним `HttpContext` текущего запроса. Поэтому изменения, сделанные раньше, доступны последующим компонентам.

---

### Прямой и обратный порядок выполнения

Пример двух middleware и завершающего обработчика:

```cs

app.Use(async (context, next) =>
{
    Console.WriteLine("A: до 1");
    await next(context);
    Console.WriteLine("A: после 1");
});

app.Use(async (context, next) =>
{
    Console.WriteLine("B: до 2");
    await next(context);
    Console.WriteLine("B: после 2");
});

app.Run(async context =>
{
    Console.WriteLine("Обработчик");
    await context.Response.WriteAsync("OK");
});
```

Если далее по конвейеру обработка завершается успешно, порядок выполнения будет:

```
A: до 1
B: до 2
Обработчик
B: после 2
A: после 1
```

Код до `next` выполняется в порядке подключения компонентов, а код после него — в обратном порядке. **Обратный проход — продолжение ранее начатых вызовов middleware**.

---

### Досрочное завершение конвейера

Middleware может обработать запрос самостоятельно и **не вызвать `next`**. Такое поведение называется _short-circuiting_: следующие компоненты не выполняются.

Например, middleware статических файлов может найти файл, записать его в ответ и завершить обработку без перехода к остальному конвейеру.

При этом ранее вызванные middleware продолжают выполнение после своих `await next(context)`, если вложенная обработка завершилась успешно.

Код после `await next(context)` также не является гарантированной очисткой: если вложенный вызов выбросил исключение, этот код будет пропущен. Для обязательных завершающих действий используется `try/finally`.

---

# 2. `IApplicationBuilder`: построение конвейера

`IApplicationBuilder` задаёт контракт для построения конвейера обработки запросов. `WebApplication` реализует этот интерфейс, поэтому middleware обычно подключаются через объект `app`.

Основные методы:

|Метод|Назначение|
|---|---|
|`Use(...)`|Добавляет компонент в конвейер|
|`Build()`|Собирает итоговый `RequestDelegate`|
|`New()`|Создаёт отдельный builder для нового конвейера|

Регистрация компонентов выполняется при настройке приложения. Обработка запросов начинается уже через собранный делегат. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder?view=aspnetcore-10.0&utm_source=chatgpt.com)

---

### `Use`: добавление компонента

#### Базовый метод `IApplicationBuilder`

```cs
IApplicationBuilder Use(Func<RequestDelegate, RequestDelegate> middleware);
```

Добавляет в конвейер функцию, которая **создаёт текущий обработчик на основе следующего**.

Параметр `middleware` имеет тип `Func<RequestDelegate, RequestDelegate>`:

- Принимает `RequestDelegate next` — обработчик оставшейся части конвейера
- Возвращает `RequestDelegate` — обработчик добавляемого компонента

```cs
Func<RequestDelegate, RequestDelegate> middleware = next =>
{
    RequestDelegate handler = async context =>
    {
        Console.WriteLine("До следующих компонентов");

        await next(context);

        Console.WriteLine("После следующих компонентов");
    };

    return handler;
};

app.Use(middleware);
```

`Use` регистрирует внешнюю функцию `next => ...`. При сборке конвейера ей передаётся следующий обработчик, и она возвращает `handler`, сохраняющий доступ к `next` через замыкание.

При поступлении запроса выполняется уже **возвращённый `handler`**: он получает `HttpContext`, выполняет свою работу и при необходимости вызывает `next(context)`. 

#### Обработчик с `Func<Task>` в качестве `next`

```cs
public static IApplicationBuilder Use(
	this IApplicationBuilder app,
    Func<HttpContext, Func<Task>, Task> middleware);
```

Это метод расширения. Он принимает обработчик с двумя параметрами: контекстом и функцией продолжения.

`next` имеет тип `Func<Task>`, поэтому вызывается **без аргументов** — текущий контекст уже учитывается:

```cs
app.Use(async (context, next) =>
{
    // Работа до
    await next();
    // Работа после
});
```

#### Обработчик с `RequestDelegate` в качестве `next`

```cs
public static IApplicationBuilder Use(
    this IApplicationBuilder app,
    Func<HttpContext, RequestDelegate, Task> middleware);
```

Здесь `next` имеет тип `RequestDelegate`, поэтому ему передаётся контекст:

```cs
app.Use(async (context, next) =>
{
    // Работа до
    await next(context);
    // Работа после
});
```

Обе формы с двумя параметрами являются методами расширения и используют базовый `Use` для регистрации компонента.

---

### `Run`: терминальный обработчик

`Run` — метод расширения для `IApplicationBuilder` из класса `RunExtensions`. Добавляет **терминальный обработчик** в конвейер:

```cs
public static void Run(
    this IApplicationBuilder app,
    RequestDelegate handler);
```

Параметр `handler` имеет тип `RequestDelegate`: принимает `HttpContext` и возвращает `Task`. Он **не получает `next`**, поэтому не передаёт управление следующим компонентам. 

```cs
RequestDelegate handler = async context =>
{
    await context.Response.WriteAsync("OK");
};

app.Run(handler);
```

Компоненты, расположенные после терминального обработчика в этой цепочке, не выполняются. Ранее вызванные middleware продолжают выполнение после своих `await next(context)`, если обработчик завершился успешно.

#### Отличие от запуска приложения

У `WebApplication` также есть метод:

```cs
public void Run(string? url = null);
```

Это другой метод с другим назначением:

|Вызов|Назначение|
|---|---|
|`app.Run(handler)`|Регистрирует терминальный обработчик|
|`app.Run()`|Запускает приложение и блокирует вызывающий поток до его остановки|

---

### `Build`: сборка конвейера

```cs
RequestDelegate Build();
```

`Build()` связывает зарегистрированные компоненты и возвращает единый делегат для обработки запросов. Сам вызов `Build()` запросы не обрабатывает.

Компоненты соединяются с конца: сначала подготавливается оставшаяся обработка, затем предыдущий компонент получает её как свой `next`.

Например, при регистрации A, B и C:

- C получает завершающий делегат конвейера
- B получает делегат C
- A получает делегат B

Результатом становится делегат A, через который начинается выполнение всей цепочки. **Обратный порядок сборки обеспечивает прямой порядок вызова зарегистрированных компонентов.**

В обычном приложении на `WebApplication` сборку основного конвейера выполняет инфраструктура при запуске.

Важно различать:

|Вызов|Результат|
|---|---|
|`WebApplicationBuilder.Build()`|Построенное приложение — `WebApplication`|
|`IApplicationBuilder.Build()`|Собранный конвейер — `RequestDelegate`|

---

### `New`: отдельный конвейер

```cs
IApplicationBuilder New();
```

`New()` создаёт новый builder для независимого списка middleware. Уже зарегистрированные компоненты исходного builder в него не копируются; при этом сохраняется доступ к параметрам и сервисам приложения.

Новый builder можно настроить и собрать отдельно. Само его создание не подключает полученный конвейер к основному — связь должна быть задана отдельно.

Этот механизм используется при построении веток. Обычно в прикладном коде ветвление задают через `Map`, `MapWhen` и `UseWhen`, которые предоставляют более удобный API.

---

# 3. Middleware в отдельном классе: `UseMiddleware<T>`

Логику middleware можно вынести в отдельный класс и подключить через `UseMiddleware<T>`. Это удобно для повторного использования компонента и отделения его реализации от настройки конвейера.

Обычный класс middleware работает **по соглашению**: специальный интерфейс не требуется, но конструктор и метод обработки должны соответствовать определённой форме.

---

### Метод `UseMiddleware`

`UseMiddleware` — метод расширения для `IApplicationBuilder` из класса `UseMiddlewareExtensions`. Имеет две формы:

```cs
public static IApplicationBuilder UseMiddleware<TMiddleware>(
    this IApplicationBuilder app,
    params object?[] args);
```

```cs
public static IApplicationBuilder UseMiddleware(
    this IApplicationBuilder app,
    Type middleware,
    params object?[] args);
```

Тип middleware задаётся через параметр типа или объект `Type`:

```cs
app.UseMiddleware<RequestLoggingMiddleware>();

app.UseMiddleware(typeof(RequestLoggingMiddleware));
```

Это альтернативные способы подключения одного компонента. 

`args` позволяет передать дополнительные аргументы конструктора. Метод возвращает тот же `IApplicationBuilder`.

---

### Структура класса

Для обычного middleware необходимы:

- Публичный конструктор, принимающий `RequestDelegate next`
- Один публичный метод обработки с именем `Invoke` или `InvokeAsync`
- Первый параметр метода — `HttpContext`
- Возвращаемый тип метода — `Task`

Названия `Invoke` и `InvokeAsync` поддерживаются как альтернативы. Объявлять оба метода или несколько их перегрузок в одном классе нельзя: инфраструктура должна однозначно определить метод обработки.

> Это пример **duck typing** на уровне фреймворка: класс распознаётся как middleware по наличию методов нужной формы, а не по реализации интерфейса. Такой подход позволяет использовать обычный класс и гибко расширять сигнатуру `Invoke` / `InvokeAsync` дополнительными DI-зависимостями. Интерфейс потребовал бы фиксированной сигнатуры метода, а здесь достаточно соблюсти соглашение.

```cs
public sealed class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<RequestLoggingMiddleware> _logger;

    public RequestLoggingMiddleware(
        RequestDelegate next,
        ILogger<RequestLoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        _logger.LogInformation(
            "Request: {Method} {Path}",
            context.Request.Method,
            context.Request.Path);

        await _next(context);

        _logger.LogInformation(
            "Response: {StatusCode}",
            context.Response.StatusCode);
    }
}
```

Подключение:

```cs
app.UseMiddleware<RequestLoggingMiddleware>();
```

`next` передаётся в конструктор при сборке конвейера и сохраняется в поле. При обработке запроса вызывается `InvokeAsync`, а `_next(context)` передаёт управление дальше.

---

### Получение зависимостей

Зависимости можно объявлять в двух местах:

|Место|Откуда получаются зависимости|
|---|---|
|Конструктор|Из сервисов приложения; также учитываются явно переданные `args`|
|Дополнительные параметры `Invoke` / `InvokeAsync`|Из `HttpContext.RequestServices` текущего запроса|

`RequestDelegate next` и `HttpContext` передаются инфраструктурой. Остальные необходимые сервисы должны быть зарегистрированы в DI. 

---

### Время жизни экземпляра

Обычный middleware, подключённый через `UseMiddleware<T>`, имеет время жизни приложения и **фактически используется как singleton**: для каждого подключения создаётся один экземпляр, общий для всех запросов. 

Зависимости, которые должны получаться отдельно при обработке каждого запроса, объявляют параметрами `Invoke` или `InvokeAsync`. Это относится к scoped и  transient сервисам, для которых нужен новый экземпляр при каждом вызове.

Метод обработки может вызываться одновременно для разных запросов. Данные конкретного запроса следует хранить в локальных переменных или `HttpContext`, а доступ к изменяемому состоянию в полях экземпляра должен быть потокобезопасным.

---

# 4. Middleware через `IMiddleware`

`IMiddleware` задаёт явный контракт middleware. Класс реализует интерфейс, регистрируется в DI и подключается к конвейеру через `UseMiddleware<T>`.

При обработке запроса экземпляр middleware получается из DI, поэтому его время жизни определяется регистрацией сервиса.

---

### Контракт `IMiddleware`

```cs
public interface IMiddleware
{
    Task InvokeAsync(HttpContext context, RequestDelegate next);
}
```

Метод принимает:

- `context` — контекст текущего запроса
- `next` — делегат оставшейся части конвейера

`next` передаётся **в метод обработки**, а не в конструктор. Вызов `await next(context)` продолжает конвейер; отсутствие вызова завершает обработку на текущем компоненте. 

Сигнатура фиксирована интерфейсом. Дополнительные DI-зависимости объявляются в конструкторе.

---

### Реализация и подключение

```cs
public sealed class RequestLoggingMiddleware : IMiddleware
{
    private readonly ILogger<RequestLoggingMiddleware> _logger;

    public RequestLoggingMiddleware(
        ILogger<RequestLoggingMiddleware> logger)
    {
        _logger = logger;
    }

    public async Task InvokeAsync(
        HttpContext context,
        RequestDelegate next)
    {
        _logger.LogInformation(
            "Request: {Method} {Path}",
            context.Request.Method,
            context.Request.Path);

        await next(context);
    }
}
```

Класс необходимо зарегистрировать в DI до построения приложения:

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddScoped<RequestLoggingMiddleware>();

var app = builder.Build();

app.UseMiddleware<RequestLoggingMiddleware>();

app.Run(context => context.Response.WriteAsync("OK"));

app.Run();
```

Регистрация в DI позволяет получить экземпляр, а `UseMiddleware<T>` добавляет его выполнение в конвейер. Это два отдельных действия: одной регистрации сервиса недостаточно для обработки запросов.

---

### Время жизни и зависимости

Для `IMiddleware` обычно выбирают `Scoped` или `Transient`:

|Регистрация|Поведение|
|---|---|
|`AddScoped<T>()`|Один экземпляр в области текущего запроса|
|`AddTransient<T>()`|Новый экземпляр при каждом разрешении middleware из DI|

При этих регистрациях зависимости текущего запроса можно получать **через конструктор**, включая scoped-сервисы. Полученные transient-зависимости сохраняются вместе с конкретным экземпляром middleware.

`IMiddleware` сам по себе не устанавливает время жизни. При регистрации как `Singleton` экземпляр будет общим для запросов, и ограничения на зависимости и состояние останутся соответствующими singleton-сервису. 

---

### Отличия от обычного класса middleware

|Особенность|Обычный класс|Класс с `IMiddleware`|
|---|---|---|
|Контракт обработки|Соглашение об имени и сигнатуре метода|Интерфейс|
|Передача `next`|Через конструктор|Через `InvokeAsync`|
|Регистрация самого класса в DI|Не требуется|Требуется|
|Время жизни экземпляра|Один экземпляр на подключение, фактически singleton|Определяется DI-регистрацией|
|Зависимости текущего запроса|Через параметры `Invoke` / `InvokeAsync`|Через конструктор|

Для класса с `IMiddleware` нельзя передавать дополнительные аргументы через `UseMiddleware<T>(args)`: это приводит к `NotSupportedException`. Зависимости и настройки предоставляются через DI.

---

# 5. Ветвление: `Map`, `MapWhen`, `UseWhen`

Ветвление позволяет выполнять отдельный набор middleware только для запросов, соответствующих определённому условию.

Все три метода — расширения для `IApplicationBuilder`. Параметр `configuration` имеет тип `Action<IApplicationBuilder>`: он получает builder ветки, через который подключаются её компоненты. Эта функция выполняется при настройке приложения, а обработчики ветки — при поступлении подходящих запросов.

|Метод|Условие входа в ветку|Продолжение основного конвейера при совпадении|
|---|---|---|
|`Map`|Префикс пути запроса|Нет|
|`MapWhen`|Произвольное условие|Нет|
|`UseWhen`|Произвольное условие|Да, если ветка вызывает `next`|

Если условие не выполнено, ветка пропускается и запрос продолжает основной конвейер.

---

### `Map`: ветвление по пути

Метод из класса `MapExtensions`. Перегрузки:

```cs
public static IApplicationBuilder Map(
    this IApplicationBuilder app,
    string pathMatch,
    Action<IApplicationBuilder> configuration);
```

```cs
public static IApplicationBuilder Map(
    this IApplicationBuilder app,
    PathString pathMatch,
    Action<IApplicationBuilder> configuration);
```

```cs
public static IApplicationBuilder Map(
    this IApplicationBuilder app,
    PathString pathMatch,
    bool preserveMatchedPathSegment,
    Action<IApplicationBuilder> configuration);
```

`pathMatch` задаёт начальную часть пути. Совпадение учитывает границы сегментов: `"/api"` соответствует `"/api"` и `"/api/products"`, но не `"/apix"`.

```cs
app.Map("/api", branch =>
{
    branch.Run(context =>
        context.Response.WriteAsync("API branch"));
});

app.Run(context =>
    context.Response.WriteAsync("Main pipeline"));
```

Запросы с подходящим путём обрабатываются веткой и получают `"API branch"`. Остальные доходят до основного обработчика и получают `"Main pipeline"`.

**При входе в ветку `Map` оставшаяся часть основного конвейера не выполняется**, даже если внутри ветки её middleware вызывают свой `next`: он продолжает именно конвейер ветки.

#### Изменение `Path` и `PathBase`

По умолчанию совпавшая часть пути переносится из `Request.Path` в `Request.PathBase`.

Для запроса `/api/products`, если исходный `PathBase` пуст:

|Свойство|До входа в ветку|Внутри ветки|
|---|---|---|
|`PathBase`|Пустое значение|`/api`|
|`Path`|`/api/products`|`/products`|

При `preserveMatchedPathSegment: true` путь сохраняется без такого переноса.

---

### `MapWhen`: отдельная ветка по условию

Метод из класса `MapWhenExtensions`:

```cs
public static IApplicationBuilder MapWhen(
    this IApplicationBuilder app,
    Func<HttpContext, bool> predicate,
    Action<IApplicationBuilder> configuration);
```

`predicate` проверяется для каждого запроса, дошедшего до этого компонента. Он получает `HttpContext` и определяет, нужно ли выполнять ветку.

```cs
app.MapWhen(
    context => context.Request.Query.ContainsKey("special"),
    branch =>
    {
        branch.Run(context =>
            context.Response.WriteAsync("Special branch"));
    });

app.Run(context =>
    context.Response.WriteAsync("Main pipeline"));
```

При наличии параметра `special` выполняется отдельная ветка. Основной обработчик после `MapWhen` для такого запроса не вызывается.

`MapWhen` не изменяет `Path` и `PathBase`. Его отличие от `Map` — выбор ветки через произвольное условие вместо сопоставления пути.

---

### `UseWhen`: условное включение middleware

Метод из класса `UseWhenExtensions`:

```cs
public static IApplicationBuilder UseWhen(
    this IApplicationBuilder app,
    Func<HttpContext, bool> predicate,
    Action<IApplicationBuilder> configuration);
```

Условие проверяется аналогично `MapWhen`, но ветка связана с продолжением основного конвейера.

```cs
app.UseWhen(
    context => context.Request.Path.StartsWithSegments("/api"),
    branch =>
    {
        branch.Use(async (context, next) =>
        {
            Console.WriteLine("API: до");

            await next(context);

            Console.WriteLine("API: после");
        });
    });

app.Run(async context =>
{
    Console.WriteLine("Основной обработчик");
    await context.Response.WriteAsync("OK");
});
```

Для запроса `/api/products` порядок выполнения:

```
API: до
Основной обработчик
API: после
```

Для остальных запросов выполняется только основной обработчик.

`UseWhen` не изменяет путь запроса. **Продолжение основного конвейера происходит через `next` внутри ветки**, поэтому код после него выполняется уже после последующих основных компонентов.

Если ветка завершает обработку без вызова `next`, например через `Run`, основной конвейер дальше не выполняется.

---

# 6. Порядок middleware

**Middleware выполняются в порядке добавления в конвейер.** Поэтому положение компонента определяет, какие данные ему уже доступны и какие следующие компоненты он может вызвать, пропустить или обернуть своей логикой.

До `await next(context)` код выполняется в порядке регистрации, после — в обратном порядке. Если компонент не вызывает `next`, следующие компоненты не выполняются, но управление возвращается к предыдущим.

---

### Зависимости между компонентами

**Если middleware использует результат работы другого компонента, оно должно находиться после него.**

Например:

- Компонент, которому нужен аутентифицированный `User`, размещают после `UseAuthentication`.
- Компонент, которому нужны сведения о выбранном endpoint, размещают после `UseRouting`.
- `UseAuthorization` размещают после аутентификации и выбора endpoint: ему нужны пользователь и требования доступа к выбранному endpoint.

При этом компоненты, которые должны обрабатывать ошибки или измерять время выполнения последующих компонентов, размещают **перед ними**, чтобы обернуть их вызов через `next`.

Например, обработчик исключений может перехватить исключение из следующего middleware, но не из компонента, который выполняется раньше него.

---

### Порядок стандартных middleware

Состав конвейера зависит от приложения, но для распространённых компонентов используются следующие ориентиры:

|Компонент|Расположение и причина|
|---|---|
|`UseExceptionHandler`|В начале конвейера, чтобы перехватывать исключения из последующих компонентов|
|`UseHttpsRedirection`|До основной обработки, чтобы HTTP-запрос можно было сразу перенаправить на HTTPS|
|`UseStaticFiles`|Часто до маршрутизации и авторизации — для выдачи общедоступных статических файлов|
|`UseRouting`|До компонентов, использующих сведения о выбранном endpoint|
|`UseCors`|После `UseRouting`, перед аутентификацией и авторизацией|
|`UseAuthentication`|Перед авторизацией и другими компонентами, которым нужен аутентифицированный пользователь|
|`UseAuthorization`|После маршрутизации и аутентификации, перед выполнением endpoint|

Это ориентиры для компонентов, присутствующих в приложении, а не обязательный список для каждого проекта.

---

### Досрочное завершение обработки

Расположение middleware определяет, **какие запросы вообще дойдут до следующих компонентов**.

Например:

```cs
app.UseStaticFiles();

app.UseAuthentication();
app.UseAuthorization();
```

Если `UseStaticFiles` найдёт запрошенный файл и выдаст его, middleware аутентификации и авторизации для этого запроса не выполнятся. Поэтому такая схема используется для общедоступных файлов.

Аналогично, middleware логирования, размещённое после `UseStaticFiles`, не увидит запросы, обработанные этим компонентом. Чтобы учитывать их, логирование нужно разместить перед ним.

---

### Порядок middleware и регистрация endpoints

В `WebApplication` вызов `MapGet` **регистрирует endpoint, а не вставляет его обработчик в текущую позицию цепочки middleware**:

```cs
app.MapGet("/", () => "Hello");

app.Use(async (context, next) =>
{
    Console.WriteLine("До endpoint");

    await next(context);

    Console.WriteLine("После endpoint");
});
```

Несмотря на расположение `MapGet` выше, это middleware оборачивает выполнение endpoint.

`WebApplication` автоматически добавляет маршрутизацию и выполнение endpoints при наличии зарегистрированных endpoints. Если нужно явно определить положение этапа выбора endpoint, используют `UseRouting()`.

При этом терминальный `app.Run(handler)`, расположенный до выполнения endpoints, может остановить запрос и не дать ему дойти до выбранного обработчика.