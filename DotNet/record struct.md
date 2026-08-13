**`record struct`** — значимый тип (`struct`) с автоматически генерируемой **record-семантикой**. Он сохраняет value semantics обычной структуры, но компилятор добавляет готовую реализацию сравнения и ряд удобных операций для value objects.

```cs
public readonly record struct Point(int X, int Y);
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
var a = new Point(10, 20);
var b = new Point(10, 20);

a == b; // true
```

В отличие от обычного `struct`, для которого без собственной реализации equality может использоваться универсальная логика `ValueType.Equals`, `record struct` уже имеет сгенерированный `Equals(T)`:

```cs
public bool Equals(Point other)
    => EqualityComparer<int>.Default.Equals(X, other.X)
    && EqualityComparer<int>.Default.Equals(Y, other.Y);
```

То есть `record struct` из коробки получает эффективное типизированное сравнение без необходимости вручную реализовывать `IEquatable<T>`.

При этом он остаётся **value type**.

`with` создаёт изменённую копию:

```cs
var b = a with { X = 30 };
```

Обычный `record struct` mutable:

```cs
public record struct Point(int X, int Y);

var point = new Point(1, 2);
point.X = 10;
```

Для value objects обычно предпочтительнее `readonly record struct`:

```cs
public readonly record struct Money(
    decimal Amount,
    string Currency);
```

`record struct` особенно удобен для небольших типов, которые представляют одно логическое значение, должны иметь value semantics и сравниваться по своему содержимому.

```
struct
+ IEquatable<T>
+ strongly typed Equals(T)
+ value equality
+ == / !=
+ GetHashCode
+ ToString
+ Deconstruct
+ with
= record struct
```