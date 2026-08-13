
**`yield return`** используется для создания ленивого итератора. Метод с `yield return` не формирует коллекцию целиком, а возвращает элементы по одному во время перечисления

```csharp
public static IEnumerable<int> GetNumbers()
{
    yield return 10;
    yield return 20;
}
```

Вызов метода обычно не выполняет его тело. Выполнение начинается при перечислении.

Компилятор преобразует метод в скрытую **машину состояний**, реализующую:

```cs
IEnumerable<T>
IEnumerator<T>
```

Упрощённо исходный метод превращается в создание объекта итератора:

```csharp
public static IEnumerable<int> GetNumbers()
{
    return new GetNumbersIterator();
}
```

А сгенерированный итератор концептуально выглядит так:

```csharp
private sealed class GetNumbersIterator :
    IEnumerable<int>,
    IEnumerator<int>
{
    private int _state;
    private int _current;

    public int Current => _current;

    object IEnumerator.Current => Current;

    public bool MoveNext()
    {
        switch (_state)
        {
            case 0:
                _current = 10;
                _state = 1;
                return true;

            case 1:
                _current = 20;
                _state = 2;
                return true;

            default:
                return false;
        }
    }

    public IEnumerator<int> GetEnumerator() => new GetNumbersIterator();

    IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();

    public void Dispose()
    { 
    }

    public void Reset() => throw new NotSupportedException();
}
```

Каждый `yield return`:

- записывает значение в Current
- запоминает позицию выполнения
- возвращает true из MoveNext()

Следующий вызов `MoveNext()` продолжает выполнение после предыдущего `yield return`

Когда метод заканчивается или выполняется `yield break`, `MoveNext()` возвращает `false`

## Итератор с циклом

```csharp
public static IEnumerable<int> Count(int max)
{
    for (var i = 0; i < max; i++)
        yield return i;
}
```

Переменные, которые должны сохраняться между вызовами `MoveNext()`, становятся полями машины состояний:

```csharp
private int _max;
private int _i;
private int _state;
private int _current;
```

Упрощённая логика `MoveNext()`:

```csharp
public bool MoveNext()
{
    switch (_state)
    {
        case 0:
            _i = 0;
            break;

        case 1:
            _i++;
            break;

        default:
            return false;
    }

    if (_i < _max)
    {
        _current = _i;
        _state = 1;
        return true;
    }

    return false;
}
```

## Отложенное выполнение

```csharp
public static IEnumerable<int> GetNumbers()
{
    Console.WriteLine("Start");

    yield return 1;

    Console.WriteLine("Continue");

    yield return 2;
}
```

```csharp
var numbers = GetNumbers();
```

Здесь ничего не выводится

При первом `MoveNext()`:

```text
Start
```

При втором:

```text
Continue
```

Поэтому исключения внутри итератора тоже обычно возникают **во время перечисления**, а не при вызове метода

## Как работает `foreach`

```csharp
foreach (var number in numbers)
{
    Console.WriteLine(number);
}
```

Концептуально разворачивается в:

```csharp
using var enumerator = numbers.GetEnumerator();

while (enumerator.MoveNext())
{
    var number = enumerator.Current;
    Console.WriteLine(number);
}
```

## `yield break`

`yield break` досрочно завершает перечисление:

```csharp
public static IEnumerable<int> CountUntilNegative(IEnumerable<int> values)
{
    foreach (var value in values)
    {
        if (value < 0)
            yield break;

        yield return value;
    }
}
```

