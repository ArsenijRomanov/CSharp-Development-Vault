
**Repository** — паттерн доступа к данным, который скрывает детали хранения объектов и предоставляет приложению интерфейс работы с ними как с коллекцией.

```cs
public interface IUserRepository
{
    Task<User?> GetByIdAsync(UserId id);
    void Add(User user);
    void Remove(User user);
}
```

Код приложения работает только с абстракцией:

~~~mermaid
%%{init: {"flowchart": {"useMaxWidth": true, "nodeSpacing": 8, "rankSpacing": 14}, "themeVariables": {"fontSize": "11px"}}}%%
flowchart TD
    A[Application / Domain]
    A --> B[IUserRepository]
    B --> C[Repository implementation]
    C --> D[EF Core / SQL / Database]
~~~

Repository позволяет вынести из бизнес-логики детали запросов, ORM и конкретного источника данных.