
---

## Оглавление

- [[#1. Назначение `WebApplication`|1. Назначение WebApplication]]
- [[#2. Реализуемые интерфейсы|2. Реализуемые интерфейсы]]
- [[#3. Роль `IHost`|3. Роль IHost]]
- [[#4. Роль `IApplicationBuilder`|4. Роль IApplicationBuilder]]
- [[#5. Роль `IEndpointRouteBuilder`|5. Роль IEndpointRouteBuilder]]
- [[#6. Основные свойства `WebApplication`|6. Основные свойства WebApplication]]
- [[#7. Настройка HTTP-приложения после `Build()`|7. Настройка HTTP-приложения после Build()]]
- [[#8. Запуск приложения|8. Запуск приложения]]

---

# 1. Назначение `WebApplication`

**`WebApplication`** — центральный объект уже построенного ASP.NET Core приложения, через который выполняется его дальнейшая конфигурация и запуск.

Создаётся вызовом:

```cs
var app = builder.Build();
```

`WebApplication` представляет уже построенное приложение и используется на следующем этапе его жизненного цикла.

Через `WebApplication` доступны несколько основных возможностей:

- управление жизненным циклом приложения
- построение middleware pipeline
- регистрация endpoints
- доступ к сервисам приложения
- доступ к configuration и environment
- запуск приложения

---

# 2. Реализуемые интерфейсы

`WebApplication` реализует интерфейсы:

- `IHost`
- `IApplicationBuilder`
- `IEndpointRouteBuilder`
- `IAsyncDisposable`

Реализация `IAsyncDisposable`, позволяет асинхронно освобождать связанные с приложением ресурсы при завершении работы.

`IHost`, в свою очередь, наследует `IDisposable`, поэтому `WebApplication` также может быть освобождён синхронно.

---

# 3. Роль `IHost`

Через интерфейс `IHost` `WebApplication` выступает как **запускаемый host приложения** и предоставляет базовые операции управления его жизненным циклом.

Контракт `IHost`:

- `Services`
- `StartAsync(...)`
- `StopAsync(...)`
- `Dispose()`

Extension-методы:

- `Start()`
- `Run()`
- `WaitForShutdown()`
- `RunAsync()`
- `WaitForShutdownAsync(...)`

## Основные возможности

```cs
// Доступ к построенному DI-контейнеру
app.Services;

// Запуск host
await app.StartAsync(...);

// Корректная остановка host
await app.StopAsync(...);

// Освобождение ресурсов
app.Dispose();
```

### `Services`

```cs
app.Services;
```

Предоставляет `IServiceProvider` уже построенного приложения.

То есть здесь важно отличие от `builder.Services`:


`builder.Services`:
- `IServiceCollection`
 - регистрация сервисов

`app.Services`:
- `IServiceProvider`
- получение зарегистрированных сервисов

### `StartAsync(...)`

Запускает host и связанную с ним инфраструктуру приложения.

Для web-приложения после запуска host приложение начинает работать как запущенное серверное приложение.

### `StopAsync(...)`

Инициирует **корректную остановку** host:

Остановка выполняется не как мгновенное уничтожение процесса, а через lifecycle host, позволяя инфраструктуре и сервисам приложения корректно завершить работу.

## Методы запуска более высокого уровня

Помимо методов самого `IHost`, для него существуют extension methods, предоставляющие более удобные варианты запуска и ожидания завершения приложения:

```cs
// Запуск и блокирующее ожидание завершения 
app.Run();

// Асинхронный запуск и ожидание завершения
await app.RunAsync();

// Ожидание сигнала остановки
app.WaitForShutdown();
await app.WaitForShutdownAsync(...);
```

Важно различать:

- `StartAsync(...)` — запускает host и возвращает управление после запуска
- `Run / RunAsync` — запускают host и ожидают завершения приложения
- `StopAsync(...)` — инициирует корректную остановку

## Общая роль

Таким образом, через `IHost` объект `WebApplication` предоставляет:

- доступ к `IServiceProvider`
- запуск приложения
- остановку приложения
- ожидание завершения
- освобождение ресурсов

---

# 4. Роль `IApplicationBuilder`

Через `IApplicationBuilder` объект `WebApplication` выступает как **builder middleware pipeline**, через который настраивается последовательность обработки HTTP-запросов.

Контракт `IApplicationBuilder`:

- `ApplicationServices`
- `ServerFeatures`
- `Properties`
	
- `Use(...)`
- `New()`
- `Build()`

### `ApplicationServices`

Предоставляет `IServiceProvider`, используемый при построении pipeline.

В случае `WebApplication` обычно тот же контейнер доступен напрямую через:

```cs
app.Services;
```

### `ServerFeatures`

Предоставляет набор **features web-сервера**, доступных приложению.

Через него инфраструктура ASP.NET Core может получать дополнительные возможности конкретного server implementation.

### `Properties`

Коллекция дополнительных данных, связанных с конкретным `IApplicationBuilder`.

Используется в основном самой инфраструктурой и extension methods для передачи состояния при построении pipeline.

---

## Построение pipeline

Главный метод интерфейса:

```cs
// Добавление компонента в pipeline
app.Use(...);
```

`Use(...)` последовательно добавляет middleware-компоненты.

---

## `Build()`

У `IApplicationBuilder` есть собственный:

```cs
app.Build();
```

Он **не имеет отношения к `WebApplicationBuilder.Build()`**.

Здесь `Build()` собирает зарегистрированные middleware в единый обработчик запросов:

```
middleware registrations
        ↓
IApplicationBuilder.Build()
        ↓
RequestDelegate
```

> При обычном использовании вызывается инфраструктурой, а не прикладным кодом.

---

## `New()`

```cs
app.New();
```

Создаёт новый `IApplicationBuilder`, который можно использовать для построения отдельной цепочки обработки.

Такой механизм, в частности, полезен при создании **ветвей pipeline**.

---

## Основные extension methods

Поверх `IApplicationBuilder` определено множество extension methods, через которые обычно и конфигурируется HTTP pipeline:

```cs
// Добавление middleware
app.Use(...);
app.UseMiddleware<...>();

// Конечный обработчик
app.Run(...);

// Ветвление pipeline
app.Map(...);
app.MapWhen(...);
app.UseWhen(...);
```

Кроме общих операций, отдельные подсистемы ASP.NET Core предоставляют собственные middleware extensions:

```cs
// Routing
app.UseRouting();

// Authentication / Authorization
app.UseAuthentication();
app.UseAuthorization();

// CORS
app.UseCors(...);

// Static files
app.UseStaticFiles();

// Exception handling
app.UseExceptionHandler(...);
```

---

# 5. Роль `IEndpointRouteBuilder`

Через `IEndpointRouteBuilder` объект `WebApplication` выступает как **builder набора эндпоинтов приложения**.

Именно через эту роль регистрируются конечные обработчики HTTP-запросов, между которыми routing затем выбирает подходящий endpoint.

Контракт `IEndpointRouteBuilder`:

- `ServiceProvider`
- `DataSources`
- `CreateApplicationBuilder()`

## Основные свойства

```cs
// DI-контейнер приложения
app.ServiceProvider;

// Источники зарегистрированных endpoints
app.DataSources;
```

На `WebApplication` эти члены интерфейса могут быть доступны не как обычные публичные свойства `app`, поскольку часть контрактов реализуется явно. Здесь важна именно структура `IEndpointRouteBuilder`.

### `ServiceProvider`

Предоставляет `IServiceProvider`, который может использоваться инфраструктурой routing и регистрации endpoints.

### `DataSources`

Содержит коллекцию `EndpointDataSource`.

`EndpointDataSource` представляет источник, из которого routing получает зарегистрированные endpoints.

При обычной разработке напрямую работать с `DataSources` обычно не требуется — endpoints чаще регистрируются через extension methods.

### `CreateApplicationBuilder()`

```cs
routeBuilder.CreateApplicationBuilder();
```

Создаёт `IApplicationBuilder`, который инфраструктура может использовать при построении обработчика endpoint.

В прикладном коде этот метод обычно напрямую не вызывается.

---

## Регистрация endpoints

Большая часть API, которой разработчик реально пользуется, представлена extension-методами над `IEndpointRouteBuilder`.

```cs
// Endpoints для конкретных HTTP-методов
app.MapGet(...);
app.MapPost(...);
app.MapPut(...);
app.MapPatch(...);
app.MapDelete(...);

// Endpoint для произвольного набора HTTP-методов
app.MapMethods(...);

// Endpoint без ограничения конкретным HTTP-методом
app.Map(...);

// Группировка endpoints
app.MapGroup(...);

// Fallback endpoint
app.MapFallback(...);
```

Отдельные подсистемы ASP.NET Core добавляют собственные extension methods:

```cs
// Controllers
app.MapControllers();

// Другие подсистемы
app.MapHealthChecks(...);
```

Их механика рассматривается уже вместе с соответствующими технологиями.

---

# 6. Основные свойства `WebApplication`

Помимо ролей, предоставляемых через реализуемые интерфейсы, `WebApplication` содержит несколько основных публичных свойств:

- `Services`
- `Configuration`
- `Environment`
- `Lifetime`
- `Logger`
- `Urls`

### `Services`

```cs
app.Services;
```

Имеет тип:

```cs
IServiceProvider
```

Предоставляет доступ к уже построенному DI-контейнеру приложения.

---

### `Configuration`

```cs
app.Configuration;
```

Предоставляет итоговую конфигурацию приложения.

Через неё можно читать конфигурационные значения уже после `Build()`:

```cs
var value = app.Configuration["SomeKey"];
```

Это та же общая система конфигурации, которая на этапе построения была доступна через:

```cs
builder.Configuration;
```

---

### `Environment`

```cs
app.Environment;
```

Имеет тип:

```cs
IWebHostEnvironment
```

Предоставляет информацию об окружении работающего приложения:

```cs
app.Environment.EnvironmentName;
app.Environment.ApplicationName;
app.Environment.ContentRootPath;
app.Environment.WebRootPath;
```

То есть информация об environment доступна как во время построения приложения, так и после `Build()`.

---

### `Lifetime`

```cs
app.Lifetime;
```

Имеет тип:

```cs
IHostApplicationLifetime
```

Предоставляет информацию о lifecycle приложения и возможность реагировать на его основные стадии:

```cs
ApplicationStarted
ApplicationStopping
ApplicationStopped
```

Также через него можно запросить остановку приложения:

```cs
app.Lifetime.StopApplication();
```

---

### `Logger`

```cs
app.Logger;
```

Имеет тип:

```cs
ILogger
```

Предоставляет logger, связанный с самим приложением:

```cs
app.Logger.LogInformation(...);
app.Logger.LogWarning(...);
app.Logger.LogError(...);
```

Прикладные компоненты обычно получают собственные `ILogger<T>` через DI.

---

### `Urls`

```cs
app.Urls;
```

Содержит коллекцию URL-адресов, на которых web-приложение должно принимать запросы.

Например:

```cs
app.Urls.Add("http://localhost:5000");
app.Urls.Add("https://localhost:5001");
```

---

# 7. Настройка HTTP-приложения после `Build()`

После создания `WebApplication` основная конфигурация HTTP-приложения выполняется через объект `app`.

```cs
var app = builder.Build();
```

На этом этапе обычно настраиваются две основные вещи:

- `Middleware Pipeline`
- `Endpoints`

## Настройка middleware pipeline

Через роль `IApplicationBuilder` в pipeline добавляются middleware:

```cs
// Добавление middleware
app.Use(...);
app.UseMiddleware<...>();

// Готовые middleware ASP.NET Core
app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();
app.UseCors(...);
app.UseExceptionHandler(...);
```

## Регистрация endpoints

Через роль `IEndpointRouteBuilder` регистрируются endpoints приложения:

```cs
// Minimal API endpoints
app.MapGet(...);
app.MapPost(...);
app.MapPut(...);
app.MapDelete(...);

// Группы endpoints
app.MapGroup(...);

// Controllers
app.MapControllers();
```

---

# 8. Запуск приложения

После настройки middleware pipeline и регистрации endpoints `WebApplication` необходимо запустить.

Для этого доступны несколько основных операций:

```cs
// Запуск и ожидание завершения приложения
app.Run();
await app.RunAsync();

// Только запуск приложения
await app.StartAsync();

// Корректная остановка приложения
await app.StopAsync();
```

### `Run()` и `RunAsync()`

`Run()` и `RunAsync()` запускают приложение и затем **ожидают его завершения**.

Поэтому обычно именно `Run()` находится в конце `Program.cs`:

```cs
var app = builder.Build();

app.Use...();
app.Map...();

app.Run();
```

Разница между ними заключается в форме ожидания:

- `Run()` — синхронно блокирует вызывающий поток до завершения приложения
- `RunAsync()` — асинхронно ожидает завершения приложения

---

### `StartAsync()`

`StartAsync()` **только запускает приложение**, после чего возвращает управление вызывающему коду.

```cs
await app.StartAsync();

// приложение уже работает
DoSomething();

await app.StopAsync();
```

`StartAsync()` полезен, когда после запуска host вызывающий код должен продолжить выполнять собственную работу.

---

### `StopAsync()`

`StopAsync()` инициирует **корректную остановку приложения**:

При такой остановке ASP.NET Core и связанные сервисы получают возможность завершить свою работу корректно, а не просто быть мгновенно уничтоженными вместе с процессом.
