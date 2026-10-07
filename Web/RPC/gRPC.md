
---

## Оглавление

- [[#1. RPC|1. RPC]]
- [[#2. Контракт и генерация кода|2. Контракт и генерация кода]]
- [[#3. Сервер и клиент в .NET|3. Сервер и клиент в .NET]]
- [[#4. Четыре типа RPC|4. Четыре типа RPC]]
- [[#5. Контекст, завершение и ошибки|5. Контекст, завершение и ошибки]]
- [[#6. Interceptors|6. Interceptors]]

---

# 1. RPC

**RPC — Remote Procedure Call** — подход, при котором клиент вызывает функцию на другом процессе или сервере почти так же, как обычный локальный метод

<div style="text-align: center;">

<img src="Pasted image 20260805011036.png" style="max-width: 450px; width: 100%;">

</div>

**gRPC** — фреймворк удалённого вызова процедур, в котором клиент вызывает методы сервиса, работающего в другом процессе или на другом сервере

Контракт сервиса описывается в `.proto`, после чего для клиента и сервера генерируется типизированный код. Для передачи сообщений используется Protobuf, а транспортом служит HTTP/2.

## 1.1. RPC-модель

В gRPC клиент работает с сервисами и методами:

```cs
UserReply reply = await client.GetUserAsync(
    new GetUserRequest
    {
        UserId = 42
    });
```

Логически это выглядит как вызов метода, но фактически сгенерированный клиент:

1. сериализует request
2. формирует gRPC-вызов
3. передаёт его по HTTP/2
4. получает ответ
5. десериализует response

На сервере gRPC runtime находит соответствующий обработчик и вызывает его с десериализованным сообщением

## 1.2. Связь с HTTP/2

Один RPC-вызов обычно выполняется внутри одного HTTP/2-потока:

```
HTTP/2 connection
└── HTTP/2 stream
    └── один RPC-вызов
        ├── metadata
        ├── одно или несколько gRPC-сообщений
        └── итоговый status
```

HTTP/2 даёт gRPC:

- мультиплексирование нескольких RPC через одно соединение
- независимые двусторонние потоки
- управление потоком данных

Благодаря этому один RPC может содержать не только один запрос и один ответ, но и потоки сообщений в одном или обоих направлениях.

## 1.3. Когда применять

gRPC хорошо подходит для:

- взаимодействия внутренних сервисов
- строго типизированных контрактов
- частых вызовов между приложениями
- обмена большим количеством небольших сообщений
- client, server и bidirectional streaming
- систем, написанных на разных поддерживаемых языках

---

# 2. Контракт и генерация кода

## 2.1. Описание сервиса

gRPC-сервис описывается в `.proto` через `service`, а удалённые операции — через `rpc`

```protobuf
service UserService {             // набор удалённых методов
  rpc GetUser(GetUserRequest)     // конкретный RPC-метод
      returns (GetUserResponse);
}

message GetUserRequest {          // входное сообщение
  int64 user_id = 1;
}

message GetUserResponse {         // выходное сообщение
  int64 user_id = 1;
  string user_name = 2;
  string email = 3;
}
```

Клиент и сервер используют один контракт, поэтому им заранее известны имена методов и типы передаваемых сообщений.

## 2.2. Формы RPC-методов

Направление потока обозначается ключевым словом `stream`

```cs
service UserService {
  // Unary (одно сообщение)
  rpc GetUser(GetUserRequest)
      returns (GetUserResponse);

  // Server streaming (поток сообщений от сервера)
  rpc GetUsers(GetUsersRequest)
      returns (stream User);

  // Client streaming (поток сообщений от клиента)
  rpc ImportUsers(stream User)
      returns (ImportUsersResponse);

  // Bidirectional streaming (двунаправленный поток сообщений)
  rpc Synchronize(stream SyncRequest)
      returns (stream SyncResponse);
}
```

## 2.3. Генерация C#-кода

`Grpc.Tools` запускает генерацию во время сборки проекта

```xml
<ItemGroup>
  <PackageReference Include="Google.Protobuf"
                    Version="..." />

  <PackageReference Include="Grpc.Tools"
                    Version="..."
                    PrivateAssets="All" />
</ItemGroup>
```

Подключение контракта:

```xml
<ItemGroup>
  <Protobuf Include="Protos\users.proto"
            GrpcServices="Both" />
</ItemGroup>
```

`GrpcServices` определяет, какой gRPC-код необходимо сгенерировать:

- `Server`  $\rightarrow$ серверный базовый класс
- `Client`  $\rightarrow$ клиентский класс
- `Both`      $\rightarrow$ клиентский и серверный код
- `None`     $\rightarrow$ только Protobuf-сообщения

## 2.4. Сгенерированные типы

Для такого сервиса:

```protobuf
service UserService {
  rpc GetUser(GetUserRequest)
      returns (GetUserResponse);
}
```

генерируются два основных gRPC-типа:

```cs
UserService.UserServiceBase
UserService.UserServiceClient
```

### Серверный базовый класс

```cs
public class UserGrpcService : UserService.UserServiceBase
{
    public override Task<GetUserResponse> GetUser(
        GetUserRequest request,
        ServerCallContext context)
    {
        // Серверная логика
    }
}
```

`UserServiceBase` содержит виртуальные методы, которые сервер переопределяет своей реализацией

### Клиентский класс

```cs
var client =
    new UserService.UserServiceClient(channel);

GetUserResponse response =
    await client.GetUserAsync(
        new GetUserRequest
        {
            UserId = 42
        });
```

`UserServiceClient` содержит типизированные методы, которые формируют удалённые вызовы. Сетевую логику вручную писать не требуется.

---

# 3. Сервер и клиент в .NET

## 3.1. Настройка сервера

Для размещения gRPC-сервисов используется ASP.NET Core и пакет `Grpc.AspNetCore`

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddGrpc();

var app = builder.Build();

app.MapGrpcService<UserGrpcService>();

app.Run();
```

- `AddGrpc` — регистрирует инфраструктуру gRPC
- `MapGrpcService<UserGrpcService>` — добавляет сервис в маршрутизацию ASP.NET Core

Каждую серверную реализацию необходимо отдельно подключить через `MapGrpcService<T>()`.


## 3.2. Реализация сервиса

Серверный класс наследуется от сгенерированного `UserServiceBase`

```cs
public sealed class UserGrpcService : UserService.UserServiceBase
{
    private readonly IUserRepository _repository;
	
    public UserGrpcService(IUserRepository repository)
    {
        _repository = repository;
    }
	
    public override async Task<GetUserResponse> GetUser(
        GetUserRequest request,           // десериализованный запрос клиента
        ServerCallContext context)        // контекст текущего RPC-вызова
    {
        User? user = await _repository.FindAsync(
            request.UserId,
            context.CancellationToken);
		
        if (user is null)
        {
            throw new RpcException(
                new Status(
                    StatusCode.NotFound,
                    "User not found"));
        }
		
        return new GetUserResponse        // ответ сервера
        {
            UserId = user.Id,
            UserName = user.Name,
            Email = user.Email
        };
    }
}
```

Зависимости внедряются через обычный ASP.NET Core DI. Экземпляр gRPC-сервиса по умолчанию создаётся с `Scoped` lifetime — на один RPC-вызов.


## 3.3. Создание клиента

Для клиента используется пакет `Grpc.Net.Client`

```cs
using Grpc.Net.Client;

using GrpcChannel channel = GrpcChannel.ForAddress("https://localhost:5001");

var client = new UserService.UserServiceClient(channel);

GetUserResponse response = await client.GetUserAsync(
        new GetUserRequest
        {
            UserId = 42
        });

Console.WriteLine(response.UserName);
```

Канал является долгоживущим объектом. Его не следует создавать заново для каждого вызова:

```cs
// Плохо
foreach (long id in userIds)
{
    using var channel =
        GrpcChannel.ForAddress(address);

    var client =
        new UserService.UserServiceClient(channel);

    await client.GetUserAsync(
        new GetUserRequest { UserId = id });
}
```

Правильнее переиспользовать один канал и созданные через него клиенты. Канал безопасно использовать для параллельных вызовов, а несколько RPC могут выполняться через одно HTTP/2-соединение.


## 3.4. Клиент через Dependency Injection

В ASP.NET Core приложении клиент обычно регистрируют через `Grpc.Net.ClientFactory`

```cs
builder.Services.AddGrpcClient<UserService.UserServiceClient>(
    options =>
    {
        options.Address =
            new Uri("https://users-service");
    });
```

После этого клиент внедряется через конструктор.

Client factory централизованно создаёт и настраивает логические gRPC-клиенты, а также управляет используемыми ими HTTP-обработчиками и каналами.

---

# 4. Четыре типа RPC

gRPC поддерживает четыре формы вызова, которые различаются количеством сообщений в каждом направлении. Во всех случаях это **один RPC-вызов**, но streaming-вызов может содержать несколько самостоятельных Protobuf-сообщений.

## Контракт

```protobuf
message NumberRequest {
  int32 value = 1;
}

message NumberResponse {
  int32 value = 1;
}

message SummaryResponse {
  int32 count = 1;
  int64 sum = 2;
}

service NumberService {
  // Одно сообщение → одно сообщение
  rpc Double(NumberRequest)
      returns (NumberResponse);

  // Одно сообщение → поток сообщений
  rpc Generate(NumberRequest)
      returns (stream NumberResponse);

  // Поток сообщений → одно сообщение
  rpc Sum(stream NumberRequest)
      returns (SummaryResponse);

  // Поток сообщений ↔ поток сообщений
  rpc Transform(stream NumberRequest)
      returns (stream NumberResponse);
}
```

```
Unary
→ request → response

Server streaming
→ request → response, response, response...

Client streaming
→ request, request, request... → response

Bidirectional streaming
→ request, request... ↔ response, response...
```

## 4.1. Unary RPC

Клиент отправляет одно сообщение и получает одно сообщение

```
NumberRequest → NumberResponse
```

### Сервер

```cs
public override Task<NumberResponse> Double(
    NumberRequest request,
    ServerCallContext context)
{
    return Task.FromResult(
        new NumberResponse
        {
            Value = request.Value * 2
        });
}
```

### Клиент

```cs
NumberResponse response =
    await client.DoubleAsync(
        new NumberRequest
        {
            Value = 10
        });

Console.WriteLine(response.Value);
```

Unary подходит для обычных коротких операций

## 4.2. Server streaming

Клиент отправляет одно сообщение, после чего сервер постепенно возвращает поток сообщений

```protob
NumberRequest
→ NumberResponse №1
→ NumberResponse №2
→ NumberResponse №3
```

### Сервер

```cs
public override async Task Generate(
    NumberRequest request,
    IServerStreamWriter<NumberResponse> responseStream,
    ServerCallContext context)
{
    for (var value = 1; value <= request.Value; value++)
    {
        await responseStream.WriteAsync(
            new NumberResponse
            {
                Value = value
            });
    }
}
```

Каждый `WriteAsync` отправляет отдельное Protobuf-сообщение

### Клиент

```cs
using var call = client.Generate(
    new NumberRequest
    {
        Value = 5
    });

await foreach (
    NumberResponse response
    in call.ResponseStream.ReadAllAsync())
{
    Console.WriteLine(response.Value);
}
```

Клиент начинает обработку до завершения всего вызова

Server streaming подходит для:

- большой последовательности результатов
- постепенно появляющихся результатов
- уведомлений и обновлений
- длительных вычислений

## 4.3. Client streaming

Клиент отправляет поток сообщений, а сервер после его завершения возвращает один итоговый ответ

```
NumberRequest №1
NumberRequest №2
NumberRequest №3
→ SummaryResponse
```

### Сервер

```cs
public override async Task<SummaryResponse> Sum(
    IAsyncStreamReader<NumberRequest> requestStream,
    ServerCallContext context)
{
    var count = 0;
    long sum = 0;

    await foreach (
        NumberRequest request
        in requestStream.ReadAllAsync(
            context.CancellationToken))
    {
        count++;
        sum += request.Value;
    }

    return new SummaryResponse
    {
        Count = count,
        Sum = sum
    };
}
```

### Клиент

```cs
using var call = client.Sum();

for (var value = 1; value <= 5; value++)
{
    await call.RequestStream.WriteAsync(
        new NumberRequest
        {
            Value = value
        });
}

await call.RequestStream.CompleteAsync();

SummaryResponse response =
    await call.ResponseAsync;

Console.WriteLine(response.Sum);
```

`CompleteAsync` сообщает серверу, что клиент больше не будет отправлять сообщения. После этого сервер может завершить чтение и вернуть итоговый ответ.

Client streaming подходит для:

- загрузки данных частями
- передачи телеметрии
- импорта последовательности объектов
- агрегации большого набора значений

## 4.4. Bidirectional streaming

Клиент и сервер независимо отправляют друг другу потоки сообщений

```
клиент → request №1
клиент → request №2
сервер ← response №1
клиент → request №3
сервер ← response №2
```

Серверу не нужно ждать завершения клиентского потока, чтобы начать отправлять ответы

### Сервер

```cs
public override async Task Transform(
    IAsyncStreamReader<NumberRequest> requestStream,
    IServerStreamWriter<NumberResponse> responseStream,
    ServerCallContext context)
{
    await foreach (
        NumberRequest request
        in requestStream.ReadAllAsync(
            context.CancellationToken))
    {
        await responseStream.WriteAsync(
            new NumberResponse
            {
                Value = request.Value * 2
            });
    }
}
```

В этом простом варианте сервер читает сообщение, обрабатывает его и сразу отправляет результат

### Клиент

Чтение ответов запускается отдельно от отправки запросов:

```cs
using var call = client.Transform();

Task readTask = ReadResponsesAsync(
    call.ResponseStream);

for (var value = 1; value <= 5; value++)
{
    await call.RequestStream.WriteAsync(
        new NumberRequest
        {
            Value = value
        });
}

await call.RequestStream.CompleteAsync();

await readTask;
```

```cs
static async Task ReadResponsesAsync(
    IAsyncStreamReader<NumberResponse> responseStream)
{
    await foreach (
        NumberResponse response
        in responseStream.ReadAllAsync())
    {
        Console.WriteLine(response.Value);
    }
}
```

Здесь работают два независимых асинхронных процесса:

```
основной Task → отправляет запросы
readTask      → принимает ответы
```

Bidirectional streaming подходит для продолжительного диалога:

- чат
- синхронизация
- телеметрия с управляющими командами
- интерактивная обработка
- передача данных с промежуточной обратной связью

Обе стороны могут отправлять разное количество сообщений. Соответствие вида «один запрос — один ответ» не требуется.

## 4.6. Сигнатуры серверных методов

```cs
// Unary
Task<Response> Method(
    Request request,
    ServerCallContext context);
```

```cs
// Server streaming
Task Method(
    Request request,
    IServerStreamWriter<Response> responseStream,
    ServerCallContext context);
```

```cs
// Client streaming
Task<Response> Method(
    IAsyncStreamReader<Request> requestStream,
    ServerCallContext context);
```

```cs
// Bidirectional streaming
Task Method(
    IAsyncStreamReader<Request> requestStream,
    IServerStreamWriter<Response> responseStream,
    ServerCallContext context);
```

---

# 5. Контекст, завершение и ошибки

## 5.1. `ServerCallContext`

Каждый серверный метод получает `ServerCallContext` — контекст конкретного RPC-вызова

```cs
public override async Task<GetUserResponse> GetUser(
    GetUserRequest request,
    ServerCallContext context)
{
    // Контекст текущего вызова
}
```

Через него доступны:

- `RequestHeaders`      — метадата клиента
- `ResponseTrailers`  — метадата, отправляемая в конце вызова
- `Deadline`                   — крайний срок выполнения
- `CancellationToken` — отмена вызова
- `Method`                       — полное имя RPC-метода
- `Peer`                           — информация об удалённой стороне


В ASP.NET Core через `context.GetHttpContext()` также можно получить underlying `HttpContext`.

## 5.2. Metadata

**Metadata** — дополнительные пары ключ–значение, относящиеся ко всему RPC-вызову, а не к отдельному Protobuf-сообщению

```
бизнес-данные → request и response
технические данные вызова → metadata
```

Например:

```
correlation-id
trace-id
версия клиента
служебные параметры
```

Metadata передаётся через HTTP/2 headers и trailers. Ключи являются строками, а значения могут быть строковыми или бинарными. Зарезервированный префикс `grpc-` использовать нельзя.

Клиент передаёт request headers:

```cs
var metadata = new Metadata
{
    { "correlation-id", Guid.NewGuid().ToString() }
};

GetUserResponse response = await client.GetUserAsync(
    new GetUserRequest
    {
        UserId = 42
    },
    headers: metadata);
```

Сервер читает их через контекст:

```cs
string? correlationId = context.RequestHeaders.GetValue("correlation-id");
```

Metadata не стоит использовать вместо полей сообщения: она предназначена прежде всего для данных, описывающих вызов целиком

## 5.3. Response headers и trailers

Сервер может отправить metadata в начале ответа:

```cs
var headers = new Metadata
{
    { "server-version", "2.1" }
};

await context.WriteResponseHeadersAsync(headers);
```

Клиент получает её через `ResponseHeadersAsync`:

```cs
using var call = client.GetUserAsync(request);

Metadata headers =
    await call.ResponseHeadersAsync;

GetUserResponse response =
    await call.ResponseAsync;
```

Response headers приходят до сообщений ответа.

Trailers отправляются в конце RPC:

```cs
context.ResponseTrailers.Add(
    "processed-by",
    Environment.MachineName);
```

Получить их можно только после завершения ответа:

```cs
GetUserResponse response =
    await call.ResponseAsync;

Metadata trailers =
    call.GetTrailers();
```

## 5.4. Deadline

**Deadline** — момент времени, после которого клиент больше не готов ждать завершения RPC

```cs
try
{
    GetUserResponse response =
        await client.GetUserAsync(
            request,
            deadline: DateTime.UtcNow.AddSeconds(3));
}
catch (RpcException exception)
    when (exception.StatusCode ==
          StatusCode.DeadlineExceeded)
{
    Console.WriteLine("Время ожидания истекло");
}
```

По умолчанию deadline не задаётся, поэтому вызов потенциально может ожидать неопределённо долго. Для сетевых операций следует устанавливать реалистичное ограничение времени.

При превышении deadline:

```
клиент → завершает вызов с DeadlineExceeded
сервер → CancellationToken получает сигнал отмены
```

При этом CLR не может принудительно остановить серверный метод. Метод должен сам учитывать отмену.

## 5.5. Cancellation

Клиент может отменить вызов через `CancellationToken`

```cs
using var cancellationSource =
    new CancellationTokenSource();

GetUserResponse response =
    await client.GetUserAsync(
        request,
        cancellationToken:
            cancellationSource.Token);
```

На сервере используется токен из `ServerCallContext`:

```cs
public override async Task<GetUserResponse> GetUser(
    GetUserRequest request,
    ServerCallContext context)
{
    User? user = await _repository.FindAsync(
        request.UserId,
        context.CancellationToken);

    return Map(user);
}
```

Этот токен необходимо передавать в запросы к БД, HTTP-вызовы, ожидания и другую асинхронную работу. Иначе клиент уже прекратит ожидание, а сервер продолжит бесполезную обработку.

Отмена не откатывает уже выполненные изменения:

```
запись в БД завершилась
→ клиент отменил RPC
→ запись автоматически не отменяется
```

Это нужно учитывать при проектировании изменяющих состояние операций.

## 5.6. Статус вызова

Каждый RPC завершается gRPC-статусом

```
OK → вызов успешно завершён
не-OK status → вызов завершён ошибкой
```

Распространённые статусы:

- `InvalidArgument` — некорректный запрос
- `NotFound` — сущность не найдена
- `AlreadyExists` — сущность уже существует
- `PermissionDenied` — операция запрещена
- `Unauthenticated` — отсутствует допустимая аутентификация
- `Cancelled` — вызов отменён
- `DeadlineExceeded` — превышен deadline
- `Unavailable` — сервис или соединение временно недоступны
- `Internal` — внутренняя ошибка сервиса

Статусы являются частью стандартной модели ошибок gRPC и не зависят от формата сериализации сообщений.

## 5.7. `RpcException`

Сервер явно завершает вызов ошибкой через `RpcException`

```cs
if (user is null)
{
    throw new RpcException(
        new Status(
            StatusCode.NotFound,
            "User not found"));
}
```

Клиент получает исключение:

```cs
try
{
    GetUserResponse response =
        await client.GetUserAsync(request);
}
catch (RpcException exception)
    when (exception.StatusCode ==
          StatusCode.NotFound)
{
    Console.WriteLine(exception.Status.Detail);
}
```

`RpcException` может возникнуть не только из-за серверной бизнес-проверки, но и из-за сетевой ошибки, отмены или превышения deadline.

Необработанное обычное исключение сервера преобразуется в `StatusCode.Unknown` с обобщённым сообщением, чтобы внутренние детали исключения не утекали клиенту.

## 5.8. Техническая ошибка и бизнес-результат

gRPC status означает, что RPC не смог нормально выполнить запрошенную операцию:

- невалидный запрос
- нет доступа
- объект не найден
- сервис недоступен
- вызов отменён

Ожидаемый результат бизнес-операции часто лучше возвращать обычным сообщением:

```protobuf
message TransferResponse {
  bool completed = 1;
  string rejection_reason = 2;
}
```

- технически вызов выполнен, но перевод отклонён бизнес-правилом — обычный response со статусом OK
- вызов невозможно корректно выполнить — не-OK gRPC status

Граница зависит от семантики API, но gRPC-статусы не должны заменять полноценную модель бизнес-результатов

---

# 6. Interceptors

## 6.1. Что такое interceptor

**Interceptor** — компонент, который перехватывает gRPC-вызов и выполняет общую логику до или после обработчика, как middleware

Интерсепторы подходят для сквозной технической логики:

- логирование
- метрики
- добавление metadata
- валидация
- преобразование исключений

Интерсептор наследуется от `Interceptor` и переопределяет методы для нужных типов RPC.

## 6.2. Серверный interceptor

Серверный interceptor перехватывает входящие вызовы

```cs
public sealed class LoggingInterceptor : Interceptor
{
    private readonly ILogger<LoggingInterceptor> _logger;

    public LoggingInterceptor(ILogger<LoggingInterceptor> logger)
    {
        _logger = logger;
    }

    public override async Task<TResponse>UnaryServerHandler<TRequest, TResponse>(
            TRequest request,
            ServerCallContext context,
            UnaryServerMethod<TRequest, TResponse> continuation)
    {
        _logger.LogInformation(
            "Начало RPC {Method}",
            context.Method);

        try
        {
            TResponse response =
                await continuation(request, context);

            _logger.LogInformation(
                "RPC {Method} завершён",
                context.Method);

            return response;
        }
        catch (Exception exception)
        {
            _logger.LogError(
                exception,
                "Ошибка RPC {Method}",
                context.Method);

            throw;
        }
    }
}
```

`continuation` вызывает следующий interceptor в цепочке либо сам обработчик RPC

Если не вызвать `continuation`, запрос до обработчика не дойдёт.

## 6.3. Регистрация на сервере

Для всех gRPC-сервисов:

```cs
builder.Services.AddGrpc(options =>
{
    options.Interceptors.Add<LoggingInterceptor>();
});
```

Для конкретного сервиса:

```cs
builder.Services
    .AddGrpc()
    .AddServiceOptions<UserGrpcService>(options =>
    {
        options.Interceptors.Add<LoggingInterceptor>();
    });
```

Интерсепторы выполняются в порядке регистрации. Глобальные интерсепторы выполняются раньше интерсепторов конкретного сервиса. По умолчанию серверный interceptor создаётся отдельно для каждого RPC-вызова.

## 6.4. Клиентский interceptor

Клиентский interceptor перехватывает исходящие вызовы

```cs
public sealed class ClientLoggingInterceptor : Interceptor
{
    private readonly ILogger<ClientLoggingInterceptor> _logger;

    public ClientLoggingInterceptor(ILogger<ClientLoggingInterceptor> logger)
    {
        _logger = logger;
    }

    public override AsyncUnaryCall<TResponse>AsyncUnaryCall<TRequest, TResponse>(
            TRequest request,
            ClientInterceptorContext<TRequest, TResponse> context,
            AsyncUnaryCallContinuation<TRequest, TResponse> continuation)
    {
        _logger.LogInformation(
            "Вызов {Method}",
            context.Method.FullName);

        return continuation(request, context);
    }
}
```

`continuation` создаёт реальный RPC-вызов либо передаёт управление следующему interceptor. Клиентский interceptor имеет доступ к request, metadata, deadline и cancellation текущего вызова.

Регистрация через client factory:

```cs
builder.Services
    .AddGrpcClient<UserService.UserServiceClient>(
        options =>
        {
            options.Address =
                new Uri("https://users-service");
        })
    .AddInterceptor<ClientLoggingInterceptor>();
```

Интерсептор также можно подключить непосредственно к каналу через `Intercept`, после чего из полученного `CallInvoker` создаётся сгенерированный клиент.

## 6.5. Interceptors и streaming

Для каждого типа RPC существуют отдельные методы interceptor

Сервер:

```cs
UnaryServerHandler
ClientStreamingServerHandler
ServerStreamingServerHandler
DuplexStreamingServerHandler
```

Клиент:

```cs
AsyncUnaryCall
AsyncClientStreamingCall
AsyncServerStreamingCall
AsyncDuplexStreamingCall
```

Интерсептор может обернуть весь streaming-вызов, а при необходимости — дополнительно обернуть reader или writer для обработки каждого сообщения.

## 6.6. Отличие от middleware

Оба механизма образуют цепочку и позволяют выполнить код до и после следующего компонента

```
ASP.NET Core middleware
→ работает на уровне HTTP
→ применяется ко всем HTTP-запросам
→ видит HttpContext и потоки байтов

gRPC interceptor
→ работает на уровне gRPC
→ применяется к RPC-вызовам
→ видит десериализованные request и response
→ получает ServerCallContext
```

Middleware выполняется раньше серверных gRPC-interceptors. Для логики, связанной именно с RPC-методами и сообщениями, обычно удобнее interceptor.



