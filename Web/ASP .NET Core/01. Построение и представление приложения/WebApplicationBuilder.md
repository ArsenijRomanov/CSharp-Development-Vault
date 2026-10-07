
---

## Оглавление

- [[#1. Назначение `WebApplicationBuilder`|1. Назначение WebApplicationBuilder]]
- [[#2. Что настраивается через builder|2. Что настраивается через builder]]
- [[#3. `Services`|3. Services]]
- [[#4. `Configuration`|4. Configuration]]
- [[#5. `Logging`|5. Logging]]
- [[#6. `Metrics`|6. Metrics]]
- [[#7. `Environment`|7. Environment]]
- [[#8. `Host`|8. Host]]
- [[#9. `WebHost`|9. WebHost]]
- [[#10. `Build()`|10. Build()]]

---

# 1. Назначение `WebApplicationBuilder`

**`WebApplicationBuilder`** — объект ASP.NET Core, используемый на этапе построения и конфигурации будущего web-приложения.

Обычно создаётся в начале приложения:

```cs
var builder = WebApplication.CreateBuilder(args);
```

`WebApplicationBuilder` объединяет основные направления конфигурации приложения:

```
WebApplicationBuilder
│
├── Services
├── Configuration
├── Logging
├── Metrics
├── Environment
├── Host
└── WebHost
```

Через него до построения приложения можно:

- регистрировать сервисы
- настраивать конфигурацию
- настраивать логирование и метрики
- получать информацию об окружении
- изменять настройки host и web host

Сам `WebApplicationBuilder` **не является работающим web-приложением**. Он накапливает конфигурацию, на основе которой затем строится `WebApplication`.

```cs
var app = builder.Build();
```

Концептуально:

```
WebApplication.CreateBuilder(...)
            ↓
   WebApplicationBuilder
            ↓
конфигурация будущего приложения
            ↓
          Build()
            ↓
      WebApplication
```

Таким образом, `WebApplicationBuilder` представляет **фазу построения приложения**, а `Build()` служит границей между конфигурацией будущего приложения и работой с уже построенным `WebApplication`.

---

# 2. Что настраивается через builder

`WebApplicationBuilder` выступает как единая точка доступа к основным направлениям конфигурации будущего ASP.NET Core приложения.

Его основные свойства можно представить так:

- `Services`           — регистрация сервисов приложения
- `Configuration` — конфигурационные данные приложения
- `Logging`             — настройка логирования
- `Metrics`             — настройка инфраструктуры метрик
- `Environment`     — информация о текущем окружении
- `Host`                   — общая конфигурация host
- `WebHost`             — web-specific конфигурация приложения

`WebApplicationBuilder` агрегирует объекты и билдеры различных подсистем, через которые выполняется их конфигурация, через один `builder` приложение получает доступ к этим подсистемам:

```cs
builder.Services;
builder.Configuration;
builder.Logging;
builder.Metrics;
builder.Environment;
builder.Host;
builder.WebHost;
```

Все накопленные настройки затем используются при вызове:

```cs
var app = builder.Build();
```

для построения `WebApplication`.

---

# 3. `Services`

`Services` предоставляет доступ к коллекции сервисов, которые будут использоваться системой Dependency Injection приложения.

```cs
builder.Services;
```

Свойство имеет тип:

```cs
IServiceCollection
```

На этапе построения приложения через эту коллекцию регистрируются зависимости и инфраструктурные сервисы.

```cs
// Регистрация пользовательских сервисов
builder.Services.AddTransient<...>();
builder.Services.AddScoped<...>();
builder.Services.AddSingleton<...>();

// Регистрация инфраструктуры ASP.NET Core
builder.Services.AddControllers();
builder.Services.AddAuthentication(...);
builder.Services.AddAuthorization();
```

Важно, что `Services` содержит не сами готовые объекты приложения, а в первую очередь **описания регистраций**, по которым DI-контейнер впоследствии сможет создавать и предоставлять необходимые экземпляры.

Через `Services` регистрируются как собственные сервисы приложения, так и функциональность самого ASP.NET Core, если она должна быть доступна через DI.

---

# 4. `Configuration`

`Configuration` предоставляет доступ к конфигурации приложения.

```cs
builder.Configuration;
```

Свойство имеет тип:

```cs
ConfigurationManager
```

Через него можно как читать уже доступные конфигурационные значения, так и подключать дополнительные источники конфигурации.

```cs
// Чтение конфигурации
var value = builder.Configuration["SomeKey"];

// Подключение дополнительных источников
builder.Configuration.AddJsonFile(...);
builder.Configuration.AddEnvironmentVariables();
builder.Configuration.AddCommandLine(...);
```

При создании builder ASP.NET Core уже подключает набор стандартных источников конфигурации, например:

- `appsettings.json`
- `appsettings.{Environment}.json`
- `environment variables`
- `command-line arguments`
- и т.д.

Конфигурация представляет собой набор значений, организованных по ключам:

```cs
ConnectionStrings:MainDatabase
Logging:LogLevel:Default
MyService:Timeout
```

Доступ к вложенным значениям выполняется через составные ключи:

```cs
builder.Configuration["Logging:LogLevel:Default"];
```

Несколько источников могут задавать один и тот же ключ. В таком случае итоговое значение определяется порядком и приоритетом подключённых источников.

`Configuration` используется не только для непосредственного чтения значений, но и как основа для последующего binding конфигурации на типизированные объекты.

---

# 5. `Logging`

`Logging` предоставляет доступ к настройке инфраструктуры логирования приложения.

```cs
builder.Logging;
```

Свойство имеет тип:

```cs
ILoggingBuilder
```

Через него на этапе построения приложения настраивается, **какие logging providers будут использоваться и какие сообщения должны попадать в лог**.

Например:

```cs
// Добавление logging providers
builder.Logging.AddConsole();
builder.Logging.AddDebug();

// Удаление зарегистрированных providers
builder.Logging.ClearProviders();

// Настройка фильтрации логов
builder.Logging.AddFilter(...);
```

**Logging provider** определяет, куда и каким способом будут записываться сообщения.

Само приложение обычно пишет сообщения через абстракцию `ILogger`.

---

# 6. `Metrics`

`Metrics` предоставляет доступ к настройке инфраструктуры метрик приложения.

```cs
builder.Metrics;
```

Свойство имеет тип:

```cs
IMetricsBuilder
```

Через него на этапе построения приложения можно настраивать, **какие метрики включены и куда направляется их вывод**.

Например:

```cs
// Подключение конфигурации метрик
builder.Metrics.AddConfiguration(...);

// Добавление listener
builder.Metrics.AddListener(...);

// Отладочный вывод метрик
builder.Metrics.AddDebugConsole();
```

Метрики используются для числового наблюдения за состоянием и поведением приложения, например:

- количество запросов
- длительность операций
- число ошибок
- размер очередей
- использование ресурсов

`builder.Metrics` отвечает именно за **конфигурацию metrics infrastructure**, а сами измерения во время работы приложения создаются и публикуются через соответствующие metrics API.

---

# 7. `Environment`

`Environment` предоставляет информацию об окружении, в котором запускается ASP.NET Core приложение.

```cs
builder.Environment;
```

Свойство имеет тип:

```cs
IWebHostEnvironment
```

Через него доступны основные сведения о текущем приложении и его файловом окружении:

```cs
// Имя текущего environment
builder.Environment.EnvironmentName;

// Имя приложения
builder.Environment.ApplicationName;

// Корневая директория приложения
builder.Environment.ContentRootPath;

// Корневая директория статических web-файлов
builder.Environment.WebRootPath;
```

ASP.NET Core обычно использует именованные окружения:

```
Development
Staging
Production
```

Текущее окружение можно проверять через специальные методы:

```cs
builder.Environment.IsDevelopment();
builder.Environment.IsStaging();
builder.Environment.IsProduction();
```

`Environment` в отличие от `Services`, `Configuration` или `Logging` используется в основном не для построения отдельной подсистемы, а для получения информации о среде, в которой строится и выполняется приложение.

---

# 8. `Host`

`Host` предоставляет доступ к настройке **общей hosting-инфраструктуры .NET-приложения**.

```cs
builder.Host;
```

Свойство имеет тип:

```cs
ConfigureHostBuilder
```

`ConfigureHostBuilder` реализует `IHostBuilder`, поэтому через `builder.Host` доступны host-specific настройки, но сам host здесь не строится — окончательное построение происходит через `builder.Build()`. 

Через `Host` можно настраивать несколько основных вещей:

```cs
// Конфигурация host
builder.Host.ConfigureHostConfiguration(...);

// Конфигурация приложения
builder.Host.ConfigureAppConfiguration(...);

// Регистрация сервисов
builder.Host.ConfigureServices(...);

// Настройка DI-контейнера
builder.Host.ConfigureContainer<...>(...);

// Замена фабрики ServiceProvider
builder.Host.UseServiceProviderFactory<...>(...);
```

Важно отличать `Host` от уже рассмотренных свойств `Services` и `Configuration`.

Например, сервисы обычно регистрируются напрямую:

```cs
builder.Services.Add...();
```

а конфигурация изменяется через:

```cs
builder.Configuration;
```

`builder.Host` нужен в основном тогда, когда требуется доступ к более общим механизмам Generic Host или существующим extension methods для `IHostBuilder`. 

Например, через него можно изменить параметры lifecycle host:

```cs
// Настройка поведения host при завершении приложения
builder.Host.ConfigureHostOptions(...);
```

На уровне архитектуры:

```
Generic Host
│
├── lifecycle приложения
├── DI infrastructure
├── configuration
├── logging
└── hosted services

        ↑
   builder.Host
```

То есть `Host` — это точка доступа к **общей инфраструктуре .NET host**, не специфичной только для HTTP.

---

# 9. `WebHost`

`WebHost` предоставляет доступ к **web-specific настройкам host**, связанным с запуском ASP.NET Core как web-приложения.

```cs
builder.WebHost;
```

Свойство имеет тип:

```cs
ConfigureWebHostBuilder
```

`ConfigureWebHostBuilder` реализует `IWebHostBuilder` и предоставляет настройки, специфичные именно для web-hosting.

Через `WebHost` можно настраивать, например:

```cs
// Адреса, на которых приложение принимает запросы
builder.WebHost.UseUrls(...);

// Web root приложения
builder.WebHost.UseWebRoot(...);

// Настройка web-сервера
builder.WebHost.ConfigureKestrel(...);

// Общие web-host settings
builder.WebHost.UseSetting(...);
```

`Host` относится к приложению как к .NET host вообще, а `WebHost` добавляет настройки, необходимые именно для web-приложения.

В типичном ASP.NET Core приложении большая часть стандартной web-конфигурации уже создаётся `WebApplication.CreateBuilder(...)`, поэтому напрямую обращаться к `builder.WebHost` требуется в основном при изменении конкретных web-host/server настроек.

---

# 10. `Build()`

`Build()` завершает этап конфигурации `WebApplicationBuilder` и создаёт объект `WebApplication`.

```cs
var app = builder.Build();
```

До вызова `Build()` приложение существует в виде набора настроек, регистраций и конфигурации:

```
WebApplicationBuilder
│
├── Services
├── Configuration
├── Logging
├── Metrics
├── Environment
├── Host
└── WebHost
```

При вызове:

```cs
builder.Build();
```

эта конфигурация используется для построения готового приложения.

После `Build()` происходит переход от **конфигурации будущего приложения** к работе с уже построенным `WebApplication`.

```
до Build()
    → настройка инфраструктуры приложения

Build()
    → построение приложения

после Build()
    → настройка HTTP pipeline и endpoints
    → запуск приложения
```

Например:

```cs
var builder = WebApplication.CreateBuilder(args);

// Конфигурация будущего приложения
builder.Services.Add...();
builder.Logging.Add...();

var app = builder.Build();

// Конфигурация построенного HTTP-приложения
app.Use...();
app.Map...();

app.Run();
```

`Build()` также приводит к построению инфраструктуры, необходимой для работы приложения, включая DI-контейнер на основе регистраций из `builder.Services`.
