
---

## Оглавление

- [[#1. Назначение контроллеров и понятие Action|1. Назначение контроллеров и понятие Action]]
    - [[#1.1. Что такое контроллер|1.1. Что такое контроллер]]
    - [[#1.2. Что такое Action|1.2. Что такое Action]]
    - [[#1.3. Контроллер, action и endpoint|1.3. Контроллер, action и endpoint]]
    - [[#1.4. Роль ASP.NET Core MVC|1.4. Роль ASP.NET Core MVC]]
    - [[#1.5. Ответственность контроллера|1.5. Ответственность контроллера]]
	
- [[#2. Подключение: `AddControllers` и `MapControllers`|2. Подключение: AddControllers и MapControllers]]
    - [[#2.1. `AddControllers`: регистрация сервисов|2.1. AddControllers: регистрация сервисов]]
    - [[#2.2. `MapControllers`: регистрация endpoints|2.2. MapControllers: регистрация endpoints]]
    - [[#2.3. Минимальный пример|2.3. Минимальный пример]]
    - [[#2.4. Совместное использование с Minimal API|2.4. Совместное использование с Minimal API]]
	
- [[#3. Устройство контроллера: `ControllerBase`|3. Устройство контроллера: ControllerBase]]
    - [[#3.1. Какие классы считаются контроллерами|3.1. Какие классы считаются контроллерами]]
    - [[#3.2. Какие методы считаются actions|3.2. Какие методы считаются actions]]
    - [[#3.3. Основные свойства `ControllerBase`|3.3. Основные свойства ControllerBase]]
    - [[#3.4. Конструктор и внедрение зависимостей|3.4. Конструктор и внедрение зависимостей]]
    - [[#3.5. Время жизни экземпляра|3.5. Время жизни экземпляра]]
	
- [[#4. Маршрутизация через атрибуты|4. Маршрутизация через атрибуты]]
    - [[#4.1. `[Route]`: шаблон маршрута|4.1. [Route]: шаблон маршрута]]
    - [[#4.2. Атрибуты HTTP-методов|4.2. Атрибуты HTTP-методов]]
    - [[#4.3. Объединение маршрутов контроллера и action|4.3. Объединение маршрутов контроллера и action]]
    - [[#4.4. Абсолютные шаблоны|4.4. Абсолютные шаблоны]]
    - [[#4.5. Подстановки `[controller]` и `[action]`|4.5. Подстановки [controller] и [action]​]]
    - [[#4.6. Несколько маршрутов для одного action|4.6. Несколько маршрутов для одного action]]
    - [[#4.7. Имя маршрута и приоритет|4.7. Имя маршрута и приоритет]]
    - [[#4.8. Отличие от маршрутизации по соглашениям|4.8. Отличие от маршрутизации по соглашениям]]
	
- [[#5. Поведение `[ApiController]`|5. Поведение [ApiController]​]]
    - [[#5.1. Отличие от `ControllerBase`|5.1. Отличие от ControllerBase]]
    - [[#5.2. Обязательность маршрутизации через атрибуты|5.2. Обязательность маршрутизации через атрибуты]]
    - [[#5.3. Автоматическое определение источников параметров|5.3. Автоматическое определение источников параметров]]
    - [[#5.4. Автоматический ответ `400`|5.4. Автоматический ответ 400]]
    - [[#5.5. Дополнительные соглашения|5.5. Дополнительные соглашения]]
    - [[#5.6. Настройка через `ApiBehaviorOptions`|5.6. Настройка через ApiBehaviorOptions]]
	
- [[#6. Параметры actions и model binding|6. Параметры actions и model binding]]
    - [[#6.1. Явное указание источника|6.1. Явное указание источника]]
    - [[#6.2. Route, query и headers|6.2. Route, query и headers]]
    - [[#6.3. DTO из тела запроса и query string|6.3. DTO из тела запроса и query string]]
    - [[#6.4. Коллекции|6.4. Коллекции]]
    - [[#6.5. Формы и файлы|6.5. Формы и файлы]]
    - [[#6.6. Сервисы и `CancellationToken`|6.6. Сервисы и CancellationToken]]
    - [[#6.7. Отсутствующие значения и ошибки преобразования|6.7. Отсутствующие значения и ошибки преобразования]]
    - [[#6.8. Отличия от binding в Minimal API|6.8. Отличия от binding в Minimal API]]
	
- [[#7. Валидация и `ModelState`|7. Валидация и ModelState]]
    - [[#7.1. Отличие валидации от model binding|7.1. Отличие валидации от model binding]]
    - [[#7.2. Правила валидации DTO|7.2. Правила валидации DTO]]
    - [[#7.3. Что содержит `ModelState`|7.3. Что содержит ModelState]]
    - [[#7.4. Автоматический и ручной возврат ошибок|7.4. Автоматический и ручной возврат ошибок]]
    - [[#7.5. Проверка нескольких свойств|7.5. Проверка нескольких свойств]]
    - [[#7.6. Повторная валидация|7.6. Повторная валидация]]
    - [[#7.7. Входные ограничения и бизнес-правила|7.7. Входные ограничения и бизнес-правила]]
	
- [[#8. Возвращаемые значения actions|8. Возвращаемые значения actions]]
    - [[#8.1. Возврат обычного значения|8.1. Возврат обычного значения]]
    - [[#8.2. `IActionResult`|8.2. IActionResult]]
    - [[#8.3. `ActionResult<T>`|8.3. ActionResult<T>]]
    - [[#8.4. Асинхронные actions|8.4. Асинхронные actions]]
    - [[#8.5. Основные методы формирования ответа|8.5. Основные методы формирования ответа]]
    - [[#8.6. Создание ресурса: `Created`, `CreatedAtAction`, `CreatedAtRoute`|8.6. Создание ресурса: Created, CreatedAtAction, CreatedAtRoute]]
    - [[#8.7. `Problem`: описание ошибки|8.7. Problem: описание ошибки]]
    - [[#8.8. Отличие от результатов Minimal API|8.8. Отличие от результатов Minimal API]]
	
- [[#9. Формат ответа и метаданные API|9. Формат ответа и метаданные API]]
    - [[#9.1. `Accept` и `Content-Type`|9.1. Accept и Content-Type]]
    - [[#9.2. Content negotiation|9.2. Content negotiation]]
    - [[#9.3. Результаты с фиксированным форматом|9.3. Результаты с фиксированным форматом]]
    - [[#9.4. `[Produces]`: формат ответа|9.4. [Produces]: формат ответа]]
    - [[#9.5. `[Consumes]`: формат входного тела|9.5. [Consumes]: формат входного тела]]
    - [[#9.6. `[ProducesResponseType]`: описание возможных ответов|9.6. [ProducesResponseType]: описание возможных ответов]]
    - [[#9.7. Настройка JSON|9.7. Настройка JSON]]
	
- [[#10. Фильтры MVC|10. Фильтры MVC]]
    - [[#10.1. Место фильтров в pipeline|10.1. Место фильтров в pipeline]]
    - [[#10.2. Виды фильтров|10.2. Виды фильтров]]
    - [[#10.3. Action filters|10.3. Action filters]]
    - [[#10.4. Short-circuit|10.4. Short-circuit]]
    - [[#10.5. Регистрация и DI|10.5. Регистрация и DI]]
    - [[#10.6. Порядок выполнения|10.6. Порядок выполнения]]
    - [[#10.7. Result filters|10.7. Result filters]]
    - [[#10.8. Exception filters|10.8. Exception filters]]

---

# 1. Назначение контроллеров и понятие Action

### 1.1. Что такое контроллер

> [!info] Определение  
> **Контроллер** — класс, который объединяет методы обработки HTTP-запросов, связанные по назначению. Эти методы называются **actions** — методами действий.

Например, `{cs}ProductsController` может содержать действия для получения, создания, изменения и удаления товаров.

Группировка позволяет задавать общие настройки на уровне класса: префикс маршрутов, требования авторизации и другие правила обработки. 

API-контроллеры обычно наследуются от `{cs}ControllerBase`. Этот класс предоставляет доступ к текущему запросу и методы формирования HTTP-результатов, например `{cs}Ok()`, `{cs}NotFound()` и `{cs}BadRequest()`. 

---

### 1.2. Что такое Action

> [!info] Определение  
> **Action** — метод контроллера, который инфраструктура MVC распознаёт как обработчик запросов. Он получает параметры, выполняет необходимую работу и возвращает результат для формирования ответа.

Пример контроллера с двумя actions:

```cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("products")]
public class ProductsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok(new[] { "Keyboard", "Mouse" });
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        return Ok(new { id });
    }
}
```

| Запрос             | Вызываемый action |
| ------------------ | ----------------- |
| `GET /products`    | `{cs}GetAll()`    |
| `GET /products/42` | `{cs}GetById(42)` |

В этом примере:

- `{cs}[Route("products")]` задаёт общий префикс маршрутов.
- `{cs}[HttpGet]` связывает action с HTTP-методом `GET`.
- `{cs}[HttpGet("{id:int}")]` дополнительно задаёт шаблон пути.
- `{cs}Ok(...)` создаёт результат успешного ответа с переданными данными.

Параметр `{cs}id` заполняется инфраструктурой из маршрута: action получает уже преобразованное значение `{cs}int`.

**Имя метода само по себе не определяет HTTP-метод запроса:** в примере обработка `GET` задана атрибутами. 

---

### 1.3. Контроллер, action и endpoint

Это связанные понятия, но каждое обозначает свою часть обработки:

| Понятие    | Назначение                                                                 |
| ---------- | -------------------------------------------------------------------------- |
| Контроллер | Класс, объединяющий actions и общие настройки                              |
| Action     | Метод, выполняющий обработку                                               |
| Endpoint   | Зарегистрированная точка обработки с маршрутом, обработчиком и метаданными |

Для actions создаются endpoints. При обработке запроса маршрутизация выбирает подходящий endpoint, после чего инфраструктура MVC обеспечивает вызов соответствующего метода контроллера.

В общих чертах обработка выглядит так:

1. Маршрутизация выбирает endpoint.
2. MVC получает экземпляр контроллера и подготавливает параметры action.
3. Вызывается action.
4. Его результат используется для формирования HTTP-ответа.

Обработка также может завершиться до вызова action — например, при запрете доступа или ошибках входных данных. 

---

### 1.4. Роль ASP.NET Core MVC

**ASP.NET Core MVC** — инфраструктура для разработки веб-приложений и HTTP API. Она обеспечивает работу контроллеров, привязку и валидацию параметров, выполнение фильтров и формирование ответов.

Название происходит от архитектурного паттерна **Model–View–Controller**:

|Часть|Ответственность|
|---|---|
|Model|Данные, состояние и бизнес-правила приложения|
|View|Представление данных пользователю|
|Controller|Обработка входящего запроса и координация работы|

В HTTP API используется поддержка контроллеров и обработки данных; HTML-представления не обязательны. Контроллер может возвращать JSON, файл или ответ только со статусом. 

---

### 1.5. Ответственность контроллера

Обычно action:

1. Получает подготовленные входные данные.
2. Вызывает сервис, выполняющий операцию приложения.
3. Выбирает HTTP-результат: успешный ответ, отсутствие ресурса, ошибку и т. д.

**Бизнес-логику и работу с хранилищами обычно выносят в отдельные компоненты.** Контроллер связывает HTTP-запрос с операцией приложения и переводит её результат в HTTP-ответ. 

В Minimal API обработчики регистрируются через `{cs}MapGet()`, `{cs}MapPost()` и другие методы. При использовании контроллеров обработчики оформляются как методы классов, а маршруты и настройки задаются преимущественно атрибутами. Оба подхода работают через общую маршрутизацию и конвейер middleware

---

# 2. Подключение: `AddControllers` и `MapControllers`

Для подключения API-контроллеров используются два метода:

|Метод|Назначение|
|---|---|
|`AddControllers()`|Регистрирует сервисы MVC, необходимые для работы контроллеров|
|`MapControllers()`|Регистрирует endpoints для actions с маршрутизацией через атрибуты|

Первый вызывается при настройке сервисов, второй — при регистрации endpoints приложения.

---

### 2.1. `AddControllers`: регистрация сервисов

`{cs}AddControllers()` — метод расширения для `{cs}IServiceCollection`. Он подключает инфраструктуру обработки запросов через контроллеры: вызов actions, привязку и валидацию параметров, формирование ответов и другие необходимые возможности MVC.

Имеет две перегрузки: 

```cs
public static IMvcBuilder AddControllers(
    this IServiceCollection services);

public static IMvcBuilder AddControllers(
    this IServiceCollection services,
    Action<MvcOptions>? configure);
```

Обычное подключение:

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
```

Перегрузка с `{cs}configure` позволяет дополнительно настроить `{cs}MvcOptions`: например, глобальные фильтры и параметры валидации.

#### Возвращаемое значение: `IMvcBuilder`

Метод возвращает `{cs}IMvcBuilder` — объект для дальнейшей настройки сервисов MVC. Через его методы расширения можно, например:

|Метод|Назначение|
|---|---|
|`AddJsonOptions(...)`|Настройка JSON для контроллеров|
|`ConfigureApiBehaviorOptions(...)`|Настройка поведения API-контроллеров|
|`AddMvcOptions(...)`|Дополнительная настройка `MvcOptions`|

Это позволяет продолжать настройку цепочкой вызовов после `{cs}AddControllers()`. 

---

### 2.2. `MapControllers`: регистрация endpoints

`{cs}MapControllers()` — метод расширения для `{cs}IEndpointRouteBuilder`:

```cs
public static ControllerActionEndpointConventionBuilder MapControllers(
    this IEndpointRouteBuilder endpoints);
```

Он подключает endpoints actions, маршруты которых заданы атрибутами — например, `{cs}[Route]` и `{cs}[HttpGet]`. Сам метод не принимает шаблон маршрута. 

В `{cs}WebApplication` вызывается после сборки приложения:

```cs
var app = builder.Build();

app.MapControllers();
```

**Один вызов подключает actions всех обнаруженных контроллеров.** Регистрировать каждый контроллер или action отдельным вызовом не требуется.

Метод возвращает `{cs}ControllerActionEndpointConventionBuilder`, реализующий `{cs}IEndpointConventionBuilder`. Через него можно задавать общие настройки endpoints контроллеров, например требования авторизации или дополнительные метаданные. 

> [!note] Регистрация и выполнение  
> `{cs}AddControllers()` подключает сервисы обработки, а `{cs}MapControllers()` делает actions доступными через маршрутизацию. Вызов action происходит позднее — при обработке подходящего запроса.

---

### 2.3. Минимальный пример

#### `Program.cs`

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

var app = builder.Build();

app.MapControllers();

app.Run();
```

#### `ProductsController.cs`

```cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("products")]
public class ProductsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok(new[] { "Keyboard", "Mouse" });
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        return Ok(new { id });
    }
}
```

Приложение предоставляет два endpoint:

|Запрос|Action|Ответ|
|---|---|---|
|`GET /products`|`GetAll()`|JSON-массив названий|
|`GET /products/42`|`GetById(42)`|JSON-объект с `id = 42`|

Маршруты берутся из атрибутов контроллера и его методов. В `{cs}Program.cs` их повторять не требуется. 

---

### 2.4. Совместное использование с Minimal API

В одном приложении можно регистрировать и endpoints контроллеров, и обработчики Minimal API:

```cs
app.MapControllers();

app.MapGet("/health", () => "OK");
```

Все они участвуют в общей маршрутизации. `{cs}MapControllers()` регистрирует endpoints, поэтому положение его вызова среди других методов `{cs}Map...()` не задаёт последовательность выполнения обработчиков. Подходящий endpoint выбирается по условиям маршрутизации.

---

# 3. Устройство контроллера: `ControllerBase`

`{cs}ControllerBase` — абстрактный базовый класс для контроллеров, предоставляющий доступ к текущему запросу и методы формирования HTTP-результатов:

```cs
[Controller]
public abstract class ControllerBase
```

Он находится в пространстве имён `{cs}Microsoft.AspNetCore.Mvc`. API-контроллер обычно наследуется от него: 

```cs
[ApiController]
[Route("products")]
public class ProductsController : ControllerBase
{
    // Actions и зависимости контроллера
}
```

---

### 3.1. Какие классы считаются контроллерами

При стандартном обнаружении MVC рассматривает класс как контроллер, если он:

- Публичный и объявлен вне другого класса.
- Не абстрактный.
- Не содержит незаданных параметров типа — например, открытый `{cs}ProductsController<T>` не подходит.
- Не помечен атрибутом `{cs}[NonController]`.

Дополнительно должно выполняться хотя бы одно условие:

- Имя класса заканчивается на `Controller`.
- Класс имеет атрибут `{cs}[Controller]`, в том числе унаследованный.

`{cs}ControllerBase` уже помечен `{cs}[Controller]`, поэтому его наследники получают этот признак. **Наследование не обязательно для обнаружения контроллера, но предоставляет готовые свойства и методы для обработки запросов.** 

 Для организации проекта используется папка `Controllers`.

---

### 3.2. Какие методы считаются actions

В обычном случае action — это **публичный метод экземпляра контроллера**.

Метод не должен быть статическим, абстрактным или обобщённым. Конструкторы, методы доступа к свойствам и служебные методы вроде `{cs}ToString()` также не рассматриваются как actions.

Атрибут `{cs}[NonAction]` явно исключает метод из actions: 

```cs
[NonAction]
public string NormalizeName(string name)
{
    return name.Trim();
}
```

Такой метод остаётся обычным методом класса: его можно вызвать из кода, но MVC не использует его как action.

Для внутренних вспомогательных методов обычно достаточно `{cs}private` или `{cs}protected`.

> [!note] Атрибут HTTP-метода не определяет наличие action  
> Публичный метод может распознаваться как action и без `{cs}[HttpGet]` или `{cs}[HttpPost]`. Эти атрибуты задают условия маршрутизации. Для исключения публичного метода используется `{cs}[NonAction]`.

---

### 3.3. Основные свойства `ControllerBase`

|Свойство|Тип|Назначение|
|---|---|---|
|`HttpContext`|`HttpContext`|Контекст текущего запроса|
|`Request`|`HttpRequest`|Текущий HTTP-запрос|
|`Response`|`HttpResponse`|Текущий HTTP-ответ|
|`User`|`ClaimsPrincipal`|Пользователь текущего запроса|
|`RouteData`|`RouteData`|Данные маршрутизации, включая значения параметров|
|`ModelState`|`ModelStateDictionary`|Состояние привязки и валидации входных данных|
|`ControllerContext`|`ControllerContext`|Контекст выполнения MVC со сведениями о текущем action|
|`Url`|`IUrlHelper`|Генерация ссылок на actions и маршруты|

Эти свойства предоставляются базовым классом и доступны непосредственно в методах контроллера. 

Например:

```cs
string method = Request.Method;
string? userName = User.Identity?.Name;
string traceId = HttpContext.TraceIdentifier;

object? id = RouteData.Values["id"];
```

`{cs}Request`, `{cs}Response` и `{cs}User` обращаются к соответствующим объектам текущего `{cs}HttpContext`.

> [!warning] Контекст в конструкторе  
> MVC устанавливает контекст контроллера после создания экземпляра. Поэтому обращаться к его свойствам `{cs}HttpContext`, `{cs}Request` и `{cs}User` следует в actions, а не в конструкторе. 

---

### 3.4. Конструктор и внедрение зависимостей

Зависимости объявляют параметрами публичного конструктора. При создании контроллера MVC получает их из DI:

```cs
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Logging;

[ApiController]
[Route("products")]
public class ProductsController : ControllerBase
{
    private readonly ILogger<ProductsController> _logger;

    public ProductsController(ILogger<ProductsController> logger)
    {
        _logger = logger;
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        _logger.LogInformation(
            "Запрошен товар {ProductId}", id);

        return Ok(new { id });
    }
}
```

Поля позволяют использовать полученные зависимости в разных actions. Пользовательские сервисы предварительно регистрируют в DI; поддержка `{cs}ILogger<T>` уже подключена стандартным приложением.

Зависимость также можно получить через параметр отдельного action, явно указав `{cs}[FromServices]`. 

---

### 3.5. Время жизни экземпляра

**По умолчанию MVC создаёт отдельный экземпляр контроллера для каждого обрабатываемого им запроса.** После обработки экземпляр освобождается; если контроллер реализует интерфейс освобождения ресурсов, вызывается соответствующий метод.

Поэтому значения обычных полей контроллера не сохраняются между запросами. Например, счётчик в поле экземпляра не будет общим счётчиком обращений к API. 

При этом зависимости контроллера сохраняют время жизни, заданное их регистрацией: новый экземпляр контроллера может получить тот же singleton-сервис или scoped-сервис текущего запроса.

По умолчанию сам класс контроллера отдельно регистрировать в DI не требуется: MVC создаёт его, используя DI для получения зависимостей конструктора. 

---

# 4. Маршрутизация через атрибуты

> [!info] Определение  
> **Маршрутизация через атрибуты (attribute routing)** — способ задания маршрутов непосредственно на классах контроллеров и их actions с помощью атрибутов.

Атрибуты описывают шаблоны пути и допустимые HTTP-методы. На их основе MVC создаёт endpoints, подключаемые через `{cs}MapControllers()`.

---

### 4.1. `[Route]`: шаблон маршрута

`{cs}[Route]` можно применить к контроллеру или action. Он задаёт шаблон пути:

```cs
public RouteAttribute(string template);
```

На контроллере обычно задают общий префикс:

```cs
[Route("api/products")]
public class ProductsController : ControllerBase
{
    // Actions
}
```

На action — маршрут конкретной операции:

```cs
[Route("api/products/{id:int}")]
public IActionResult GetById(int id)
{
    return Ok(new { id });
}
```

---

### 4.2. Атрибуты HTTP-методов

Для задания HTTP-метода используются отдельные атрибуты:

|Атрибут|HTTP-метод|
|---|---|
|`[HttpGet]`|`GET`|
|`[HttpPost]`|`POST`|
|`[HttpPut]`|`PUT`|
|`[HttpDelete]`|`DELETE`|
|`[HttpPatch]`|`PATCH`|
|`[HttpHead]`|`HEAD`|
|`[HttpOptions]`|`OPTIONS`|

Эти атрибуты поддерживают две формы: без шаблона и с шаблоном маршрута. Например, конструкторы `{cs}HttpGetAttribute`: 

```cs
public HttpGetAttribute();

public HttpGetAttribute(string template);
```

Поэтому можно написать:

```cs
[HttpGet]
```

или:

```cs
[HttpGet("{id:int}")]
```

Во втором случае атрибут одновременно задаёт **шаблон пути и ограничение по HTTP-методу**. Дополнительный `{cs}[Route("{id:int}")]` не требуется.

Также допустимо разделить эти настройки:

```cs
[Route("{id:int}")]
[HttpGet]
public IActionResult GetById(int id)
{
    return Ok(new { id });
}
```

#### Несколько HTTP-методов: `[AcceptVerbs]`

`{cs}[AcceptVerbs]` позволяет перечислить допустимые методы, в том числе те, для которых нет отдельного атрибута:

```cs
public AcceptVerbsAttribute(string method);

public AcceptVerbsAttribute(params string[] methods);
```

Шаблон передаётся через свойство `{cs}Route`: 

```cs
[AcceptVerbs("QUERY", "POST", Route = "{id:int}")]
public IActionResult GetById(int id)
{
    return Ok(new { id });
}
```

---

### 4.3. Объединение маршрутов контроллера и action

**Шаблон контроллера становится префиксом шаблона action.**

```cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/products")]
public class ProductsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok(new[] { "Keyboard", "Mouse" });
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        return Ok(new { id });
    }
}
```

|Шаблон контроллера|Атрибут action|Итоговый маршрут|
|---|---|---|
|`api/products`|`[HttpGet]`|`GET /api/products`|
|`api/products`|`[HttpGet("{id:int}")]`|`GET /api/products/{id:int}`|

Если action не задаёт дополнительный шаблон, используется путь контроллера. Без шаблона на контроллере путь полностью задаётся на action. 

В шаблонах действует обычный синтаксис маршрутов: параметры, ограничения, необязательные значения, значения по умолчанию и catch-all.

Один путь может использоваться разными actions с разными HTTP-методами: например, `{http}GET /api/products` для получения списка и `{http}POST /api/products` для создания товара.

---

### 4.4. Абсолютные шаблоны

Если шаблон action начинается с `/` или `~/`, **префикс контроллера к нему не добавляется**.

Например, внутри контроллера с `{cs}[Route("api/products")]`:

```cs
[HttpGet("/status")]
public IActionResult GetStatus()
{
    return Ok("OK");
}
```

Итоговый маршрут — `{http}GET /status`.

Запись `{cs}[HttpGet("~/status")]` даёт тот же результат. Здесь «абсолютный» означает независимость от префикса контроллера; схему и адрес сервера такой шаблон не задаёт. 

---

### 4.5. Подстановки `[controller]` и `[action]`

В шаблонах можно использовать подстановки имён:

|Подстановка|Значение|
|---|---|
|`[controller]`|Имя контроллера без суффикса `Controller`|
|`[action]`|Имя action в MVC|

```cs
[ApiController]
[Route("api/[controller]/[action]")]
public class ProductsController : ControllerBase
{
    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        return Ok(new { id });
    }
}
```

Итоговый шаблон — `/api/Products/GetById/{id:int}`.

Подстановки заменяются при построении маршрутов. Поэтому переименование контроллера или action может изменить URL. При явно заданном пути вроде `"api/products"` имена классов и методов на этот путь не влияют. 

> [!note] Подстановка и параметр маршрута  
> `[controller]` подставляет заранее известное имя контроллера, а `{id}` обозначает значение, извлекаемое из пути входящего запроса.

---

### 4.6. Несколько маршрутов для одного action

На одном action можно указать несколько маршрутов:

```cs
[HttpGet("{id:int}")]
[HttpGet("by-id/{id:int}")]
public IActionResult GetById(int id)
{
    return Ok(new { id });
}
```

При префиксе `api/products` оба запроса вызовут этот метод:

- `{http}GET /api/products/42`
- `{http}GET /api/products/by-id/42`

Несколько `{cs}[Route]` на контроллере задают несколько префиксов. Каждый относительный шаблон action объединяется с каждым префиксом контроллера. **Один action таким образом может быть связан с несколькими endpoints.** 

---

### 4.7. Имя маршрута и приоритет

У `{cs}[Route]` и атрибутов HTTP-методов есть свойства:

|Свойство|Тип|Назначение|
|---|---|---|
|`Name`|`string?`|Имя маршрута для генерации ссылок|
|`Order`|`int`|Приоритет, учитываемый при выборе endpoint|

#### `Name`: именование маршрута

```cs
[HttpGet("{id:int}", Name = "GetProduct")]
public IActionResult GetById(int id)
{
    return Ok(new { id });
}
```

Имя можно использовать для генерации ссылки:

```cs
string? path = Url.RouteUrl(
    "GetProduct",
    new { id = 42 });

// /api/products/42
```

**Имя не меняет путь и не участвует в сопоставлении входящего запроса.** Для именованных endpoints следует использовать уникальные имена в пределах приложения. 

#### `Order`: приоритет маршрута

```cs
[HttpGet("{id:int}", Order = -1)]
```

Меньшее значение означает больший приоритет. Если порядок не задан ни на action, ни на контроллере, используется `0`. Явно заданное значение action имеет приоритет над значением контроллера.

Обычно достаточно различий в шаблонах и HTTP-методах; `{cs}Order` нужен для явного изменения стандартного выбора. 

---

### 4.8. Отличие от маршрутизации по соглашениям

При маршрутизации через атрибуты шаблоны задаются непосредственно на контроллерах и actions.

При **маршрутизации по соглашениям** общий шаблон задаётся при регистрации:

```cs
app.MapControllerRoute(
    name: "default",
    pattern: "{controller}/{action}/{id?}");
```

В таком случае путь `/Products/GetById/42` содержит имена контроллера и action, по которым определяется обработчик.

Для API-контроллеров с `{cs}[ApiController]` применяется маршрутизация через атрибуты. Их подключают через `{cs}MapControllers()`. 

---

# 5. Поведение `[ApiController]`

> [!info] Определение  
> **`{cs}[ApiController]`** — атрибут, который включает для контроллера набор правил обработки HTTP API: определение источников параметров, автоматические ответы при ошибках входных данных и другие соглашения.

Атрибут находится в пространстве имён `{cs}Microsoft.AspNetCore.Mvc` и применяется к классу контроллера:

```cs
[ApiController]
[Route("products")]
public class ProductsController : ControllerBase
{
    // Actions
}
```

---

### 5.1. Отличие от `ControllerBase`

Наследование от `{cs}ControllerBase` и применение `{cs}[ApiController]` решают разные задачи:

|Механизм|Назначение|
|---|---|
|`ControllerBase`|Предоставляет свойства контекста и методы формирования результатов: `HttpContext`, `ModelState`, `Ok()`, `NotFound()` и другие|
|`[ApiController]`|Включает дополнительные правила обработки, которые применяет инфраструктура MVC|

**Само наследование от `{cs}ControllerBase` не включает поведение `{cs}[ApiController]`.** Контроллер без этого атрибута также может обрабатывать HTTP-запросы и возвращать JSON. 

Атрибут наследуется: его можно поставить на собственный базовый класс контроллеров. Также поддерживается применение ко всей сборке:

```cs
using Microsoft.AspNetCore.Mvc;

[assembly: ApiController]
```

В таком случае правила распространяются на все контроллеры этой сборки. 

---

### 5.2. Обязательность маршрутизации через атрибуты

Для actions контроллера с `{cs}[ApiController]` маршруты должны задаваться атрибутами.

Маршрут может складываться из общего шаблона контроллера и атрибута action:

```cs
[Route("products")]
```

```cs
[HttpGet("{id:int}")]
```

Либо полностью задаваться на самом action.

**Маршрутизация по соглашениям через `{cs}MapControllerRoute()` не заменяет это требование.** При этом сам `{cs}[ApiController]` не задаёт путь или HTTP-метод: для этого используются `{cs}[Route]`, `{cs}[HttpGet]` и другие атрибуты маршрутизации. 

---

### 5.3. Автоматическое определение источников параметров

Если источник параметра не указан явно, MVC определяет его по типу и имени параметра.

Основные правила для обычных параметров:

|Параметр|Определяемый источник|
|---|---|
|Сложный тип, зарегистрированный в DI|Сервисы — аналог `[FromServices]`|
|Обычный сложный тип, не зарегистрированный в DI, например DTO|Тело запроса — аналог `[FromBody]`|
|`IFormFile` или `IFormFileCollection`|Данные формы — аналог `[FromForm]`|
|Простой параметр, имя которого присутствует в шаблоне маршрута|Маршрут — аналог `[FromRoute]`|
|Остальной простой параметр|Query string — аналог `[FromQuery]`|

Специальные типы, например `{cs}CancellationToken`, обрабатываются по собственным правилам.

**Явно указанный источник не заменяется автоматическим определением.** Например, `{cs}[FromQuery]` позволяет получить DTO из query string вместо тела запроса. 

```cs
[HttpGet("{id:int}")]
public IActionResult GetById(int id, string? language)
{
    return Ok(new { id, language });
}
```

Для запроса `{http}GET /products/42?language=ru`:

|Параметр|Источник|Значение|
|---|---|---|
|`id`|Маршрут|`42`|
|`language`|Query string|`"ru"`|

Заголовки по имени параметра автоматически не определяются: для них используется `{cs}[FromHeader]`.

Простые типы вроде `{cs}string` и `{cs}int` не получают источник тела автоматически. Если значение должно читаться из тела, указывают `{cs}[FromBody]`.

Если несколько параметров action оказываются привязанными к телу через `{cs}[FromBody]`, явно или автоматически, MVC выбрасывает исключение при построении описания actions. Обычно необходимые данные объединяют в один DTO. 

---

### 5.4. Автоматический ответ `400`

До вызова action MVC выполняет привязку параметров и валидацию модели. Возникшие ошибки сохраняются в `{cs}ModelState`.

При включённом поведении `{cs}[ApiController]`, если `{cs}ModelState.IsValid` равно `{cs}false`, инфраструктура **возвращает `400 Bad Request`, не вызывая action**. Это выполняет фильтр `{cs}ModelStateInvalidFilter`. 

Например, внутри контроллера:

```cs
[HttpPost]
public IActionResult Create(CreateProductRequest request)
{
    return Ok(request);
}
```

DTO:

```cs
using System.ComponentModel.DataAnnotations;

public class CreateProductRequest
{
    [Required]
    public string? Name { get; set; }
}
```

Если в JSON передать `"name": null` или пустую строку, проверка `{cs}[Required]` завершится ошибкой. Метод `{cs}Create()` не выполнится.

Аналогично, ошибка преобразования query-параметра в число может сделать модель недопустимой. Поэтому отдельная проверка `{cs}ModelState.IsValid` в начале каждого action обычно не требуется. 

По умолчанию ответ содержит `{cs}ValidationProblemDetails`: статус, описание ошибки и коллекцию `{cs}errors` с ошибками отдельных полей. 

> [!note] Граница автоматической проверки  
> Автоматический ответ относится к ошибкам, уже попавшим в `{cs}ModelState` до вызова action. Он не проверяет самостоятельно существование товара, достаточность средств или другие правила прикладной операции.

---

### 5.5. Дополнительные соглашения

#### Тип содержимого при загрузке файлов

Для параметров `{cs}IFormFile` и `{cs}IFormFileCollection` MVC автоматически добавляет требование к типу содержимого запроса — `multipart/form-data`, если оно не задано явно.

Это дополняет определение источника формы: инфраструктура также учитывает ожидаемый `{http}Content-Type` запроса. 

#### Формат ошибок: `ProblemDetails`

Некоторые результаты со статусом ошибки автоматически преобразуются в ответ с `{cs}ProblemDetails`.

Например:

```cs
return NotFound();
```

По умолчанию такой результат формирует `404` с описанием ошибки в теле.

Это не означает преобразование любого ответа со статусом `400` и выше. Например, `{cs}BadRequest(new { message = "Ошибка" })` уже содержит собственный объект ответа, который этот механизм не заменяет. Автоматическое преобразование применяется к поддерживаемым результатам ошибок, реализующим `{cs}IClientErrorActionResult`. 

---

### 5.6. Настройка через `ApiBehaviorOptions`

Правила можно настроить через `{cs}ApiBehaviorOptions`. Для этого используется метод расширения `{cs}ConfigureApiBehaviorOptions()`:

```cs
public static IMvcBuilder ConfigureApiBehaviorOptions(
    this IMvcBuilder builder,
    Action<ApiBehaviorOptions> setupAction);
```

Метод принимает делегат настройки и возвращает тот же `{cs}IMvcBuilder`. 

Например, отключение автоматического ответа при недопустимой модели:

```cs
builder.Services.AddControllers()
    .ConfigureApiBehaviorOptions(options =>
    {
        options.SuppressModelStateInvalidFilter = true;
    });
```

Основные настройки:

|Свойство|Действие|
|---|---|
|`SuppressModelStateInvalidFilter`|При `true` отключает автоматический ответ при недопустимом `ModelState`|
|`SuppressInferBindingSourcesForParameters`|При `true` отключает определение источников параметров по правилам `[ApiController]`|
|`DisableImplicitFromServicesParameters`|При `true` отключает автоматическое определение источника DI; явный `[FromServices]` продолжает работать|
|`SuppressConsumesConstraintForFormFileParameters`|При `true` отключает автоматическое требование `multipart/form-data` для файлов|
|`SuppressMapClientErrors`|При `true` отключает автоматическое преобразование результатов ошибок в `ProblemDetails`|
|`InvalidModelStateResponseFactory`|Задаёт делегат формирования ответа при недопустимом `ModelState`|

Настройки независимы. Например, отключение автоматического `400` **не отключает привязку параметров и валидацию**: ошибки продолжают попадать в `{cs}ModelState`, но выбор ответа становится ответственностью кода приложения. 

---

# 6. Параметры actions и model binding

> [!info] Определение  
> **Model binding** — механизм MVC, который подготавливает аргументы action: получает данные из выбранных источников, преобразует их в .NET-типы и заполняет параметры и свойства моделей. Ошибки привязки сохраняются в `{cs}ModelState`. 

Привязка выполняется **до вызова action**. Поэтому метод получает уже готовые значения: например, число `{cs}42` вместо строки `"42"` из URL.

Model binding работает и без `{cs}[ApiController]`. Этот атрибут добавляет автоматическое определение источников и реакцию на невалидный `{cs}ModelState`, рассмотренные в пункте 5.

В примерах используется контроллер с `{cs}[ApiController]` и базовым маршрутом `/products`. После первого примера показаны отдельные actions и DTO.

### 6.1. Явное указание источника

Атрибуты пространства имён `{cs}Microsoft.AspNetCore.Mvc` определяют, откуда следует получить значение:

|Атрибут|Источник|
|---|---|
|`[FromRoute]`|Значения параметров выбранного маршрута|
|`[FromQuery]`|Query string|
|`[FromHeader]`|HTTP-заголовки|
|`[FromBody]`|Тело запроса, прочитанное input formatter|
|`[FromForm]`|Поля формы в теле запроса|
|`[FromServices]`|DI-контейнер текущего запроса|

Явный атрибут имеет приоритет над автоматическим определением источника. Например, `{cs}[FromQuery]` позволяет привязать DTO из query, хотя обычный DTO-параметр под `{cs}[ApiController]` по умолчанию связывается с телом запроса. 

Источник и HTTP-метод определяются независимо: `{cs}[HttpPost]` выбирает action для POST-запроса, а `{cs}[FromQuery]` читает query string этого запроса.

### 6.2. Route, query и headers

```cs
[ApiController]
[Route("products")]
public class ProductsController : ControllerBase
{
    [HttpGet("{id:int}")]
    public IActionResult GetById(
        [FromRoute(Name = "id")] int productId,
        [FromQuery(Name = "q")] string? search,
        [FromHeader(Name = "X-Request-Id")] string? requestId)
    {
        return Ok(new { productId, search, requestId });
    }
}
```

Запрос:

```http
GET /products/42?q=phone&id=100 HTTP/1.1
Host: example.com
X-Request-Id: req-123
```

В action попадут:

|Параметр|Значение|Откуда получено|
|---|---|---|
|`productId`|`42`|Параметр маршрута `id`|
|`search`|`"phone"`|Query-параметр `q`|
|`requestId`|`"req-123"`|Заголовок `X-Request-Id`|

Свойство `{cs}Name` задаёт имя во внешнем источнике, если оно отличается от имени C#-параметра. Без него используется имя самого параметра. Значение `id=100` из query не влияет на `{cs}productId`, поскольку для него явно выбран route. 

### 6.3. DTO из тела запроса и query string

#### DTO из тела — `[FromBody]`

```cs
public record CreateProductRequest(string Name, decimal Price);
```

```cs
[HttpPost]
public IActionResult Create([FromBody] CreateProductRequest request)
{
    return Ok(new { request.Name, request.Price });
}
```

```http
POST /products HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Keyboard",
  "price": 4500
}
```

MVC передаёт чтение тела **input formatter**, который десериализует содержимое в `{cs}CreateProductRequest`. При стандартной конфигурации JSON обрабатывается через `{cs}System.Text.Json`; другие форматы требуют соответствующих formatters. 

В action попадёт объект с `{cs}Name == "Keyboard"` и `{cs}Price == 4500m`.

> [!warning] Один параметр из тела  
> У action может быть только один параметр, привязываемый через `{cs}[FromBody]`, включая автоматически определённый источник. Несколько объектов следует объединять в один DTO. Параметры из route, query и DI можно использовать вместе с ним. 

Если весь DTO привязывается через `{cs}[FromBody]`, атрибуты источников на его свойствах игнорируются: `{cs}[FromQuery]` на свойстве не заставит JSON formatter прочитать query string. 

#### DTO из query — `[FromQuery]`

```cs
public class ProductFilter
{
    public string? Category { get; set; }
    public decimal? MinPrice { get; set; }
    public int Page { get; set; } = 1;
}
```

```cs
[HttpGet("search")]
public IActionResult Search([FromQuery] ProductFilter filter)
{
    return Ok(filter);
}
```

Для запроса 

```http
GET /products/search?category=books&minPrice=500&page=2
```

будет создан объект:

```cs
new ProductFilter
{
    Category = "books",
    MinPrice = 500m,
    Page = 2
};
```

Здесь объект собирается из отдельных query-параметров. Для такого класса используются публичный конструктор без параметров и публичные свойства с setter. Если `{cs}page` отсутствует, инициализатор свойства сохраняет значение `{cs}1`. 

### 6.4. Коллекции

Несколько значений одного query-параметра можно привязать к массиву или списку:

```cs
[HttpGet("by-ids")]
public IActionResult GetByIds([FromQuery] int[] ids)
{
    return Ok(ids);
}
```

```http
GET /products/by-ids?ids=10&ids=20&ids=30 HTTP/1.1
Host: example.com
```

В `{cs}ids` попадёт массив `{cs}[10, 20, 30]`. Вместо `{cs}int[]` можно использовать `{cs}List<int>`.

Также поддерживается индексированная запись: `ids[0]=10&ids[1]=20`. Запись `ids=10,20` сама по себе не означает два целых числа: стандартная привязка коллекции не разделяет такое значение по запятой. 

### 6.5. Формы и файлы

#### Поля формы — `[FromForm]`

```cs
[HttpPost("form")]
public IActionResult CreateFromForm(
    [FromForm] string name,
    [FromForm] decimal price)
{
    return Ok(new { name, price });
}
```

```http
POST /products/form HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded

name=Keyboard&price=4500
```

Параметры получат значения `{cs}"Keyboard"` и `{cs}4500m`. По умолчанию имена полей совпадают с именами параметров; изменить сопоставление можно через `{cs}Name`.

Через `{cs}[FromForm]` можно привязывать и целый DTO. Для форм используются `application/x-www-form-urlencoded` или `multipart/form-data`; JSON обрабатывается через `{cs}[FromBody]`. 

#### Файлы — `IFormFile`

```cs
[HttpPost("upload")]
public IActionResult Upload(
    IFormFile file,
    [FromForm] string? description)
{
    return Ok(new
    {
        file.FileName,
        file.Length,
        description
    });
}
```

Запрос должен использовать `multipart/form-data` и содержать:

|Имя части|Содержимое|
|---|---|
|`file`|Загружаемый файл|
|`description`|Необязательное текстовое описание|

Для `{cs}IFormFile` под `{cs}[ApiController]` источник формы определяется автоматически. Имя файловой части должно соответствовать имени параметра.

Для нескольких файлов можно использовать `{cs}IFormFileCollection` или `{cs}List<IFormFile>`. Model binding предоставляет доступ к загруженным данным; сохранение файла в постоянное хранилище выполняет код приложения. 

### 6.6. Сервисы и `CancellationToken`

#### Сервис из DI — `[FromServices]`

```cs
[HttpGet("diagnostics")]
public IActionResult Diagnostics(
    [FromServices] ILogger<ProductsController> logger)
{
    logger.LogInformation("Diagnostics requested");

    return Ok(new { status = "ok" });
}
```

Значение `{cs}logger` получается из DI-контейнера текущего запроса. Такая инъекция удобна для зависимости, которую использует только один action. 

#### Токен отмены запроса

Параметр `{cs}CancellationToken` автоматически получает `{cs}HttpContext.RequestAborted`. Атрибут источника ему не нужен. 

В следующем примере `{cs}IProductService` зарегистрирован в DI, а его метод `{cs}GetAsync` принимает идентификатор и токен отмены:

```cs
[HttpGet("{id:int}/details")]
public async Task<IActionResult> GetDetails(
    [FromRoute] int id,
    [FromServices] IProductService service,
    CancellationToken cancellationToken)
{
    var product = await service.GetAsync(id, cancellationToken);

    if (product is null)
        return NotFound();

    return Ok(product);
}
```

Токен позволяет передать отмену запроса выполняемым операциям. Вызываемые методы должны учитывать переданный токен.

### 6.7. Отсутствующие значения и ошибки преобразования

```cs
[HttpGet("paged")]
public IActionResult GetPage(
    [FromQuery] int page = 1,
    [FromQuery] int? categoryId = null,
    [FromQuery] string? search = null)
{
    return Ok(new { page, categoryId, search });
}
```

Для запроса `{http}GET /products/paged` будут использованы `{cs}page == 1`, `{cs}categoryId == null` и `{cs}search == null`: значения по умолчанию задаются в сигнатуре action. 

Отсутствие значения и некорректное значение — разные ситуации:

|Объявление|Параметр отсутствует|Передано `page=abc`|
|---|---|---|
|`[FromQuery] int page`|`0` по умолчанию|Ошибка привязки|
|`[FromQuery] int page = 1`|`1`|Ошибка привязки|
|`[FromQuery] int? page`|`null`|Ошибка привязки|

Nullable-тип допускает отсутствие значения, но не отменяет преобразование предоставленной строки в число. Ошибка преобразования записывается в `{cs}ModelState`; при стандартном поведении `{cs}[ApiController]` возвращается `{http}400 Bad Request`, а action не вызывается. 

> [!note] Обязательность параметра  
> Не-nullable `{cs}int` у контроллера сам по себе не требует присутствия значения в запросе. Требования к наличию и допустимости входных данных задаются отдельно; это относится к следующему пункту о валидации.

### 6.8. Отличия от binding в Minimal API

Контроллеры используют механизм MVC model binding. Совпадающие атрибуты источников не означают полностью одинаковое поведение.

|Ситуация|Controller action|Minimal API handler|
|---|---|---|
|Отсутствует query-параметр `int page` без значения по умолчанию|Обычно используется `0`|Обязательный параметр отсутствует → `400`|
|Несколько query-параметров нужно собрать в DTO|`[FromQuery] ProductFilter filter`|Обычно отдельные параметры или `[AsParameters]`|
|Требуется текущий HTTP-контекст|Свойства `HttpContext`, `Request`, `Response` контроллера|Специальные параметры `HttpContext`, `HttpRequest`, `HttpResponse`|
|Чтение тела через `[FromBody]`|Input formatter MVC|JSON-десериализация|

В частности, `{cs}[AsParameters]` предназначен для Minimal API; для привязки query DTO в контроллере он не требуется. 

---

# 7. Валидация и `ModelState`

> [!info] Определение  
> **Валидация модели** — проверка привязанных входных данных на соответствие заданным правилам: обязательности, диапазонам, ограничениям длины и другим условиям. В MVC она выполняется до вызова action, а результаты сохраняются в `{cs}ModelState`. 

### 7.1. Отличие валидации от model binding

**Model binding** отвечает за получение и преобразование данных, а **валидация** — за допустимость полученного значения.

Например, для числового поля с ограничением от 1 до 100:

|Входные данные|Результат|
|---|---|
|`"abc"`|Ошибка binding: строку невозможно преобразовать в число|
|`0`|Преобразование успешно, но значение не проходит валидацию|
|`10`|Преобразование и валидация успешны|

Оба вида ошибок попадают в `{cs}ModelState`. Поэтому `{cs}ModelState.IsValid` отражает не только результат проверки атрибутов, но и ошибки получения входных данных. 

### 7.2. Правила валидации DTO

Стандартные атрибуты находятся в пространстве имён `{cs}System.ComponentModel.DataAnnotations`.

```cs
using System.ComponentModel.DataAnnotations;

public class CreateProductRequest
{
    [Required(ErrorMessage = "Название обязательно")]
    [StringLength(
        100,
        MinimumLength = 2,
        ErrorMessage = "Название должно содержать от 2 до 100 символов")]
    public string? Name { get; set; }

    [Required(ErrorMessage = "Количество обязательно")]
    [Range(
        1,
        1000,
        ErrorMessage = "Количество должно быть от 1 до 1000")]
    public int? Quantity { get; set; }
}
```

Основные ограничения:

|Атрибут|Проверка|
|---|---|
|`[Required]`|Значение не равно `null`; строка по умолчанию также не может быть пустой или состоять из пробелов|
|`[StringLength(max, MinimumLength = min)]`|Длина строки находится в заданных пределах|
|`[MinLength(n)]` / `[MaxLength(n)]`|Минимальная или максимальная длина строки либо коллекции|
|`[Range(min, max)]`|Значение находится в заданном диапазоне|
|`[EmailAddress]`|Строка соответствует проверяемому формату email|

Границы обычного `{cs}[Range]` включаются в допустимый диапазон. Ограничение длины само по себе не делает строку обязательной: для запрета `{cs}null` используется `{cs}[Required]`. 

#### `[Required]` и числовые значения

Атрибут `{cs}[Required]` проверяет **полученное значение**, а не факт присутствия поля в исходном запросе.

Для свойства `{cs}int Quantity` отсутствующее поле обычно оставляет `{cs}0`. Это полноценное значение `{cs}int`, поэтому `{cs}[Required]` его не отклоняет.

Объявление `{cs}int? Quantity` вместе с `{cs}[Required]` позволяет различить ситуации:

|Входные данные|Значение свойства|Проверка|
|---|---|---|
|Поле отсутствует или содержит `null`|`null`|Ошибка `[Required]`|
|Передан `0`|`0`|Ошибка `[Range]`|
|Передан `10`|`10`|Проверки успешны|

Так можно отдельно сообщить об отсутствующем поле и о недопустимом числе. 

#### Nullable reference types

При включённом nullable-контексте MVC по умолчанию рассматривает обычные non-nullable ссылочные параметры и свойства как имеющие `{cs}[Required(AllowEmptyStrings = true)]`.

Поэтому `{cs}string Name` может стать обязательным без явно указанного атрибута, а `{cs}string? Name` допускает `{cs}null`, если нет другого ограничения. Это не полностью эквивалентно явному `{cs}[Required]`, который по умолчанию запрещает также пустые и пробельные строки. 

Неявное правило можно отключить:

```cs
builder.Services.AddControllers(options =>
{
    options.SuppressImplicitRequiredAttributeForNonNullableReferenceTypes = true;
});
```

Явно указанные атрибуты `{cs}[Required]` продолжат работать.

### 7.3. Что содержит `ModelState`

> [!info] Определение  
> **`ModelState`** — словарь состояния привязки и валидации входных данных текущего запроса. Его записи связывают ключи полей с ошибками, состоянием проверки и, когда binding сохраняет их, исходными значениями. 

Свойство объявлено в `{cs}ControllerBase`:

```cs
public ModelStateDictionary ModelState { get; }
```

Основные элементы:

|Элемент|Назначение|
|---|---|
|`ModelState.IsValid`|Нет записей с ошибками или незавершённой валидацией|
|`ModelState.ErrorCount`|Количество сохранённых ошибок|
|`ModelState[key]`|Запись для указанного ключа|
|`entry.Errors`|Ошибки конкретной записи|
|`entry.RawValue` / `entry.AttemptedValue`|Исходное значение и его строковое представление, если они сохранены|
|`entry.ValidationState`|Состояние проверки записи|

Ключ может обозначать отдельное свойство, например `Quantity`, или вложенный путь, например `Address.City`. Для ошибок чтения JSON также встречаются пути вида `$.quantity`.

`{cs}ModelState` не является самим DTO и не представляет полную копию тела запроса. Изменение свойства DTO не пересчитывает автоматически сохранённые результаты проверки. 

### 7.4. Автоматический и ручной возврат ошибок

#### Автоматический ответ с `[ApiController]`

```cs
[ApiController]
[Route("products")]
public class ProductsController : ControllerBase
{
    [HttpPost]
    public IActionResult Create([FromBody] CreateProductRequest request)
    {
        return Ok(request);
    }
}
```

Если передать:

```json
{
  "name": "",
  "quantity": 0
}
```

MVC обнаружит ошибки валидации. При стандартном поведении `{cs}[ApiController]` будет возвращён `{http}400 Bad Request`, а метод `{cs}Create` не выполнится.

Ответ содержит `{cs}ValidationProblemDetails`. Основная часть тела:

```cs
{
  "title": "One or more validation errors occurred.",
  "status": 400,
  "errors": {
    "Name": [
      "Название обязательно"
    ],
    "Quantity": [
      "Количество должно быть от 1 до 1000"
    ]
  }
}
```

В полном ответе могут присутствовать также `{cs}type`, `{cs}traceId` и другие поля. Имена ключей зависят от настроек метаданных валидации. 

#### Ручная проверка

Если `{cs}[ApiController]` отсутствует или автоматический ответ отключён через `{cs}SuppressModelStateInvalidFilter`, результат проверяется в action:

```cs
[HttpPost]
public IActionResult Create([FromBody] CreateProductRequest request)
{
    if (!ModelState.IsValid)
        return ValidationProblem();

    return Ok(request);
}
```

Отключение автоматического ответа не отключает binding и валидацию: меняется обработка их результата. 

#### `ValidationProblem`

Основные перегрузки метода `{cs}ControllerBase`:

```cs
public virtual ActionResult ValidationProblem();

public virtual ActionResult ValidationProblem(
    ModelStateDictionary modelStateDictionary);

public virtual ActionResult ValidationProblem(
    ValidationProblemDetails descriptor);
```

Они используют соответственно текущий `{cs}ModelState`, явно переданный словарь или готовый объект описания ошибок. Возвращаемый `{cs}ActionResult` представляет HTTP-ответ; вызов метода не запускает проверку модели. 

Для настройки описания и статуса доступна перегрузка с параметрами `{cs}detail`, `{cs}instance`, `{cs}statusCode`, `{cs}title`, `{cs}type` и `{cs}modelStateDictionary`:

```cs
return ValidationProblem(
    title: "Некорректные данные товара",
    detail: "Исправьте указанные поля",
    modelStateDictionary: ModelState);
```

По умолчанию используется статус `{cs}400`. В отличие от `{cs}BadRequest(ModelState)`, метод формирует ответ в формате `{cs}ValidationProblemDetails`, согласованном со стандартным автоматическим ответом. 

#### Добавление ошибки вручную

Для текстовой ошибки используется метод `{cs}ModelStateDictionary`:

```cs
public void AddModelError(string key, string errorMessage);
```

Например, после проверки доступного количества товара:

```cs
ModelState.AddModelError(
    nameof(CreateProductRequest.Quantity),
    "Недостаточно товара на складе");

return ValidationProblem();
```

Ключ связывает ошибку с конкретным полем. Для ошибки модели в целом можно передать `{cs}string.Empty`. 

> [!note] Ошибка внутри action  
> Добавление ошибки в `{cs}ModelState` не завершает action автоматически. Проверка, обеспечивающая автоматический `400`, уже прошла до его вызова, поэтому из метода нужно явно вернуть результат.

### 7.5. Проверка нескольких свойств

Для условия, связывающего несколько полей DTO, можно реализовать `{cs}IValidatableObject`.

Его метод:

```cs
IEnumerable<ValidationResult> Validate(ValidationContext validationContext);
```

Это метод интерфейса, возвращающий последовательность найденных ошибок. 

```cs
using System.ComponentModel.DataAnnotations;

public class PeriodRequest : IValidatableObject
{
    public DateOnly From { get; set; }
    public DateOnly To { get; set; }

    public IEnumerable<ValidationResult> Validate(
        ValidationContext validationContext)
    {
        if (To < From)
        {
            yield return new ValidationResult(
                "Дата окончания не может быть раньше даты начала",
                new[] { nameof(To) });
        }
    }
}
```

При MVC-валидации DTO эта проверка вызывается автоматически, а ошибка связывается с полем `{cs}To`. Такой подход подходит для условий, которые можно проверить по содержимому самого объекта. 

### 7.6. Повторная валидация

Если модель создана или изменена внутри action, для её проверки используются методы `{cs}ControllerBase`:

```cs
public virtual bool TryValidateModel(object model);

public virtual bool TryValidateModel(object model, string? prefix);
```

Методы выполняют валидацию, сохраняют результаты в `{cs}ModelState` и возвращают его `{cs}IsValid`. Параметр `{cs}prefix` задаёт префикс ключей проверяемой модели. 

Перед повторной проверкой уже проверенной модели сбрасывается её состояние:

```cs
public void ClearValidationState(string key);
```

Пример для модели, чьи записи находятся под префиксом `request`:

```cs
ModelState.ClearValidationState("request");

if (!TryValidateModel(request, "request"))
    return ValidationProblem();
```

Префикс должен соответствовать существующим ключам. `{cs}ClearValidationState` очищает ошибки подходящих записей и переводит их в состояние `{cs}Unvalidated`; пустой ключ охватывает весь словарь. Сам DTO этот метод не изменяет. 

### 7.7. Входные ограничения и бизнес-правила

Валидация DTO проверяет ограничения входных данных: наличие названия, диапазон количества, согласованность дат.

Проверки, зависящие от состояния системы, выполняются в прикладной или доменной логике: наличие товара на складе, уникальность имени, допустимость изменения уже оплаченного заказа.

`{cs}ModelState.IsValid == true` означает успешную привязку и прохождение настроенной валидации. Это не гарантирует, что запрошенную операцию можно выполнить.

Атрибуты Data Annotations и `{cs}IValidatableObject.Validate` выполняют синхронную проверку. Проверки с обращением к БД или внешнему сервису обычно выполняются отдельно; их результат при необходимости можно преобразовать в ошибку поля через `{cs}ModelState.AddModelError`.

---

# 8. Возвращаемые значения actions

Возвращаемое значение action определяет, какие данные или какой результат MVC должен отправить клиенту. Если метод асинхронный, MVC сначала ожидает его завершения, затем обрабатывает полученное значение.

Основные варианты:

|Тип возвращаемого значения|Назначение|
|---|---|
|`T`|Возврат данных конкретного типа|
|`IActionResult`|Возврат разных HTTP-результатов без указания типа тела|
|`ActionResult<T>`|Возврат данных типа `T` или другого HTTP-результата|
|`Task<T>`|Асинхронный возврат данных|
|`Task<IActionResult>`|Асинхронный возврат HTTP-результата|
|`Task<ActionResult<T>>`|Асинхронный возврат данных или HTTP-результата|

MVC поддерживает также `{cs}IResult` и HttpResults, используемые в Minimal API, но их обработка отличается от MVC-результатов. 

В примерах используется DTO:

```cs
public record ProductDto(int Id, string Name, int Quantity);
```

Actions предполагают контроллер с базовым маршрутом `/products`. Поле `{cs}_service` обозначает прикладной сервис для получения и создания товаров.

### 8.1. Возврат обычного значения

Action может возвращать непосредственно DTO, коллекцию или примитивное значение:

```cs
[HttpGet("example")]
public ProductDto GetExample()
{
    return new ProductDto(42, "Keyboard", 10);
}
```

MVC оборачивает обычное значение в `{cs}ObjectResult` и использует output formatter для формирования тела ответа. Для такого DTO при стандартной конфигурации будет возвращён `{http}200 OK` с JSON:

```json
{
  "id": 42,
  "name": "Keyboard",
  "quantity": 10
}
```

Этот вариант подходит, когда метод возвращает данные одного типа. Из метода с возвращаемым типом `{cs}ProductDto` нельзя непосредственно вернуть `{cs}NotFound()` или `{cs}BadRequest()`. 

> [!warning] Возврат `null`  
> При стандартной конфигурации MVC значение `{cs}null` в объектном результате обычно превращается в `{http}204 No Content`. Оно не означает `{http}404 Not Found`; даже `{cs}Ok(null)` может дать `204`. Отсутствие ресурса следует выражать явно через `{cs}NotFound()`. 

### 8.2. `IActionResult`

> [!info] Определение  
> **`IActionResult`** — интерфейс результата action, который MVC выполняет для формирования HTTP-ответа. Конкретный результат определяет статус, заголовки и способ записи тела ответа. 

Контракт интерфейса:

```cs
public interface IActionResult
{
    Task ExecuteResultAsync(ActionContext context);
}
```

Метод вызывается инфраструктурой MVC после получения результата action. Параметр `{cs}context` предоставляет контекст выполнения, а возвращаемый `{cs}Task` представляет завершение записи результата.

Большинство стандартных MVC-результатов наследуются от абстрактного класса `{cs}ActionResult`, который реализует `{cs}IActionResult`. Например: `{cs}OkObjectResult`, `{cs}NotFoundResult`, `{cs}NoContentResult`.

```cs
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    var product = _service.Find(id);

    if (product is null)
        return NotFound();

    return Ok(product);
}
```

Здесь возможны два результата:

- `{cs}NotFound()` — `404`
- `{cs}Ok(product)` — `200` с данными товара

Методы `{cs}ControllerBase` создают объекты результатов. Например, `{cs}Ok(product)` создаёт `{cs}OkObjectResult`; сам вызов ещё не записывает ответ клиенту. 

Тип `{cs}IActionResult` не сообщает, какой объект находится в теле успешного ответа.

### 8.3. `ActionResult<T>`

`{cs}ActionResult<T>` позволяет вернуть **значение типа `{cs}T` или объект `{cs}ActionResult`**:

```cs
[HttpGet("{id:int}")]
public ActionResult<ProductDto> GetById(int id)
{
    var product = _service.Find(id);

    if (product is null)
        return NotFound();

    return product;
}
```

Неявные преобразования обеспечивают оба варианта:

```cs
public static implicit operator ActionResult<TValue>(TValue value);

public static implicit operator ActionResult<TValue>(ActionResult result);
```

При возврате DTO MVC создаёт `{cs}ObjectResult` с данными и обычным статусом `200`. При возврате `{cs}NotFound()` выполняется переданный результат со статусом `404`. 

Сам `{cs}ActionResult<T>` не наследуется от `{cs}ActionResult` и не реализует `{cs}IActionResult`: MVC преобразует эту обёртку в исполняемый результат.

Тип `{cs}T` также позволяет инфраструктуре описания API определить ожидаемый тип тела ответа.

> [!note] Тип тела не проверяется для каждого результата  
> Сигнатура `{cs}ActionResult<ProductDto>` допускает `{cs}return Ok("other value");`, поскольку `{cs}OkObjectResult` преобразуется в обёртку независимо от типа его содержимого. Поэтому `{cs}T` описывает ожидаемые данные, но не гарантирует тип тела во всех ветках метода. 

При `{cs}ActionResult<IEnumerable<ProductDto>>` непосредственный возврат выражения со статическим типом `{cs}IEnumerable<ProductDto>` имеет ограничение C# на неявные преобразования с интерфейсами. Можно вернуть `{cs}Ok(products)` либо использовать конкретную коллекцию, например `{cs}List<ProductDto>`. 

### 8.4. Асинхронные actions

Асинхронный метод использует ту же модель результата, обёрнутую в `{cs}Task`:

```cs
[HttpGet("{id:int}", Name = "GetProduct")]
public async Task<ActionResult<ProductDto>> GetById(
    int id,
    CancellationToken cancellationToken)
{
    var product = await _service.GetAsync(id, cancellationToken);

    if (product is null)
        return NotFound();

    return product;
}
```

MVC ожидает `{cs}Task`, после чего обрабатывает полученный `{cs}ActionResult<ProductDto>`. Сам `{cs}Task` в тело ответа не сериализуется. 

Асинхронность меняет способ ожидания операции, а HTTP-статус и тело по-прежнему определяются возвращёнными данными или результатом.

### 8.5. Основные методы формирования ответа

Это обычные методы `{cs}ControllerBase`, а не extension methods.

#### Успешный ответ

```cs
public virtual OkResult Ok();

public virtual OkObjectResult Ok(object? value);

public virtual NoContentResult NoContent();
```

|Вызов|Результат|
|---|---|
|`Ok()`|`200` без тела|
|`Ok(value)`|`200` с форматируемым значением|
|`NoContent()`|`204` без тела|

`{cs}value` — объект для тела ответа. Конкретный формат его представления определяется при выполнении результата. 

#### Ошибки запроса и отсутствие ресурса

```cs
public virtual NotFoundResult NotFound();

public virtual NotFoundObjectResult NotFound(object? value);

public virtual BadRequestResult BadRequest();

public virtual BadRequestObjectResult BadRequest(object? error);

public virtual BadRequestObjectResult BadRequest(
    ModelStateDictionary modelState);
```

`{cs}NotFound` задаёт статус `404`, а `{cs}BadRequest` — `400`. Перегрузки с объектом позволяют передать содержимое ответа; перегрузка с `{cs}ModelStateDictionary` формирует объект с ошибками полей. 

Под `{cs}[ApiController]` стандартные результаты ошибок без явно заданного тела могут быть преобразованы в ответ с `{cs}ProblemDetails`. Поэтому `{cs}NotFound()` не обязательно означает пустое тело.

Для ошибок валидации используется рассмотренный в пункте 7 `{cs}ValidationProblem()`, который формирует `{cs}ValidationProblemDetails`.

#### Произвольный статус

```cs
public virtual StatusCodeResult StatusCode(int statusCode);

public virtual ObjectResult StatusCode(
    int statusCode,
    object? value);
```

```cs
return StatusCode(
    StatusCodes.Status503ServiceUnavailable,
    new { message = "Сервис временно недоступен" });
```

Первый параметр задаёт статус ответа, второй — его содержимое. 

### 8.6. Создание ресурса: `Created`, `CreatedAtAction`, `CreatedAtRoute`

Эти методы формируют результат со статусом `{http}201 Created`. Перегрузки с адресом или маршрутом дополнительно устанавливают заголовок `Location`.

#### `Created`: готовый адрес

```cs
public virtual CreatedResult Created();

public virtual CreatedResult Created(string uri, object? value);

public virtual CreatedResult Created(Uri uri, object? value);
```

```cs
return Created($"/products/{product.Id}", product);
```

`{cs}uri` задаёт адрес созданного ресурса, а `{cs}value` — тело ответа. Параметрическая перегрузка `{cs}Created()` возвращает `201` без передачи адреса и данных. 

#### `CreatedAtAction`: адрес по action

```cs
public virtual CreatedAtActionResult CreatedAtAction(
    string? actionName,
    object? value);

public virtual CreatedAtActionResult CreatedAtAction(
    string? actionName,
    object? routeValues,
    object? value);

public virtual CreatedAtActionResult CreatedAtAction(
    string? actionName,
    string? controllerName,
    object? routeValues,
    object? value);
```

Параметры:

- `{cs}actionName` — имя action для генерации URL
- `{cs}controllerName` — имя контроллера; без него используется текущий контроллер
- `{cs}routeValues` — значения для построения маршрута
- `{cs}value` — тело ответа

Пример создания товара с адресом action `{cs}GetById`:

```cs
[HttpPost]
public async Task<ActionResult<ProductDto>> Create(
    [FromBody] CreateProductRequest request,
    CancellationToken cancellationToken)
{
    var product = await _service.CreateAsync(
        request,
        cancellationToken);

    return CreatedAtAction(
        nameof(GetById),
        new { id = product.Id },
        product);
}
```

При создании товара с идентификатором `42` заголовок будет содержать адрес вида `https://example.com/products/42`. Сам `{cs}GetById` при этом не вызывается: он используется как адрес для генерации ссылки. 

> [!warning] Два аргумента — имя и тело  
> В `{cs}CreatedAtAction(nameof(GetById), new { id = 42 })` второй аргумент является телом ответа, а не `{cs}routeValues`. Для передачи идентификатора маршруту используется перегрузка с тремя аргументами. 

#### `CreatedAtRoute`: адрес по имени маршрута

```cs
public virtual CreatedAtRouteResult CreatedAtRoute(
    string? routeName,
    object? value);

public virtual CreatedAtRouteResult CreatedAtRoute(
    object? routeValues,
    object? value);

public virtual CreatedAtRouteResult CreatedAtRoute(
    string? routeName,
    object? routeValues,
    object? value);
```

Для маршрута с `{cs}Name = "GetProduct"` из примера выше:

```cs
return CreatedAtRoute(
    "GetProduct",
    new { id = product.Id },
    product);
```

Здесь `{cs}routeName` — **имя маршрута**, а не имя C#-метода. Перегрузка без имени выбирает подходящий маршрут по переданным значениям. 

Если URL для `{cs}CreatedAtAction` или `{cs}CreatedAtRoute` невозможно построить, выполнение результата завершится ошибкой. Поэтому имена и значения должны соответствовать существующему маршруту. 

### 8.7. `Problem`: описание ошибки

Основная перегрузка `{cs}ControllerBase.Problem`:

```cs
public virtual ObjectResult Problem(
    string? detail = null,
    string? instance = null,
    int? statusCode = null,
    string? title = null,
    string? type = null,
    IDictionary<string, object?>? extensions = null);
```

|Параметр|Назначение|
|---|---|
|`statusCode`|HTTP-статус ошибки|
|`title`|Краткое название проблемы|
|`detail`|Описание конкретной ошибки|
|`type`|URI, идентифицирующий тип проблемы|
|`instance`|URI, идентифицирующий конкретный случай|
|`extensions`|Дополнительные поля|

Метод создаёт `{cs}ObjectResult` с `{cs}ProblemDetails`. Если статус не передан, по умолчанию используется `500`. 

```cs
return Problem(
    statusCode: StatusCodes.Status409Conflict,
    title: "Изменение заказа невозможно",
    detail: "Заказ уже оплачен");
```

`{cs}Problem()` описывает ошибку в целом. `{cs}ValidationProblem()` дополнительно содержит словарь ошибок входных полей.

### 8.8. Отличие от результатов Minimal API

Контроллеры могут возвращать `{cs}IResult`:

```cs
[HttpGet("status")]
public IResult GetStatus()
{
    return Results.Ok(new { status = "ok" });
}
```

Однако `{cs}Results.Ok(...)` и `{cs}ControllerBase.Ok(...)` создают результаты разных инфраструктур:

|MVC-результаты|HttpResults|
|---|---|
|Реализуют `IActionResult`|Реализуют `IResult`|
|Выполняются через `ExecuteResultAsync(ActionContext)`|Выполняются через `ExecuteAsync(HttpContext)`|
|Объектные результаты используют MVC output formatters|Используют собственный способ записи ответа|
|Поддерживают MVC content negotiation|Не используют MVC content negotiation|

Поэтому возврат HttpResults из контроллера допустим, но настройки MVC formatters не определяют формат такого ответа. 

---

# 9. Формат ответа и метаданные API

### 9.1. `Accept` и `Content-Type`

Тип возвращаемого значения action и формат HTTP-тела — разные характеристики. Один DTO может быть представлен в JSON или XML, если соответствующий formatter поддерживает этот тип.

|Заголовок|Назначение|
|---|---|
|`Content-Type` запроса|Формат отправленного клиентом тела|
|`Accept` запроса|Форматы ответа, допустимые для клиента|
|`Content-Type` ответа|Фактический формат тела ответа|

Например:

```http
POST /products HTTP/1.1
Host: example.com
Content-Type: application/json
Accept: application/xml

{
  "name": "Keyboard",
  "quantity": 10
}
```

Клиент отправляет JSON и запрашивает XML в ответ. Форматы входного и выходного тела выбираются независимо. Заголовок `Accept` не определяет способ чтения тела запроса. 

MVC использует:

- **Input formatters** — для чтения тела при привязке через `{cs}[FromBody]`
- **Output formatters** — для записи значений из `{cs}ObjectResult` и его наследников, например `{cs}OkObjectResult`

При стандартной конфигурации для DTO используется JSON через `{cs}System.Text.Json`. 

### 9.2. Content negotiation

> [!info] Определение  
> **Content negotiation** — выбор представления ответа на основе форматов, указанных клиентом в `Accept`, доступных output formatters и ограничений конкретного результата. 

Для объектного результата MVC ищет formatter, который может сериализовать возвращаемое значение в подходящий формат. При нескольких вариантах учитываются предпочтения клиента, в том числе веса `q`:

```http
​
Accept: application/xml;q=1.0, application/json;q=0.8
```

Здесь XML предпочтительнее JSON. Но сервер должен иметь formatter, способный обработать возвращаемый тип. 

Если подходящий формат не найден, поведение зависит от `{cs}MvcOptions.ReturnHttpNotAcceptable`:

|Настройка|Поведение|
|---|---|
|`false`, по умолчанию|MVC пробует выбрать formatter без учёта `Accept`|
|`true`|MVC возвращает `406 Not Acceptable`|

Поэтому `Accept: application/xml` сам по себе не гарантирует XML или ошибку: при стандартной конфигурации сервер может вернуть JSON. 

Строгая обработка предпочтений клиента:

```cs
builder.Services.AddControllers(options =>
{
    options.ReturnHttpNotAcceptable = true;
    options.RespectBrowserAcceptHeader = true;
});
```

`{cs}RespectBrowserAcceptHeader` позволяет учитывать `Accept` с wildcard `*/*`, который MVC по умолчанию игнорирует. Это часто встречается в заголовках браузера. 

#### Поддержка XML

Extension methods класса `{cs}MvcXmlMvcBuilderExtensions`:

```cs
public static IMvcBuilder AddXmlSerializerFormatters(
    this IMvcBuilder builder);

public static IMvcBuilder AddXmlSerializerFormatters(
    this IMvcBuilder builder,
    Action<MvcXmlOptions> setupAction);
```

Они добавляют input и output formatters на основе `{cs}XmlSerializer`. Параметр `{cs}setupAction` позволяет настроить `{cs}MvcXmlOptions`; возвращаемый `{cs}IMvcBuilder` используется для дальнейшей конфигурации MVC.

```cs
builder.Services.AddControllers()
    .AddXmlSerializerFormatters();
```

После регистрации XML может использоваться для входного тела и ответа, если DTO поддерживается сериализатором и формат не запрещён атрибутами. 

### 9.3. Результаты с фиксированным форматом

Некоторые результаты самостоятельно определяют формат и не используют обычный выбор MVC output formatter по `Accept`.

Например, явный JSON:

```cs
[HttpGet("json")]
public IActionResult GetJson()
{
    return new JsonResult(new { status = "ok" });
}
```

И явный текст:

```cs
[HttpGet("text")]
public IActionResult GetText()
{
    return Content("ok", "text/plain");
}
```

`{cs}JsonResult` формирует JSON, а `{cs}ContentResult` отправляет указанную строку с заданным content type. Заголовок `Accept` не переключает эти результаты на XML.

Возвращённая обычным значением строка также по умолчанию обрабатывается `{cs}StringOutputFormatter` как текст, поэтому `{cs}return "ok";` не обязательно означает JSON-строку `"ok"`. 

### 9.4. `[Produces]`: формат ответа

Атрибут `{cs}[Produces]` ограничивает форматы **объектных результатов** и одновременно предоставляет метаданные форматов ответа.

```cs
[HttpGet("{id:int}")]
[Produces("application/json")]
public ActionResult<ProductDto> GetById(int id)
{
    var product = _service.Find(id);

    if (product is null)
        return NotFound();

    return product;
}
```

Для возвращаемого DTO разрешён JSON, даже если в приложении зарегистрирован XML formatter.

Можно разрешить несколько форматов:

```cs
[Produces("application/json", "application/xml")]
```

Атрибут применяется к action или контроллеру. Он задаёт ограничения для `{cs}ObjectResult`; результаты вроде `{cs}ContentResult`, `{cs}FileResult` или `{cs}IResult` используют собственный способ формирования ответа. 

Если клиент принимает только XML, а action разрешает только JSON:

- При `{cs}ReturnHttpNotAcceptable == false` MVC может вернуть JSON
- При `{cs}ReturnHttpNotAcceptable == true` MVC возвращает `406`

`{cs}[Produces("application/xml")]` не добавляет XML formatter. Для формирования ответа нужны и разрешённый формат, и его реализация. 

### 9.5. `[Consumes]`: формат входного тела

Атрибут `{cs}[Consumes]` ограничивает допустимые content types запроса.

```cs
[HttpPost]
[Consumes("application/json")]
public IActionResult Create([FromBody] CreateProductRequest request)
{
    return Ok(request);
}
```

Если запрос указывает неподдерживаемый этим action `Content-Type`, например `application/xml`, будет возвращён `{http}415 Unsupported Media Type`.

Несколько допустимых форматов задаются так:

```cs
[Consumes("application/json", "application/xml")]
```

Атрибут также участвует в выборе action. Поэтому один путь и HTTP-метод могут обрабатываться разными actions в зависимости от `Content-Type`:

```cs
[HttpPost("import")]
[Consumes("application/json")]
public IActionResult ImportJson([FromBody] CreateProductRequest request)
{
    return Ok(request);
}

[HttpPost("import")]
[Consumes("application/x-www-form-urlencoded")]
public IActionResult ImportForm([FromForm] CreateProductRequest request)
{
    return Ok(request);
}
```

Запрос JSON выбирает `{cs}ImportJson`, а запрос с полями формы — `{cs}ImportForm`. 

`{cs}[Consumes]` не добавляет parser или input formatter. Например, разрешение `application/xml` не обеспечивает чтение XML без зарегистрированного XML formatter. 

### 9.6. `[ProducesResponseType]`: описание возможных ответов

> [!info] Определение  
> **Метаданные API** — сведения об операции, её входных данных и возможных ответах, которые инфраструктура описания API использует для генерации документации, схем OpenAPI и клиентского кода.

`{cs}[ProducesResponseType]` описывает статус, тип тела и при необходимости content type конкретного ответа.

```cs
[HttpGet("{id:int}")]
[ProducesResponseType(typeof(ProductDto), StatusCodes.Status200OK)]
[ProducesResponseType(typeof(ProblemDetails), StatusCodes.Status404NotFound)]
public ActionResult<ProductDto> GetById(int id)
{
    var product = _service.Find(id);

    if (product is null)
        return NotFound();

    return product;
}
```

Метаданные сообщают, что операция может вернуть:

|Статус|Тип тела|
|---|---|
|`200`|`ProductDto`|
|`404`|`ProblemDetails`|

Для ответа без тела достаточно статуса:

```cs
[ProducesResponseType(StatusCodes.Status204NoContent)]
```

Тип и content type можно указать вместе:

```cs
[ProducesResponseType(
    typeof(ProductDto),
    StatusCodes.Status200OK,
    "application/json")]
```

Также доступна generic-форма:

```cs
[ProducesResponseType<ProductDto>(StatusCodes.Status200OK)]
```

При `{cs}ActionResult<ProductDto>` тип успешного ответа может быть выведен из `{cs}T`, поэтому допустима запись `{cs}[ProducesResponseType(StatusCodes.Status200OK)]`. 

> [!warning] Описание не проверяет результат  
> `{cs}[ProducesResponseType]` не устанавливает статус, не выбирает formatter и не проверяет фактический тип тела. Action может вернуть незаявленный ответ; тогда описание API будет расходиться с поведением. 

Таким образом, у атрибутов разные роли:

|Атрибут|Влияние на выполнение|
|---|---|
|`[Produces]`|Ограничивает формат объектного ответа|
|`[Consumes]`|Ограничивает формат запроса и участвует в выборе action|
|`[ProducesResponseType]`|Описывает возможный ответ|

### 9.7. Настройка JSON

Для JSON formatters MVC используется `{cs}Microsoft.AspNetCore.Mvc.JsonOptions`.

Extension method класса `{cs}MvcCoreMvcBuilderExtensions`:

```cs
public static IMvcBuilder AddJsonOptions(
    this IMvcBuilder builder,
    Action<Microsoft.AspNetCore.Mvc.JsonOptions> configure);
```

Параметр `{cs}configure` настраивает JSON, а метод возвращает тот же `{cs}IMvcBuilder` для продолжения конфигурации. Настройки применяются к чтению и записи JSON в MVC. 

По умолчанию используются web-настройки `{cs}System.Text.Json`, включая camelCase для имён свойств и сравнение входных имён без учёта регистра. 

Пример настройки:

```cs
using System.Text.Json.Serialization;

builder.Services.AddControllers()
    .AddJsonOptions(options =>
    {
        var json = options.JsonSerializerOptions;

        json.PropertyNamingPolicy = null;
        json.DefaultIgnoreCondition = JsonIgnoreCondition.WhenWritingNull;
        json.Converters.Add(new JsonStringEnumConverter());
    });
```

|Настройка|Эффект|
|---|---|
|`PropertyNamingPolicy = null`|Имена свойств сохраняются без преобразования: `Id`, `Name`|
|`WhenWritingNull`|Свойства со значением `null` пропускаются при сериализации|
|`JsonStringEnumConverter`|Enum записываются строковыми именами|

Для отдельного свойства можно задать имя через `{cs}[JsonPropertyName]`:

```cs
public class ProductResponse
{
    public int Id { get; set; }

    [JsonPropertyName("product_name")]
    public string Name { get; set; } = string.Empty;
}
```

Имя `product_name` применяется при сериализации и десериализации и имеет приоритет над общей naming policy. 

Настройки `{cs}AddJsonOptions` относятся к MVC. JSON для Minimal API и HttpResults настраивается отдельно через `{cs}ConfigureHttpJsonOptions`; совпадение сериализатора не означает использование одного объекта настроек.

---

# 10. Фильтры MVC

> [!info] Определение  
> **Фильтры MVC** — компоненты, выполняющие код на определённых этапах обработки выбранного action: до привязки параметров, вокруг вызова метода, при обработке исключений или вокруг выполнения результата. Они позволяют вынести общую логику из отдельных actions. 

### 10.1. Место фильтров в pipeline

Фильтры выполняются **внутри MVC**, после выбора endpoint и action.

|Middleware|Фильтры MVC|
|---|---|
|Работает в HTTP pipeline приложения|Работают в pipeline вызова action|
|Основной контекст — `HttpContext`|Доступны также аргументы action, `ModelState` и результат|
|Может обрабатывать запросы к разным видам endpoints|Применяются к MVC actions|
|Положение задаётся порядком регистрации middleware|Положение зависит от вида фильтра, области применения и `Order`|

При обычном выполнении сначала проходят authorization filters, затем resource filters охватывают привязку параметров, вызов action и выполнение результата. Action filters окружают вызов метода, а result filters — выполнение возвращённого результата. 

**Возврат из action ещё не означает завершение ответа**: после него MVC должен выполнить результат, например сериализовать DTO и записать JSON.

### 10.2. Виды фильтров

Интерфейсы находятся в пространстве имён `{cs}Microsoft.AspNetCore.Mvc.Filters`.

|Вид|Синхронный интерфейс|Асинхронный интерфейс|Этап|
|---|---|---|---|
|Authorization|`IAuthorizationFilter`|`IAsyncAuthorizationFilter`|Проверка доступа перед остальными этапами|
|Resource|`IResourceFilter`|`IAsyncResourceFilter`|Вокруг binding, action и результата|
|Action|`IActionFilter`|`IAsyncActionFilter`|Вокруг вызова action, после binding и валидации|
|Exception|`IExceptionFilter`|`IAsyncExceptionFilter`|Обработка необработанных исключений внутри охватываемой части MVC|
|Result|`IResultFilter`|`IAsyncResultFilter`|Вокруг выполнения результата|

Выбор вида определяет, какие данные доступны и какую работу можно предотвратить. Например, resource filter может вернуть закэшированный ответ **до binding**, а action filter получает уже подготовленные аргументы метода. 

Authorization filters относятся к механизму проверки доступа. Для обычных правил авторизации используются `{cs}[Authorize]` и authorization policies.

### 10.3. Action filters

#### Синхронный контракт

```cs
public interface IActionFilter : IFilterMetadata
{
    void OnActionExecuting(ActionExecutingContext context);

    void OnActionExecuted(ActionExecutedContext context);
}
```

`{cs}OnActionExecuting` вызывается перед action, а `{cs}OnActionExecuted` — после выполнения охватываемой цепочки action filters и метода. 

Основные данные контекста:

|Элемент|Назначение|
|---|---|
|`HttpContext`|Текущий HTTP-запрос и ответ|
|`ActionDescriptor`|Описание выбранного action|
|`ActionArguments`|Подготовленные аргументы метода|
|`ModelState`|Результаты binding и валидации|
|`Result`|Результат, который должен выполнить MVC|

Через `{cs}ActionArguments` можно изменить аргументы до вызова метода. Через `{cs}Result` — задать ответ вместо вызова action. 

#### Асинхронный контракт

```cs
public interface IAsyncActionFilter : IFilterMetadata
{
    Task OnActionExecutionAsync(
        ActionExecutingContext context,
        ActionExecutionDelegate next);
}
```

Продолжение имеет сигнатуру:

```
public delegate Task<ActionExecutedContext> ActionExecutionDelegate();
```

Вызов `{cs}await next()` выполняет оставшиеся action filters и сам action. Возвращаемый `{cs}ActionExecutedContext` содержит результат выполнения, включая сведения об исключении или отмене вызова. 

Пример измерения времени:

```cs
using System.Diagnostics;
using Microsoft.AspNetCore.Mvc.Filters;

public sealed class ActionTimingFilter : IAsyncActionFilter
{
    private readonly ILogger<ActionTimingFilter> _logger;

    public ActionTimingFilter(ILogger<ActionTimingFilter> logger)
    {
        _logger = logger;
    }

    public async Task OnActionExecutionAsync(
        ActionExecutingContext context,
        ActionExecutionDelegate next)
    {
        var started = Stopwatch.GetTimestamp();

        await next();

        _logger.LogInformation(
            "Action stage {Action} took {ElapsedMs} ms",
            context.ActionDescriptor.DisplayName,
            Stopwatch.GetElapsedTime(started).TotalMilliseconds);
    }
}
```

Этот фильтр измеряет время внутренней цепочки action filters и action. Сериализация тела ответа выполняется позднее и в измерение не входит.

Для одного этапа используется синхронная или асинхронная реализация. Если класс реализует обе версии интерфейса, MVC выбирает асинхронную. 

### 10.4. Short-circuit

Фильтр может завершить охватываемую часть pipeline, предоставив готовый результат.

В action filter для этого устанавливается `{cs}ActionExecutingContext.Result`. Например, при обнаружении отсутствующего обязательного заголовка:

```cs
context.Result = new BadRequestObjectResult(new
{
    message = "Отсутствует X-Request-Id"
});
```

В синхронном фильтре MVC после `{cs}OnActionExecuting` обнаружит результат и пропустит оставшиеся action filters и action.

В асинхронном фильтре после установки результата нужно завершить метод **без вызова `{cs}next`**:

```cs
if (!context.HttpContext.Request.Headers.ContainsKey("X-Request-Id"))
{
    context.Result = new BadRequestObjectResult(new
    {
        message = "Отсутствует X-Request-Id"
    });

    return;
}

await next();
```

Полученный результат затем выполняется MVC. Short-circuit action filter не означает пропуск всей обработки ответа. 

У разных видов фильтров способы остановки различаются:

|Фильтр|Способ|
|---|---|
|Authorization|Установить `AuthorizationFilterContext.Result`|
|Resource|Установить `ResourceExecutingContext.Result`; в async-варианте не вызывать `next`|
|Action|Установить `ActionExecutingContext.Result`; в async-варианте не вызывать `next`|
|Result|Установить `ResultExecutingContext.Cancel = true`; в async-варианте не вызывать `next`|

Остановка resource filter предотвращает также binding и вызов action. Остановка result filter отменяет выполнение результата; готовый ответ в этом случае должен обеспечить сам фильтр. 

### 10.5. Регистрация и DI

Фильтр можно применить глобально, к контроллеру или к отдельному action.

#### Глобальная регистрация

Коллекция `{cs}MvcOptions.Filters` предоставляет методы:

```cs
public IFilterMetadata Add<TFilterType>()
    where TFilterType : IFilterMetadata;

public IFilterMetadata Add<TFilterType>(int order)
    where TFilterType : IFilterMetadata;

public IFilterMetadata Add(Type filterType);

public IFilterMetadata Add(Type filterType, int order);
```

```cs
builder.Services.AddControllers(options =>
{
    options.Filters.Add<ActionTimingFilter>();
});
```

При добавлении **типа** MVC создаёт экземпляр фильтра с разрешением зависимостей конструктора из DI. Регистрировать сам `{cs}ActionTimingFilter` как сервис для этого не требуется; его зависимости должны быть доступны.

Методы возвращают метаданные регистрации фильтра. Параметр `{cs}order` задаёт порядок выполнения; без него используется `0`. 

Для получения самого фильтра из DI используются другие методы:

```cs
public IFilterMetadata AddService<TFilterType>()
    where TFilterType : IFilterMetadata;

public IFilterMetadata AddService<TFilterType>(int order)
    where TFilterType : IFilterMetadata;

public IFilterMetadata AddService(Type filterType);

public IFilterMetadata AddService(Type filterType, int order);
```

```cs
builder.Services.AddScoped<ActionTimingFilter>();

builder.Services.AddControllers(options =>
{
    options.Filters.AddService<ActionTimingFilter>();
});
```

Здесь экземпляр разрешается из DI согласно регистрации и lifetime сервиса. 

#### `[ServiceFilter]`

Позволяет применить зарегистрированный сервис-фильтр к контроллеру или action:

```cs
builder.Services.AddScoped<ActionTimingFilter>();
```

```cs
[HttpGet]
[ServiceFilter(typeof(ActionTimingFilter))]
public IActionResult Get()
{
    return Ok(new { status = "ok" });
}
```

Эквивалентная generic-форма:

```cs
[ServiceFilter<ActionTimingFilter>]
```

Сам тип фильтра должен быть зарегистрирован в DI. 

#### `[TypeFilter]`

```cs
[HttpGet]
[TypeFilter(typeof(ActionTimingFilter))]
public IActionResult Get()
{
    return Ok(new { status = "ok" });
}
```

`{cs}TypeFilter` создаёт экземпляр указанного типа, получая зависимости конструктора из DI. Сам фильтр регистрировать не требуется. Свойство `{cs}Arguments` позволяет дополнительно передать аргументы конструктора, которые не являются сервисами. 

#### Экземпляры и повторное использование

В `{cs}Filters` можно передать готовый экземпляр через унаследованный метод коллекции `{cs}Add(IFilterMetadata)`:

```cs
options.Filters.Add(new SomeFilter());
```

Такой экземпляр разделяется между запросами и должен быть безопасен для конкурентного использования. Конструктор уже вызван вручную, поэтому MVC не выполняет его constructor injection. 

У `{cs}ServiceFilter` и `{cs}TypeFilter` свойство `{cs}IsReusable` сообщает, что созданный фильтр можно переиспользовать между запросами. Это подсказка инфраструктуре, а не гарантия единственного экземпляра. Для фильтров со scoped-зависимостями такое переиспользование не подходит. 

### 10.6. Порядок выполнения

Для фильтров **одного этапа** сначала учитывается `{cs}Order`, затем область применения.

Контракт:

```cs
public interface IOrderedFilter : IFilterMetadata
{
    int Order { get; }
}
```

Меньшее значение `{cs}Order` означает более раннее выполнение кода «до» и более позднее выполнение кода «после». При одинаковом порядке глобальные фильтры окружают фильтры контроллера, а те — фильтры action. 

Для трёх action filters с одинаковым `{cs}Order`:

|Шаг|Выполнение|
|---|---|
|1|Глобальный фильтр: до|
|2|Фильтр контроллера: до|
|3|Фильтр action: до|
|4|Action|
|5|Фильтр action: после|
|6|Фильтр контроллера: после|
|7|Глобальный фильтр: после|

`{cs}Order` не переносит фильтр на другой этап: action filter с отрицательным порядком всё равно выполняется после начала resource-этапа.

Порядок можно задать при регистрации или через атрибут:

```cs
options.Filters.Add<ActionTimingFilter>(order: -100);
```

```cs
[ServiceFilter(typeof(ActionTimingFilter), Order = -100)]
```

### 10.7. Result filters

Синхронный контракт:

```cs
public interface IResultFilter : IFilterMetadata
{
    void OnResultExecuting(ResultExecutingContext context);

    void OnResultExecuted(ResultExecutedContext context);
}
```

Асинхронный контракт:

```cs
public interface IAsyncResultFilter : IFilterMetadata
{
    Task OnResultExecutionAsync(
        ResultExecutingContext context,
        ResultExecutionDelegate next);
}
```

Эти фильтры окружают **выполнение результата**, включая форматирование и запись тела ответа. До выполнения можно заменить `{cs}context.Result` или добавить заголовки.

Пример собственного атрибута:

```cs
using Microsoft.AspNetCore.Mvc.Filters;

public sealed class ApiVersionHeaderAttribute : ResultFilterAttribute
{
    public override void OnResultExecuting(ResultExecutingContext context)
    {
        context.HttpContext.Response.Headers["X-Api-Version"] = "1";
    }
}
```

```cs
[HttpGet]
[ApiVersionHeader]
public IActionResult Get()
{
    return Ok(new { status = "ok" });
}
```

Заголовок устанавливается перед выполнением результата. В `{cs}OnResultExecuted` ответ уже может быть начат, поэтому менять его статус и заголовки поздно. 

Обычные result filters выполняются, когда action или action filters успешно предоставили результат. Они не выполняются для результатов, полученных при остановке authorization/resource filter или обработке исключения exception filter.

Для охвата таких результатов существуют `{cs}IAlwaysRunResultFilter` и `{cs}IAsyncAlwaysRunResultFilter`. Слово _Always_ относится к выполнению результатов MVC, а не ко всем ответам приложения или запросам, остановленным middleware. 

### 10.8. Exception filters

Контракты:

```cs
public interface IExceptionFilter : IFilterMetadata
{
    void OnException(ExceptionContext context);
}
```

```cs
public interface IAsyncExceptionFilter : IFilterMetadata
{
    Task OnExceptionAsync(ExceptionContext context);
}
```

Exception filters обрабатывают необработанные исключения при создании контроллера, binding, выполнении action filters и самого action.

Они не охватывают ошибки authorization/resource filters, result filters и выполнения результата. Например, ошибка сериализации JSON возникает за пределами их области обработки. 

Для обработки исключения можно назначить результат и отметить исключение как обработанное:

```cs
context.Result = new ObjectResult(new ProblemDetails
{
    Status = StatusCodes.Status500InternalServerError,
    Title = "Ошибка выполнения операции"
})
{
    StatusCode = StatusCodes.Status500InternalServerError
};

context.ExceptionHandled = true;
```

Если исключение осталось необработанным, оно распространяется наружу и может быть перехвачено middleware обработки ошибок.

Exception filter подходит для обработки, зависящей от выбранного action или контроллера. Middleware обработки исключений имеет более широкую область: он может охватывать ошибки разных endpoints и выполнения MVC-результата. 
