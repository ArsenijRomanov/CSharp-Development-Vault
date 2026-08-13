**`record class`** — ссылочный тип (`class`) с автоматически генерируемой **record-семантикой**. Компилятор добавляет value-based equality и ряд удобных операций для data/value-like объектов.

```cs
public record User(string Name, int Age);
```

Компилятор автоматически генерирует:

- `IEquatable<T>`
- strongly typed `Equals(T)`
- `Equals(object)`
- `GetHashCode()`
- операторы `==` и `!=`
- `ToString()`
- `Deconstruct()`
- поддержку `with`

Сравнение выполняется по значениям компонентов:

```cs
var a = new User("Alex", 30);
var b = new User("Alex", 30);

a == b; // true
```

Для positional `record class` компилятор также создаёт свойства с `init`:

```cs
public record User(string Name, int Age);
```

Концептуально:

```cs
public record User
{
    public string Name { get; init; }
    public int Age { get; init; }
}
```

Поэтому свойства можно задавать при создании объекта, но нельзя менять обычным присваиванием после инициализации:

```cs
var user = new User("Alex", 30);

// user.Age = 31; // нельзя
```

`with` создаёт новый экземпляр с изменёнными значениями:

```cs
var updated = user with { Age = 31 };
```

`record class` может быть и mutable, если свойства объявлены через `set` вручную:

```cs
public record User
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```


```
class
+ IEquatable<T>
+ strongly typed Equals(T)
+ value equality
+ == / !=
+ GetHashCode
+ ToString
+ Deconstruct
+ with
+ init для positional properties
+ inheritance
= record class
```