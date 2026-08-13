
---

## Оглавление

- [[#1. Domain-Driven Design|1. Domain-Driven Design]]
	
- [[#2. Strategic DDD|2. Strategic DDD]]
	- [[#Domain и Subdomain|Domain и Subdomain]]
	- [[#Ubiquitous Language|Ubiquitous Language]]
	- [[#Bounded Context|Bounded Context]]
	- [[#Context Map|Context Map]]
	- [[#Способы взаимодействия Bounded Context'ов|Способы взаимодействия Bounded Context'ов]]
	  
- [[#3. Tactical DDD|3. Tactical DDD]]
	- [[#Entity|Entity]]
	- [[#Value Object|Value Object]]
	- [[#Invariant|Invariant]]
	- [[#Aggregate и Aggregate Root|Aggregate и Aggregate Root]]
	- [[#Domain Service|Domain Service]]
	- [[#Domain Event|Domain Event]]
	- [[#Repository|Repository]]
	- [[#Factory|Factory]]
	- [[#Specification|Specification]]
	  
- [[#4. Anemic Domain Model и Rich Domain Model|4. Anemic Domain Model и Rich Domain Model]]
	  
- [[#5. Границы Domain и остального приложения|5. Границы Domain и остального приложения]]

---

# 1. Domain-Driven Design

**DDD (Domain-Driven Design)** — подход к проектированию сложных бизнес-систем, сформулированный **Эриком Эвансом в 2003 году**, в котором **домен и его бизнес-модель ставятся в центр разработки**.

Главная идея — структура приложения должна определяться **бизнес-понятиями, правилами и процессами**, а не устройством БД, ORM, API или других инфраструктурных деталей.

Домен содержит основную бизнес-логику и должен быть максимально независим от технического способа её выполнения и хранения данных. Инфраструктура обслуживает доменную модель, а не определяет её.

DDD особенно полезен для систем со сложной предметной областью, где важно:

- явно моделировать бизнес-понятия и инварианты
- изолировать бизнес-логику от инфраструктуры
- разделять большую предметную область на независимые модели
- использовать в коде тот же язык и понятия, которыми оперирует бизнес

DDD включает два уровня:

- Strategic DDD — определяет границы и отношения доменных моделей
- Tactical DDD — определяет способы построения Domain Model внутри этих границ

DDD **не является архитектурой приложения** вроде Clean или Hexagonal Architecture, но хорошо сочетается с ними: DDD определяет, **что находится в центре системы**, а архитектурные подходы помогают защитить этот центр от внешних технических деталей.

---

# 2. Strategic DDD

**Strategic DDD** — набор концепций для разбиения сложной предметной области на отдельные модели, определения их границ, языка и способов взаимодействия между ними.

### Domain и Subdomain

**Domain** — предметная область бизнеса целиком.

**Subdomain** — отдельная часть Domain со своими задачами и правилами.

Subdomain'ы делятся на:

- **Core Domain** — ключевая часть бизнеса, создающая основную ценность продукта
- **Supporting Subdomain** — необходимая вспомогательная бизнес-логика
- **Generic Subdomain** — типовая задача, которую часто можно решить готовым решением

### Ubiquitous Language

**Ubiquitous Language** — единый язык бизнеса и разработчиков, термины которого непосредственно отражаются в модели и коде.

```
бизнес: Order, Payment, Reservation
              ↓
Domain Model использует те же понятия
```

### Bounded Context

**Bounded Context** — явная граница, внутри которой существует конкретная Domain Model и термины имеют однозначный смысл.

Один термин в разных контекстах может представлять разные модели:

```
Catalog Context

Product:
• Name
• Description
• Images


Inventory Context

Product:
• SKU
• Quantity
• ReservedQuantity
```

Важно:

- `Subdomain` — часть бизнеса
- `Bounded Context` — граница модели, описывающей часть бизнеса

Один Subdomain часто соответствует одному Bounded Context, но это не обязательное соответствие.

### Context Map

**Context Map** — описание системы Bounded Context'ов и отношений между ними.

При рассмотрении связи между двумя Bounded Context:

`Upstream`:
- контекст, от которого зависит другой контекст
- предоставляет данные, API или события

`Downstream`:
- контекст, который зависит от Upstream
- использует предоставляемые им данные или возможности

### Способы взаимодействия Bounded Context'ов

- **Anti-Corruption Layer (ACL)** — downstream преобразует чужую модель в собственную, не позволяя ей проникнуть внутрь Domain Model
- **Published Language** — контексты взаимодействуют через явно определённый общий контракт или формат сообщений
- **Open Host Service** — upstream предоставляет стабильный API для использования другими контекстами
- **Conformist** — downstream принимает модель upstream практически как есть
- **Shared Kernel** — несколько контекстов сознательно разделяют небольшой общий фрагмент модели
- **Customer / Supplier** — downstream выступает заказчиком и может влиять на развитие upstream
- **Partnership** — два контекста тесно координируют развитие своих моделей
- **Separate Ways** — контексты не интегрируются и решают задачу независимо

---

# 3. Tactical DDD

**Tactical DDD** — набор паттернов для построения **Domain Model внутри Bounded Context**: как представить бизнес-сущности, их состояние, поведение, инварианты и взаимодействие.

```text
Bounded Context
└── Domain Model
    ├── Entity
    ├── Value Object
    ├── Aggregate / Aggregate Root
    ├── Domain Service
    ├── Domain Event
    ├── Factory
    ├── Repository
    └── Specification
```

### Entity

**Entity** — доменный объект, который определяется своей **идентичностью**, а не только значениями свойств. Его состояние может меняться, но это остаётся та же сущность.

```csharp
public class Order
{
    public OrderId Id { get; }
    public OrderStatus Status { get; private set; }
}
```

Два `Order` с одинаковыми данными, но разными `Id` — разные сущности.


### Value Object

**Value Object** — объект без собственной идентичности, определяемый исключительно своими значениями. Обычно immutable и сравнивается по содержимому.

```csharp
public readonly record struct Money(decimal Amount, Currency Currency);
```

```text
Money(100, RUB) == Money(100, RUB)
```

Value Object хорошо подходит для доменных понятий вроде `Money`, `Email`, `Address`, `Discount`, `OrderId`, если для них важны собственные правила и семантика.


### Invariant

**Invariant** — бизнес-правило, которое должно оставаться истинным при любом допустимом изменении Domain Model.

Domain Model должна сама защищать свои инварианты и не позволять перевести себя в недопустимое состояние.


### Aggregate и Aggregate Root

**Aggregate** — группа связанных Entity и Value Object, рассматриваемая как **единая граница согласованности**.

У каждого Aggregate есть одна корневая Entity — **Aggregate Root**.

```text
Order                     ← Aggregate Root
├── OrderItem              ← Entity
├── OrderItem
├── ShippingAddress        ← Value Object
└── Money                  ← Value Object
```

Внешний код работает с Aggregate через его Root:

```csharp
order.AddItem(productId, quantity);
order.Confirm();
```

а не напрямую изменяет внутренние объекты.

Главные правила Aggregate:

- Root контролирует изменение состояния и защищает инварианты всего Aggregate
	
- Один Aggregate обычно сохраняется **атомарно в одной транзакции**
	  
- Другие Aggregate обычно ссылаются на него **по идентификатору**, а не держат прямую объектную связь
	  
- Aggregate стоит делать как можно меньше: объединять объекты следует по требованиям консистентности, а не просто потому, что между таблицами есть FK


### Domain Service

**Domain Service** — бизнес-логика, которая относится к Domain, но естественно не принадлежит одной конкретной Entity или Value Object.

```csharp
public class MoneyTransferService
{
    public void Transfer(Account from, Account to, Money amount)
    {
        from.Withdraw(amount);
        to.Deposit(amount);
    }
}
```

Domain Service работает **в терминах Domain Model** и не должен содержать техническую инфраструктурную логику вроде `DbContext`, HTTP или Kafka.

Если правило естественно принадлежит Entity — его лучше оставить в Entity, а не выносить в Domain Service.


### Domain Event

**Domain Event** — факт о значимом событии, которое **уже произошло внутри Domain**.

```csharp
public record OrderConfirmed(OrderId OrderId);
```

Domain Event описывает бизнес-факт, а не способ его доставки.


### Repository

**Repository** — абстракция доступа к хранилищу, предоставляющая работу с Domain Model как с коллекцией объектов.

В DDD Repository обычно создаётся **для Aggregate Root**:

```csharp
public interface IOrderRepository
{
    Task<Order?> GetAsync(OrderId id);
    void Add(Order order);
}
```

Repository возвращает и сохраняет **Aggregate**, а детали ORM, SQL и структуры БД остаются за пределами Domain Model.


### Factory

**Factory** — объект или метод, отвечающий за создание сложного Domain Object или Aggregate в корректном начальном состоянии.

```csharp
var order = Order.Create(customerId);
```

или:

```csharp
var order = orderFactory.Create(customer, cart);
```

Factory нужна, когда создание объекта само содержит заметную доменную логику. 


### Specification

**Specification** — объект, инкапсулирующий отдельное бизнес-условие или правило, которое можно переиспользовать и комбинировать.

```csharp
public class PremiumCustomerSpecification
{
    public bool IsSatisfiedBy(Customer customer)
        => customer.TotalSpent >= 100_000;
}
```

Концептуально:

Specification — "удовлетворяет ли объект этому бизнес-условию?"

Полезна, когда правило достаточно сложное, повторяется в нескольких местах или должно комбинироваться с другими правилами.

---

# 4. Anemic Domain Model и Rich Domain Model

### Anemic Domain Model

Модель, в которой доменные объекты в основном содержат **данные**, а бизнес-правила и изменение их состояния находятся во внешних сервисах.

Например, `Order` фактически является контейнером данных:

```csharp
public class Order
{
    public Guid Id { get; set; }
    public OrderStatus Status { get; set; }
    public List<OrderItem> Items { get; set; } = [];
}
```

А бизнес-логика находится в Application Service:

```csharp
public async Task ConfirmOrder(Guid orderId)
{
    var order = await repository.GetAsync(orderId);

    if (order.Items.Count == 0)
        throw new DomainException("Empty order");

    if (order.Status != OrderStatus.Created)
        throw new DomainException("Order cannot be confirmed");

    order.Status = OrderStatus.Confirmed;

    await unitOfWork.SaveChangesAsync();
}
```

Получается:

```text
Order
→ хранит состояние

OrderService
→ знает бизнес-правила
→ проверяет invariants
→ напрямую изменяет состояние Order
```

Основные проблемы:

- **инварианты находятся вне объекта**, состояние которого они должны защищать;
- объект можно легко перевести в недопустимое состояние:

```csharp
order.Status = OrderStatus.Confirmed;
```

- одна и та же бизнес-логика начинает дублироваться в разных use cases;
- Application Layer постепенно превращается в место хранения всей бизнес-логики;
- Domain Model плохо отражает поведение реального бизнеса — в ней есть существительные, но почти нет бизнес-операций.

В контексте **Domain Model / DDD** Мартин Фаулер называет такой подход антипаттерном. При этом для простого CRUD отсутствие богатой доменной модели само по себе не является проблемой.

---

### Rich Domain Model

**Rich Domain Model** — модель, в которой **бизнес-поведение и защита инвариантов находятся внутри самой Domain Model**.

Отрефакторим тот же `Order`:

```csharp
public class Order
{
    private readonly List<OrderItem> _items = [];

    public Guid Id { get; }
    public OrderStatus Status { get; private set; }

    public IReadOnlyCollection<OrderItem> Items => _items;

    public void Confirm()
    {
        if (_items.Count == 0)
            throw new DomainException("Empty order");

        if (Status != OrderStatus.Created)
            throw new DomainException("Order cannot be confirmed");

        Status = OrderStatus.Confirmed;
    }
}
```

Теперь Application Service только организует use case:

```csharp
public async Task ConfirmOrder(Guid orderId)
{
    var order = await repository.GetAsync(orderId);

    order.Confirm();

    await unitOfWork.SaveChangesAsync();
}
```


Это важная идея DDD: **объект не просто хранит данные о бизнесе — он моделирует его поведение**.

За счёт этого:

- недопустимое состояние сложнее создать
- бизнес-правило имеет одно естественное место
- уменьшается дублирование логики между use cases
- Domain Model становится выразительной и отражает **Ubiquitous Language**
- Application Layer остаётся оркестратором, а не владельцем бизнес-логики
- Domain Model проще тестировать изолированно от БД, HTTP и инфраструктуры

При этом **Rich Domain Model не означает, что абсолютно вся логика должна находиться в Entity**. Если бизнес-операция не принадлежит естественно одному объекту, она может находиться в `Domain Service`.

---

## 5. Границы Domain и остального приложения

DDD стремится сделать **Domain Model независимой от технических деталей приложения**. Бизнес-модель не должна определяться HTTP, ORM, БД, брокером сообщений или конкретным фреймворком.

### Domain Model

**Domain Model** содержит бизнес-понятия, состояние, поведение и инварианты предметной области:

```text
Entities
Value Objects
Aggregates
Domain Services
Domain Events
Repository abstractions
```

Domain не должен знать про:

- `DbContext`
- SQL и структуру таблиц
- HTTP
- Kafka / RabbitMQ
- ASP.NET Core
- конкретные внешние API

### Application / Use Cases

**Application Layer** реализует сценарии использования системы и оркестрирует Domain Model.

Application может зависеть от абстракций внешних операций:

```text
IOrderRepository
IPaymentGateway
IEmailSender
```


### Infrastructure

**Infrastructure** содержит реализацию технических механизмов:

```text
EF Core
PostgreSQL
Dapper
Kafka
HTTP clients
File System
SMTP
```


### Repository: interface и implementation

Repository в DDD работает с **Aggregate Root**, а не с таблицами:

```csharp
public interface IOrderRepository
{
    Task<Order?> GetAsync(OrderId id);
    void Add(Order order);
}
```


- `IOrderRepository` — контракт работы с `Order`
- `EfOrderRepository` — конкретный способ хранения `Order`

Абстракция Repository находится на внутренней стороне архитектурной границы, а реализация — в Infrastructure.

Точное размещение интерфейса зависит от выбранной архитектуры:

- DDD — Repository может рассматриваться как часть Domain Model
- Clean / Onion — output port часто размещается в Application


### DTO не являются Domain Model

**DTO** предназначены для передачи данных через границы системы или между архитектурными компонентами.

```text
HTTP Request
   ↓
Request DTO
   ↓
Application
   ↓
Domain Model
```

На выходе:

```text
Domain / Use Case result
   ↓
Response DTO
   ↓
HTTP Response
```

DTO не должны заменять Domain Model:

- `OrderDto` — транспорт данных
- `Order` — бизнес-поведение + invariants

Поэтому Domain Entity не стоит одновременно делать HTTP-контрактом, Kafka-сообщением и моделью БД.


### Persistence Ignorance

**Persistence Ignorance** — принцип, согласно которому Domain Model не должна знать, **как и где она хранится**.

```csharp
order.Confirm();
```

Domain работает в терминах бизнеса и не делает:

```csharp
order.Save();
dbContext.Update(order);
connection.Execute(...);
```

Механизм хранения находится снаружи

Это позволяет менять способ хранения, ORM или структуру БД без проникновения этих деталей в бизнес-модель.
