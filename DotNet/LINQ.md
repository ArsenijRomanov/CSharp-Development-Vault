### 1. Фильтрация и проверка типа [[#1. Фильтрация и проверка типа|↗]]

- `Where` — фильтрует элементы по условию [[#1.1. `Where`|↗]]
- `OfType` — оставляет элементы указанного типа [[#2.2. `OfType<TResult>`|↗]]
- `Cast` — приводит все элементы к указанному типу [[#2.3. `Cast<TResult>`|↗]]

### 2. Проекция [[#2. Проекция|↗]]

- `Select` — преобразует каждый элемент [[#2.1. `Select`|↗]]
- `SelectMany` — преобразует элементы в последовательности и разворачивает их в одну [[#2.2. `SelectMany`|↗]]
- `Index` — добавляет к каждому элементу его индекс [[#2.3. `Index`|↗]]

### 3. Разбиение последовательности [[#3. Разбиение последовательности|↗]]

- `Take` — берёт первые элементы или указанный диапазон [[#3.1. `Take`|↗]]
- `TakeWhile` — берёт элементы, пока выполняется условие [[#3.2. `TakeWhile`|↗]]
- `TakeLast` — берёт последние элементы [[#3.3. `TakeLast`|↗]]
- `Skip` — пропускает первые элементы [[#3.4. `Skip`|↗]]
- `SkipWhile` — пропускает элементы, пока выполняется условие [[#3.5. `SkipWhile`|↗]]
- `SkipLast` — пропускает последние элементы [[#3.6. `SkipLast`|↗]]
- `Chunk` — разбивает последовательность на массивы заданного размера [[#3.7. `Chunk`|↗]]

### 4. Сортировка [[#4. Сортировка|↗]]

- `Order` — сортирует элементы по возрастанию [[#4.1. `Order`|↗]]
- `OrderDescending` — сортирует элементы по убыванию [[#4.2. `OrderDescending`|↗]]
- `OrderBy` — сортирует по ключу по возрастанию [[#4.3. `OrderBy`|↗]]
- `OrderByDescending` — сортирует по ключу по убыванию [[#4.4. `OrderByDescending`|↗]]
- `ThenBy` — добавляет последующую сортировку по возрастанию [[#4.5. `ThenBy`|↗]]
- `ThenByDescending` — добавляет последующую сортировку по убыванию [[#4.6. `ThenByDescending`|↗]]
- `Reverse` — разворачивает порядок элементов [[#4.7. `Reverse`|↗]]
- `Shuffle` — перемешивает элементы [[#4.8. `Shuffle`|↗]]

### 5. Операции над множествами [[#5. Операции над множествами|↗]]

- `Distinct` — удаляет дубликаты [[#5.1. `Distinct`|↗]]
- `DistinctBy` — удаляет дубликаты по ключу [[#5.2. `DistinctBy`|↗]]
- `Union` — объединяет две последовательности без дубликатов [[#5.3. `Union`|↗]]
- `UnionBy` — объединяет последовательности без дубликатов по ключу [[#5.4. `UnionBy`|↗]]
- `Intersect` — возвращает общие элементы двух последовательностей [[#5.5. `Intersect`|↗]]
- `IntersectBy` — возвращает общие элементы по ключу [[#5.6. `IntersectBy`|↗]]
- `Except` — возвращает элементы первой последовательности, отсутствующие во второй [[#5.7. `Except`|↗]]
- `ExceptBy` — вычисляет разность последовательностей по ключу [[#5.8. `ExceptBy`|↗]]

### 6. Объединение последовательностей [[#6. Объединение последовательностей|↗]]

- `Concat` — последовательно соединяет две последовательности [[#6.1. `Concat`|↗]]
- `Append` — добавляет элемент в конец [[#6.2. `Append`|↗]]
- `Prepend` — добавляет элемент в начало [[#6.3. `Prepend`|↗]]
- `Zip` — объединяет элементы последовательностей по одинаковым позициям [[#6.4. `Zip`|↗]]

### 7. Соединение по ключу [[#7. Соединение по ключу|↗]]

- `Join` — выполняет внутреннее соединение [[#7.1. `Join`|↗]]
- `GroupJoin` — соединяет последовательности с группировкой совпадений [[#7.2. `GroupJoin`|↗]]
- `LeftJoin` — выполняет левое внешнее соединение [[#7.3. `LeftJoin`|↗]]
- `RightJoin` — выполняет правое внешнее соединение [[#7.4. `RightJoin`|↗]]

### 8. Группировка [[#8. Группировка|↗]]

- `GroupBy` — группирует элементы по ключу [[#8.1. `GroupBy`|↗]]
- `ToLookup` — создаёт индексированную по ключу группировку [[#8.2. `ToLookup`|↗]]

### 9. Получение элемента [[#9. Получение элемента|↗]]

- `First` — возвращает первый элемент [[#9.3. `First`|↗]]
- `FirstOrDefault` — возвращает первый элемент или значение по умолчанию [[#9.4. `FirstOrDefault`|↗]]
- `Last` — возвращает последний элемент [[#9.5. `Last`|↗]]
- `LastOrDefault` — возвращает последний элемент или значение по умолчанию [[#9.6. `LastOrDefault`|↗]]
- `Single` — возвращает единственный элемент [[#9.7. `Single`|↗]]
- `SingleOrDefault` — возвращает единственный элемент или значение по умолчанию [[#9.8. `SingleOrDefault`|↗]]
- `ElementAt` — возвращает элемент по индексу [[#9.1. `ElementAt`|↗]]
- `ElementAtOrDefault` — возвращает элемент по индексу или значение по умолчанию [[#9.2. `ElementAtOrDefault`|↗]]
- `DefaultIfEmpty` — возвращает исходную последовательность или один элемент по умолчанию [[#9.9. `DefaultIfEmpty`|↗]]

### 10. Проверка последовательности [[#10. Проверка последовательности|↗]]

- `Any` — проверяет наличие элементов или совпадений [[#10.1. `Any`|↗]]
- `All` — проверяет соответствие всех элементов условию [[#10.2. `All`|↗]]
- `Contains` — проверяет наличие конкретного элемента [[#10.3. `Contains`|↗]]
- `SequenceEqual` — сравнивает две последовательности поэлементно [[#10.4. `SequenceEqual`|↗]]

### 11. Подсчёт и агрегирование [[#11. Подсчёт и агрегирование|↗]]

- `Count` — возвращает количество элементов как `int` [[#11.1. `Count`|↗]]
- `LongCount` — возвращает количество элементов как `long` [[#11.2. `LongCount`|↗]]
- `CountBy` — подсчитывает элементы по ключам [[#11.4. `CountBy`|↗]]
- `Sum` — вычисляет сумму [[#11.5. `Sum`|↗]]
- `Average` — вычисляет среднее значение [[#11.6. `Average`|↗]]
- `Min` — возвращает минимальное значение [[#11.7. `Min` и `Max`|↗]]
- `MinBy` — возвращает элемент с минимальным ключом [[#11.8. `MinBy` и `MaxBy`|↗]]
- `Max` — возвращает максимальное значение [[#11.7. `Min` и `Max`|↗]]
- `MaxBy` — возвращает элемент с максимальным ключом [[#11.8. `MinBy` и `MaxBy`|↗]]
- `Aggregate` — сворачивает последовательность в одно значение [[#11.9. `Aggregate`|↗]]
- `AggregateBy` — агрегирует элементы отдельно для каждого ключа [[#11.10. `AggregateBy`|↗]]

### 12. Материализация и преобразование [[#12. Материализация и преобразование|↗]]

- `ToArray` — создаёт массив [[#12.1. `ToArray`|↗]]
- `ToList` — создаёт список [[#12.2. `ToList`|↗]]
- `ToDictionary` — создаёт словарь [[#12.3. `ToDictionary`|↗]]
- `ToHashSet` — создаёт множество [[#12.4. `ToHashSet`|↗]]
- `AsEnumerable` — представляет объект как `IEnumerable<T>` [[#12.5. `AsEnumerable`|↗]]

### 13. Генераторы последовательностей [[#13. Генераторы последовательностей|↗]]

- `Empty` — создаёт пустую последовательность [[#13.1. `Empty`|↗]]
- `Range` — создаёт диапазон целых чисел [[#13.2. `Range`|↗]]
- `Repeat` — создаёт последовательность повторяющихся значений [[#13.3. `Repeat`|↗]]
- `Sequence` — создаёт числовую последовательность с заданным шагом [[#13.4. `Sequence`|↗]]
- `InfiniteSequence` — создаёт бесконечную последовательность с заданным шагом [[#13.5. `InfiniteSequence`|↗]]

---

## 1. Фильтрация и проверка типа

### 1.1. `Where`

Фильтрует последовательность по условию. Тип элементов не изменяется. Выполнение отложенное

```cs
IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

С индексом элемента в предикате:
```cs
IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, int, bool> predicate)
```

##### Примеры:

```cs
int[] numbers = [1, 2, 3, 4, 5];

IEnumerable<int> evenNumbers =
    numbers.Where(number => number % 2 == 0);

// Результат: 2, 4
```

```cs
string[] names = ["Tom", "Bob", "Alice", "Sam"];

IEnumerable<string> result =
    names.Where((name, index) => index % 2 == 0);

// Результат: Tom, Alice
```


### 2.2. `OfType<TResult>`

Возвращает только элементы, фактический тип которых совместим с `TResult`. Несовместимые элементы пропускаются. Возвращает `IEnumerable<TResult>`. Выполнение отложенное

```cs
IEnumerable<TResult> OfType<TResult>(
    this IEnumerable source)
```

```cs
object[] values = [10, "text", 20, 3.5];

IEnumerable<int> numbers = values.OfType<int>();

// Результат: 10, 20
```

Метод учитывает наследование и реализацию интерфейсов


### 2.3. `Cast<TResult>`

Приводит каждый элемент последовательности к типу `TResult` и возвращает `IEnumerable<TResult>`. Выполнение отложенное

```cs
IEnumerable<TResult> Cast<TResult>(
    this IEnumerable source)
```

```cs
object[] values = [10, 20, 30];

IEnumerable<int> numbers = values.Cast<int>();

// Результат: 10, 20, 30
```

Если хотя бы один элемент нельзя привести к `TResult`, во время перечисления возникает `InvalidCastException`

```cs
object[] values = [10, "text", 20];

IEnumerable<int> numbers = values.Cast<int>();

// 10, затем InvalidCastException на элементе "text"
```

---

## 2. Проекция

Методы проекции преобразуют элементы исходной последовательности в другую форму. Исходная последовательность не изменяется

### 2.1. `Select`

Преобразует каждый элемент исходной последовательности с помощью функции `selector`. Для каждого исходного элемента создаётся ровно один результирующий элемент

Возвращает `IEnumerable<TResult>`. Тип элемента может измениться с `TSource` на `TResult`. Выполнение отложенное.

Перегрузки:

```cs
IEnumerable<TResult> Select<TSource, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, TResult> selector)
```

С индексом элемента:
```cs
IEnumerable<TResult> Select<TSource, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, int, TResult> selector)
```

Примеры:

```cs
int[] numbers = [1, 2, 3];

IEnumerable<string> result =
    numbers.Select(number => $"Число: {number}");

// Результат: "Число: 1", "Число: 2", "Число: 3"
```

```cs
string[] names = ["Tom", "Bob"];

IEnumerable<string> result =
    names.Select((name, index) => $"{index}: {name}");

// Результат: "0: Tom", "1: Bob"
```

### 2.2. `SelectMany`

Преобразует каждый элемент исходной последовательности во вложенную последовательность, после чего объединяет все вложенные последовательности в одну плоскую последовательность

Возвращает `IEnumerable<TResult>`. Выполнение отложенное.

Перегрузки без отдельного формирования результата:

```cs
IEnumerable<TResult> SelectMany<TSource, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, IEnumerable<TResult>> selector)
```

С индексом:
```cs
IEnumerable<TResult> SelectMany<TSource, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, int, IEnumerable<TResult>> selector)
```

Перегрузки с `resultSelector`, который формирует результирующий элемент из исходного элемента и элемента вложенной последовательности:

```cs
IEnumerable<TResult> SelectMany<TSource, TCollection, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, IEnumerable<TCollection>> collectionSelector,
    Func<TSource, TCollection, TResult> resultSelector)
```

```cs
IEnumerable<TResult> SelectMany<TSource, TCollection, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, int, IEnumerable<TCollection>> collectionSelector,
    Func<TSource, TCollection, TResult> resultSelector)
```

Разворачивание вложенных последовательностей:

```cs
string[] words = ["ab", "cd"];

IEnumerable<char> characters =
    words.SelectMany(word => word);

// Результат: 'a', 'b', 'c', 'd'
```

Использование индекса исходного элемента:

```cs
string[] words = ["ab", "cd"];

IEnumerable<string> result =
    words.SelectMany(
        (word, index) => word.Select(character => $"{index}:{character}"));

// Результат: "0:a", "0:b", "1:c", "1:d"
```

Формирование результата из элементов двух последовательностей:

```cs
string[] courses = ["C#", "Java"];
string[] students = ["Tom", "Bob"];

var enrollments = courses.SelectMany(
    course => students,
    (course, student) => new
    {
        Student = student,
        Course = course
    });

// Результат:
// Tom — C#
// Bob — C#
// Tom — Java
// Bob — Java
```

### 2.3. `Index`

Добавляет к каждому элементу его индекс, начиная с нуля

Возвращает `IEnumerable<(int Index, TSource Item)>`. Элемент результирующей последовательности является кортежем `ValueTuple<int, TSource>`. Выполнение отложенное.

Сигнатура:

```cs
IEnumerable<(int Index, TSource Item)> Index<TSource>(
    this IEnumerable<TSource> source)
```

```cs
string[] names = ["Tom", "Bob", "Alice"];

IEnumerable<(int Index, string Item)> indexedNames =
    names.Index();

// Результат:
// (0, "Tom")
// (1, "Bob")
// (2, "Alice")
```

Элементы кортежа доступны по именам `Index` и `Item`:

```cs
foreach (var entry in names.Index())
{
    Console.WriteLine($"{entry.Index}: {entry.Item}");
}

// 0: Tom
// 1: Bob
// 2: Alice
```

---

## 3. Разбиение последовательности

Методы разбиения возвращают определённую часть исходной последовательности или разделяют её на несколько последовательностей. 

### 3.1. `Take`

Возвращает первые `count` элементов либо элементы, индексы которых входят в заданный диапазон. Возвращает `IEnumerable<TSource>`. Выполнение отложенное. Конечная граница диапазона не включается.

Перегрузки:

```cs
IEnumerable<TSource> Take<TSource>(
    this IEnumerable<TSource> source,
    int count)
```

```cs
IEnumerable<TSource> Take<TSource>(
    this IEnumerable<TSource> source,
    Range range)
```

Получение первых элементов:

```cs
int[] numbers = [1, 2, 3, 4, 5];

IEnumerable<int> result = numbers.Take(3);

// Результат: 1, 2, 3
```

Получение диапазона:

```cs
int[] numbers = [1, 2, 3, 4, 5];

IEnumerable<int> result = numbers.Take(1..4);

// Результат: 2, 3, 4
```

Индексы могут отсчитываться от конца с помощью `^`:

```cs
IEnumerable<int> result = numbers.Take(^3..);

// Результат: 3, 4, 5
```

`Take(count)` является потоковым методом и прекращает перечисление источника после получения необходимого количества элементов. При `count <= 0` возвращается пустая последовательность. `Take(range)` с индексами от конца для произвольного `IEnumerable<T>` может потребовать определения длины или буферизации части источника.


### 3.2. `TakeWhile`

Возвращает элементы с начала последовательности, пока предикат возвращает `true`. На первом элементе, не прошедшем проверку, перечисление прекращается окончательно. Возвращает `IEnumerable<TSource>`. Выполнение отложенное и потоковое.

Перегрузки:

```cs
IEnumerable<TSource> TakeWhile<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

С индексом:
```cs
IEnumerable<TSource> TakeWhile<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, int, bool> predicate)
```

Примеры:

```cs
int[] numbers = [2, 4, 1, 6, 8];

IEnumerable<int> result =
    numbers.TakeWhile(number => number % 2 == 0);

// Результат: 2, 4
```

```cs
string[] names = ["Tom", "Bob", "Alice", "Sam"];

IEnumerable<string> result =
    names.TakeWhile((name, index) => index < 2);

// Результат: Tom, Bob
```


### 3.3. `TakeLast`

Возвращает последние `count` элементов последовательности. Возвращает `IEnumerable<TSource>`. Выполнение отложенное.

```cs
IEnumerable<TSource> TakeLast<TSource>(
    this IEnumerable<TSource> source,
    int count)
```

```cs
int[] numbers = [1, 2, 3, 4, 5];

IEnumerable<int> result = numbers.TakeLast(2);

// Результат: 4, 5
```

Для произвольного `IEnumerable<T>` метод должен дойти до конца источника, прежде чем сможет определить и вернуть последние элементы. Для хранения последних `count` элементов используется внутренний буфер. При `count <= 0` возвращается пустая последовательность.


### 3.4. `Skip`

Пропускает первые `count` элементов и возвращает оставшуюся часть последовательности. Возвращает `IEnumerable<TSource>`. Выполнение отложенное и потоковое.

```cs
IEnumerable<TSource> Skip<TSource>(
    this IEnumerable<TSource> source,
    int count)
```

```cs
int[] numbers = [1, 2, 3, 4, 5];

IEnumerable<int> result = numbers.Skip(2);

// Результат: 3, 4, 5
```

Если `count` больше длины источника, результат будет пустым. При `count <= 0` элементы не пропускаются


### 3.5. `SkipWhile`

Пропускает элементы с начала последовательности, пока предикат возвращает `true`. Первый элемент, для которого предикат вернул `false`, и все последующие элементы возвращаются без дальнейших проверок предиката. Возвращает `IEnumerable<TSource>`. Выполнение отложенное и потоковое.

Перегрузки:

```cs
IEnumerable<TSource> SkipWhile<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

С индексом:
```cs
IEnumerable<TSource> SkipWhile<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, int, bool> predicate)
```

Примеры:

```cs
int[] numbers = [2, 4, 1, 6, 8];

IEnumerable<int> result =
    numbers.SkipWhile(number => number % 2 == 0);

// Результат: 1, 6, 8
```

```cs
string[] names = ["Tom", "Bob", "Alice", "Sam"];

IEnumerable<string> result =
    names.SkipWhile((name, index) => index < 2);

// Результат: Alice, Sam
```


### 3.6. `SkipLast`

Возвращает последовательность без последних `count` элементов. Возвращает `IEnumerable<TSource>`. Выполнение отложенное.

```cs
IEnumerable<TSource> SkipLast<TSource>(
    this IEnumerable<TSource> source,
    int count)
```

```cs
int[] numbers = [1, 2, 3, 4, 5];

IEnumerable<int> result = numbers.SkipLast(2);

// Результат: 1, 2, 3
```

Метод хранит во внутреннем буфере последние `count` элементов. Когда становится известно, что элемент уже не входит в последние `count`, он возвращается наружу. Поэтому результат выдаётся потоково, но с задержкой на размер буфера

При `count <= 0` возвращается последовательность, эквивалентная исходной.


### 3.7. `Chunk`

Разбивает последовательность на массивы размером не более `size`. Возвращает `IEnumerable<TSource[]>`. Выполнение отложенное. Каждый элемент результирующей последовательности имеет тип `TSource[]`.

```cs
IEnumerable<TSource[]> Chunk<TSource>(
    this IEnumerable<TSource> source,
    int size)
```

```cs
int[] numbers = [1, 2, 3, 4, 5];

IEnumerable<int[]> chunks = numbers.Chunk(2);

// Результат:
// [1, 2]
// [3, 4]
// [5]
```

Все массивы, кроме последнего, имеют размер `size`. Последний массив может быть короче. При `size < 1` выбрасывается `ArgumentOutOfRangeException`.

---

## 4. Сортировка

Методы сортировки не изменяют исходную последовательность. Вызов выполняется отложенно, но при начале перечисления создается буфер. Сортировка не является потоковой.

`Order`, `OrderDescending`, `OrderBy`, `OrderByDescending`, `ThenBy` и `ThenByDescending` возвращают `IOrderedEnumerable<T>`. Этот интерфейс дополнительно позволяет добавлять последующие критерии сортировки через `ThenBy`. 

Сортировка по ключам является стабильной.

### 4.1. `Order`

Сортирует последовательность по значениям самих элементов в порядке возрастания

Возвращает `IOrderedEnumerable<TSource>`. 

Перегрузки:

```cs
IOrderedEnumerable<TSource> Order<TSource>(
    this IEnumerable<TSource> source)
```

```cs
IOrderedEnumerable<TSource> Order<TSource>(
    this IEnumerable<TSource> source,
    IComparer<TSource>? comparer)
```

Без явного компаратора используется `Comparer<TSource>.Default`.

```cs
int[] numbers = [4, 1, 3, 2];

IOrderedEnumerable<int> result = numbers.Order();

// Результат: 1, 2, 3, 4
```

С компаратором:

```cs
string[] names = ["bob", "Alice", "tom"];

IOrderedEnumerable<string> result =
    names.Order(StringComparer.OrdinalIgnoreCase);

// Результат: Alice, bob, tom
```


### 4.2. `OrderDescending`

Аналогично в порядке убывания.


### 4.3. `OrderBy`

Сортирует элементы в порядке возрастания по ключу, который возвращает `keySelector`

Возвращает `IOrderedEnumerable<TSource>`. Тип элементов последовательности не изменяется. Выполнение отложенное, с полной буферизацией источника

Перегрузки:

```cs
IOrderedEnumerable<TSource> OrderBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector)
```

```cs
IOrderedEnumerable<TSource> OrderBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IComparer<TKey>? comparer)
```

Примеры:

```cs
string[] names = ["Alice", "Tom", "Robert"];

IOrderedEnumerable<string> result =
    names.OrderBy(name => name.Length);

// Результат: Tom, Alice, Robert
```


### 4.4. `OrderByDescending`

Сортирует элементы в порядке убывания по ключу, который возвращает `keySelector`


### 4.5. `ThenBy`

Добавляет последующий критерий сортировки по возрастанию. Применяется только к `IOrderedEnumerable<TSource>`

Новый критерий используется только внутри групп элементов, у которых равны все предыдущие ключи

Возвращает `IOrderedEnumerable<TSource>`. Выполнение отложенное

Перегрузки:

```cs
IOrderedEnumerable<TSource> ThenBy<TSource, TKey>(
    this IOrderedEnumerable<TSource> source,
    Func<TSource, TKey> keySelector)
```

```cs
IOrderedEnumerable<TSource> ThenBy<TSource, TKey>(
    this IOrderedEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IComparer<TKey>? comparer)
```

```cs
var users = new[]
{
    new { Name = "Tom", Age = 30 },
    new { Name = "Bob", Age = 20 },
    new { Name = "Alice", Age = 20 }
};

IOrderedEnumerable<dynamic> result = users
    .OrderBy(user => user.Age)
    .ThenBy(user => user.Name);

// Результат:
// Alice, 20
// Bob, 20
// Tom, 30
```


### 4.6. `ThenByDescending`

Добавляет последующий критерий сортировки по убыванию


### 4.7. `Reverse`

Возвращает элементы в порядке, обратном порядку их получения из исходной последовательности. 

Возвращает `IEnumerable<TSource>`. Выполнение отложенное, но при начале перечисления источник полностью копируется во внутренний массив, после чего массив перечисляется с конца.

Перегрузки:

```cs
IEnumerable<TSource> Reverse<TSource>(
    this IEnumerable<TSource> source)
```

```cs
IEnumerable<TSource> Reverse<TSource>(
    this TSource[] source)
```

Перегрузка для массива присутствует в .NET 10. Обе перегрузки возвращают новую последовательность и не изменяют исходный массив

```cs
int[] numbers = [3, 1, 2];

IEnumerable<int> result = numbers.Reverse();

// Результат: 2, 1, 3
```


### 4.8. `Shuffle`

Возвращает элементы исходной последовательности в случайном порядке

Возвращает `IEnumerable<TSource>`. Выполнение отложенное. При начале перечисления источник полностью копируется в массив, после чего массив перемешивается. Используется некриптографический генератор случайных чисел. Метод доступен начиная с .NET 10.

```cs
IEnumerable<TSource> Shuffle<TSource>(
    this IEnumerable<TSource> source)
```

```cs
int[] numbers = [1, 2, 3, 4, 5];

IEnumerable<int> result = numbers.Shuffle();

// Один из возможных результатов: 3, 1, 5, 2, 4
```

---

## 5. Операции над множествами

Методы этой группы выполняют операции над последовательностями как над множествами

Сравнение выполняется через `IEqualityComparer<T>`. Если компаратор не передан или равен `null`, используется `EqualityComparer<T>.Default`

Все методы возвращают `IEnumerable<TSource>` и выполняются отложенно. Для отслеживания уже встреченных элементов или ключей используются внутренние хеш-множества

### 5.1. `Distinct`

Удаляет повторяющиеся элементы из одной последовательности

Перегрузки:

```cs
IEnumerable<TSource> Distinct<TSource>(
    this IEnumerable<TSource> source)
```

```cs
IEnumerable<TSource> Distinct<TSource>(
    this IEnumerable<TSource> source,
    IEqualityComparer<TSource>? comparer)
```

Пример:

```cs
int[] numbers = [1, 2, 2, 3, 1];

IEnumerable<int> result = numbers.Distinct();

// Результат: 1, 2, 3
```


### 5.2. `DistinctBy`

Удаляет повторяющиеся элементы по ключу, возвращаемому `keySelector`. В результат попадают исходные элементы типа `TSource`, а не сами ключи

Перегрузки:

```cs
IEnumerable<TSource> DistinctBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector)
```

```cs
IEnumerable<TSource> DistinctBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IEqualityComparer<TKey>? comparer)
```

Для каждого уникального ключа возвращается первый встретившийся элемент

```cs
var users = new[]
{
    new { Id = 1, Name = "Tom" },
    new { Id = 2, Name = "Bob" },
    new { Id = 1, Name = "Thomas" }
};

var result = users.DistinctBy(user => user.Id);

// Результат:
// 1, Tom
// 2, Bob
```


### 5.3. `Union`

Объединение двух последовательностей без дубликатов

Перегрузки:

```cs
IEnumerable<TSource> Union<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second)
```

```cs
IEnumerable<TSource> Union<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second,
    IEqualityComparer<TSource>? comparer)
```

Сначала перечисляется `first`, затем `second`. Каждый элемент возвращается только при первом появлении среди обеих последовательностей

```cs
int[] first = [1, 2, 2];
int[] second = [2, 3, 1, 4];

IEnumerable<int> result = first.Union(second);

// Результат: 1, 2, 3, 4
```


### 5.4. `UnionBy`

Объединение двух последовательностей по ключам без повторов

Перегрузки:

```cs
IEnumerable<TSource> UnionBy<TSource, TKey>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second,
    Func<TSource, TKey> keySelector)
```

```cs
IEnumerable<TSource> UnionBy<TSource, TKey>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second,
    Func<TSource, TKey> keySelector,
    IEqualityComparer<TKey>? comparer)
```

Пример:

```cs
var localUsers = new[]
{
    new { Id = 1, Name = "Tom" },
    new { Id = 2, Name = "Bob" }
};

var remoteUsers = new[]
{
    new { Id = 2, Name = "Robert" },
    new { Id = 3, Name = "Alice" }
};

var result = localUsers.UnionBy(
    remoteUsers,
    user => user.Id);

// Результат:
// 1, Tom
// 2, Bob
// 3, Alice
```


### 5.5. `Intersect`

Пересечение. Возвращает уникальные элементы, присутствующие одновременно в обеих последовательностях

Перегрузки:

```cs
IEnumerable<TSource> Intersect<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second)
```

```cs
IEnumerable<TSource> Intersect<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second,
    IEqualityComparer<TSource>? comparer)
```

```cs
int[] first = [1, 2, 2, 3, 5];
int[] second = [2, 3, 4];

IEnumerable<int> result = first.Intersect(second);

// Результат: 2, 3
```


### 5.6. `IntersectBy`

Перечесение по ключу. 

Перегрузки:

```cs
IEnumerable<TSource> IntersectBy<TSource, TKey>(
    this IEnumerable<TSource> first,
    IEnumerable<TKey> second,
    Func<TSource, TKey> keySelector)
```

```cs
IEnumerable<TSource> IntersectBy<TSource, TKey>(
    this IEnumerable<TSource> first,
    IEnumerable<TKey> second,
    Func<TSource, TKey> keySelector,
    IEqualityComparer<TKey>? comparer)
```

Пример:

```cs
var users = new[]
{
    new { Id = 1, Name = "Tom" },
    new { Id = 2, Name = "Bob" },
    new { Id = 3, Name = "Alice" }
};

int[] selectedIds = [2, 3];

var result = users.IntersectBy(
    selectedIds,
    user => user.Id);

// Результат:
// 2, Bob
// 3, Alice
```


### 5.7. `Except`

Разность. Возвращает уникальные элементы первой последовательности, отсутствующие во второй

Перегрузки:

```cs
IEnumerable<TSource> Except<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second)
```

```cs
IEnumerable<TSource> Except<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second,
    IEqualityComparer<TSource>? comparer)
```

Пример:

```cs
int[] first = [1, 2, 2, 3, 5];
int[] second = [2, 4, 5];

IEnumerable<int> result = first.Except(second);

// Результат: 1, 3
```


### 5.8. `ExceptBy`

Разность по ключу.

Перегрузки:

```cs
IEnumerable<TSource> ExceptBy<TSource, TKey>(
    this IEnumerable<TSource> first,
    IEnumerable<TKey> second,
    Func<TSource, TKey> keySelector)
```

```cs
IEnumerable<TSource> ExceptBy<TSource, TKey>(
    this IEnumerable<TSource> first,
    IEnumerable<TKey> second,
    Func<TSource, TKey> keySelector,
    IEqualityComparer<TKey>? comparer)
```

```cs
var users = new[]
{
    new { Id = 1, Name = "Tom" },
    new { Id = 2, Name = "Bob" },
    new { Id = 3, Name = "Alice" }
};

int[] excludedIds = [2];

var result = users.ExceptBy(
    excludedIds,
    user => user.Id);

// Результат:
// 1, Tom
// 3, Alice
```

---

## 6. Объединение последовательностей

Методы этой группы формируют последовательность из элементов нескольких источников или добавляют отдельный элемент в начало или конец. Исходные последовательности не изменяются

### 6.1. `Concat`

Последовательно объединяет две последовательности одного типа. Сначала возвращаются все элементы `first`, затем все элементы `second`

```cs
IEnumerable<TSource> Concat<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second)
```

```cs
int[] first = [1, 2, 3];
int[] second = [4, 5];

IEnumerable<int> result = first.Concat(second);

// Результат: 1, 2, 3, 4, 5
```

Не удаляет повторяющиеся элементы.


### 6.2. `Append`

Добавляет один элемент в конец последовательности

Возвращает `IEnumerable<TSource>`. Выполнение отложенное и потоковое. Сначала перечисляется весь источник, затем возвращается добавленный элемент. Исходная коллекция не изменяется.

```cs
IEnumerable<TSource> Append<TSource>(
    this IEnumerable<TSource> source,
    TSource element)
```

```cs
int[] numbers = [1, 2, 3];

IEnumerable<int> result = numbers.Append(4);

// Результат: 1, 2, 3, 4
```


### 6.3. `Prepend`

Добавляет один элемент в начало последовательности

Возвращает `IEnumerable<TSource>`. Выполнение отложенное и потоковое. Добавленный элемент возвращается до начала перечисления исходного источника. Исходная коллекция не изменяется.

```cs
IEnumerable<TSource> Prepend<TSource>(
    this IEnumerable<TSource> source,
    TSource element)
```

```cs
int[] numbers = [1, 2, 3];

IEnumerable<int> result = numbers.Prepend(0);

// Результат: 0, 1, 2, 3
// Массив numbers остаётся без изменений
```

### 6.4. `Zip`

Объединяет элементы нескольких последовательностей с одинаковыми индексами

Выполнение отложенное и потоковое. Перечислители источников двигаются синхронно. Перечисление прекращается, как только заканчивается самая короткая последовательность.

Перегрузка для двух последовательностей возвращает `IEnumerable<(TFirst First, TSecond Second)>`. Элемент результата является кортежем `ValueTuple<TFirst, TSecond>`

```cs
IEnumerable<(TFirst First, TSecond Second)> Zip<TFirst, TSecond>(
    this IEnumerable<TFirst> first,
    IEnumerable<TSecond> second)
```

```cs
string[] names = ["Tom", "Bob", "Alice"];
int[] ages = [20, 25, 30];

IEnumerable<(string First, int Second)> result =
    names.Zip(ages);

// Результат:
// ("Tom", 20)
// ("Bob", 25)
// ("Alice", 30)
```

Элементы кортежа доступны через `First` и `Second`:

```cs
foreach (var pair in names.Zip(ages))
{
    Console.WriteLine($"{pair.First}: {pair.Second}");
}

// Tom: 20
// Bob: 25
// Alice: 30
```

Перегрузка с `resultSelector` формирует произвольный результат из пары элементов и возвращает `IEnumerable<TResult>`

```cs
IEnumerable<TResult> Zip<TFirst, TSecond, TResult>(
    this IEnumerable<TFirst> first,
    IEnumerable<TSecond> second,
    Func<TFirst, TSecond, TResult> resultSelector)
```

```cs
IEnumerable<string> result = names.Zip(
    ages,
    (name, age) => $"{name}: {age}");

// Результат:
// "Tom: 20"
// "Bob: 25"
// "Alice: 30"
```

Перегрузка для трёх последовательностей возвращает `IEnumerable<(TFirst First, TSecond Second, TThird Third)>`

```cs
IEnumerable<(TFirst First, TSecond Second, TThird Third)>
    Zip<TFirst, TSecond, TThird>(
        this IEnumerable<TFirst> first,
        IEnumerable<TSecond> second,
        IEnumerable<TThird> third)
```

```cs
string[] names = ["Tom", "Bob"];
int[] ages = [20, 25];
string[] cities = ["Berlin", "Paris"];

var result = names.Zip(ages, cities);

// Результат:
// ("Tom", 20, "Berlin")
// ("Bob", 25, "Paris")
```

---

## 7. Соединение по ключу

Методы соединения сопоставляют элементы двух последовательностей по равенству ключей. Ключи извлекаются функциями `outerKeySelector` и `innerKeySelector`, сравнение выполняется через `IEqualityComparer<TKey>` (по умолчанию `EqualityComparer<TKey>.Default`)

Все методы выполняются отложенно, но одна из последовательностей при начале перечисления полностью загружается в хеш-структуру `Lookup<TKey, TElement>`. После этого вторая последовательность обрабатывается потоково. По принципу работы это `hash join`.

### 7.1. `Join`

Выполняет внутреннее соединение — возвращает только пары элементов, ключи которых совпали

Возвращает `IEnumerable<TResult>`. Для одного элемента `outer` может быть сформировано несколько результатов, если в `inner` найдено несколько совпадений

Перегрузки:

```cs
IEnumerable<TResult> Join<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter, TInner, TResult> resultSelector)
```

```cs
IEnumerable<TResult> Join<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter, TInner, TResult> resultSelector,
    IEqualityComparer<TKey>? comparer)
```

```cs
var users = new[]
{
    new { Id = 1, Name = "Tom" },
    new { Id = 2, Name = "Bob" },
    new { Id = 3, Name = "Alice" }
};

var orders = new[]
{
    new { Id = 101, UserId = 1 },
    new { Id = 102, UserId = 1 },
    new { Id = 103, UserId = 2 }
};

var result = users.Join(
    orders,
    user => user.Id,
    order => order.UserId,
    (user, order) => new
    {
        User = user.Name,
        OrderId = order.Id
    });

// Результат:
// Tom, 101
// Tom, 102
// Bob, 103
```


### 7.2. `GroupJoin`

Сопоставляет каждому элементу `outer` группу всех совпавших элементов из `inner`

`resultSelector` вызывается ровно один раз для каждого элемента `outer` и получает `IEnumerable<TInner>`. Если совпадений нет, передаётся пустая последовательность

Возвращает `IEnumerable<TResult>`

Перегрузки:

```cs
IEnumerable<TResult> GroupJoin<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter, IEnumerable<TInner>, TResult> resultSelector)
```

```cs
IEnumerable<TResult> GroupJoin<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter, IEnumerable<TInner>, TResult> resultSelector,
    IEqualityComparer<TKey>? comparer)
```

Пример:

```cs
var result = users.GroupJoin(
    orders,
    user => user.Id,
    order => order.UserId,
    (user, userOrders) => new
    {
        User = user.Name,
        Orders = userOrders.Select(order => order.Id)
    });

// Результат:
// Tom   → 101, 102
// Bob   → 103
// Alice → пустая последовательность
```

В отличие от `Join`, результат имеет иерархическую структуру: один элемент `outer` соответствует одной группе совпадений

При начале перечисления `inner` полностью загружается в `Lookup<TKey, TInner>`, после чего `outer` обрабатывается потоково.


### 7.3. `LeftJoin`

Выполняет левое внешнее соединение — возвращает все элементы `outer`, включая элементы без совпадений в `inner`

Если совпадение найдено, `resultSelector` вызывается для каждой пары. Если совпадений нет, вместо элемента `inner` передаётся `default(TInner)`

Возвращает `IEnumerable<TResult>`. Метод доступен начиная с .NET 10

Перегрузки:

```cs
IEnumerable<TResult> LeftJoin<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter, TInner?, TResult> resultSelector)
```

```cs
IEnumerable<TResult> LeftJoin<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter, TInner?, TResult> resultSelector,
    IEqualityComparer<TKey>? comparer)
```

Пример: 

```cs
var result = users.LeftJoin(
    orders,
    user => user.Id,
    order => order.UserId,
    (user, order) => new
    {
        User = user.Name,
        OrderId = order?.Id
    });

// Результат:
// Tom,   101
// Tom,   102
// Bob,   103
// Alice, null
```


### 7.4. `RightJoin`

Выполняет правое внешнее соединение — возвращает все элементы `inner`, включая элементы без совпадений в `outer`

Если совпадения нет, вместо элемента `outer` в `resultSelector` передаётся `default(TOuter)`

Возвращает `IEnumerable<TResult>`. Метод доступен начиная с .NET 10

Перегрузки:

```cs
IEnumerable<TResult> RightJoin<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter?, TInner, TResult> resultSelector)
```

```cs
IEnumerable<TResult> RightJoin<TOuter, TInner, TKey, TResult>(
    this IEnumerable<TOuter> outer,
    IEnumerable<TInner> inner,
    Func<TOuter, TKey> outerKeySelector,
    Func<TInner, TKey> innerKeySelector,
    Func<TOuter?, TInner, TResult> resultSelector,
    IEqualityComparer<TKey>? comparer)
```

Пример:

```cs
var ordersWithUnknownUser = new[]
{
    new { Id = 101, UserId = 1 },
    new { Id = 102, UserId = 4 }
};

var result = users.RightJoin(
    ordersWithUnknownUser,
    user => user.Id,
    order => order.UserId,
    (user, order) => new
    {
        User = user?.Name,
        OrderId = order.Id
    });

// Результат:
// Tom,  101
// null, 102
```

---

## 8. Группировка

Группировка объединяет элементы с одинаковыми ключами в отдельные последовательности. Ключ извлекается через `keySelector` и сравнивается с помощью `IEqualityComparer<TKey>` (по умолчанию `EqualityComparer<TKey>.Default`)

### 8.1. `GroupBy`

Группирует элементы последовательности по ключу

Базовые перегрузки:

```cs
IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector)
```

```cs
IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IEqualityComparer<TKey>? comparer)
```

`IGrouping<TKey, TElement>` представляет одну группу, реализует `IEnumerable<TElement>` и содержит свойство `Key` типа `TKey`.

```cs
string[] names = ["Tom", "Bob", "Alice", "Sam"];

IEnumerable<IGrouping<int, string>> groups =
    names.GroupBy(name => name.Length);

foreach (IGrouping<int, string> group in groups)
{
    Console.WriteLine($"Длина: {group.Key}");

    foreach (string name in group)
    {
        Console.WriteLine(name);
    }
}

// Результат:
// Длина: 3 → Tom, Bob, Sam
// Длина: 5 → Alice
```

`GroupBy` выполняется отложенно. При начале перечисления источник полностью считывается и по нему строятся все группы, поэтому метод не является потоковым

Группы возвращаются в порядке первого появления соответствующего ключа, а элементы внутри группы — в порядке их появления в исходной последовательности.

#### Перегрузки с `elementSelector`

Позволяют определить, какие значения будут храниться внутри каждой группы

```cs
IEnumerable<IGrouping<TKey, TElement>>
    GroupBy<TSource, TKey, TElement>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        Func<TSource, TElement> elementSelector)
```

```cs
IEnumerable<IGrouping<TKey, TElement>>
    GroupBy<TSource, TKey, TElement>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        Func<TSource, TElement> elementSelector,
        IEqualityComparer<TKey>? comparer)
```

Пример: 

```cs
var users = new[]
{
    new { Name = "Tom", Department = "IT" },
    new { Name = "Bob", Department = "IT" },
    new { Name = "Alice", Department = "HR" }
};

IEnumerable<IGrouping<string, string>> groups =
    users.GroupBy(
        user => user.Department,
        user => user.Name);

// Результат:
// IT → Tom, Bob
// HR → Alice
```

Исходный элемент имеет анонимный тип, но внутри группы хранится только `string`, возвращённый `elementSelector`

#### Перегрузки с `resultSelector`

Позволяют сразу преобразовать каждую группу в результирующий объект вместо возвращения `IGrouping<TKey, TElement>`

```cs
IEnumerable<TResult> GroupBy<TSource, TKey, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    Func<TKey, IEnumerable<TSource>, TResult> resultSelector)
```

```cs
IEnumerable<TResult> GroupBy<TSource, TKey, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    Func<TKey, IEnumerable<TSource>, TResult> resultSelector,
    IEqualityComparer<TKey>? comparer)
```

Пример:

```cs
var users = new[]
{
    new { Name = "Tom", Department = "IT" },
    new { Name = "Bob", Department = "IT" },
    new { Name = "Alice", Department = "HR" }
};

var result = users.GroupBy(
    user => user.Department,
    (department, departmentUsers) => new
    {
        Department = department,
        Count = departmentUsers.Count()
    });

// Результат:
// IT, 2
// HR, 1
```

`resultSelector` получает ключ группы и последовательность её элементов

#### Перегрузки с `elementSelector` и `resultSelector`

Позволяют сначала преобразовать элементы внутри групп, а затем сформировать итоговое значение из каждой группы

```cs
IEnumerable<TResult>
    GroupBy<TSource, TKey, TElement, TResult>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        Func<TSource, TElement> elementSelector,
        Func<TKey, IEnumerable<TElement>, TResult> resultSelector)
```

```cs
IEnumerable<TResult>
    GroupBy<TSource, TKey, TElement, TResult>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        Func<TSource, TElement> elementSelector,
        Func<TKey, IEnumerable<TElement>, TResult> resultSelector,
        IEqualityComparer<TKey>? comparer)
```

Пример:

```cs
var result = users.GroupBy(
    user => user.Department,
    user => user.Name,
    (department, names) => new
    {
        Department = department,
        Names = string.Join(", ", names)
    });

// Результат:
// IT → "Tom, Bob"
// HR → "Alice"
```


### 8.2. `ToLookup`

Группирует элементы по ключу и немедленно создаёт индексированную структуру `ILookup<TKey, TElement>`

Перегрузки:

```cs
ILookup<TKey, TSource> ToLookup<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector)
```

```cs
ILookup<TKey, TSource> ToLookup<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IEqualityComparer<TKey>? comparer)
```

```cs
ILookup<TKey, TElement> ToLookup<TSource, TKey, TElement>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    Func<TSource, TElement> elementSelector)
```

```cs
ILookup<TKey, TElement> ToLookup<TSource, TKey, TElement>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    Func<TSource, TElement> elementSelector,
    IEqualityComparer<TKey>? comparer)
```

В отличие от `GroupBy`, `ToLookup` выполняется немедленно: исходная последовательность полностью перечисляется непосредственно при вызове метода

`ILookup<TKey, TElement>` представляет словарь «один ко многим»: каждому ключу соответствует последовательность значений. Он поддерживает индексатор по ключу, свойство `Count`, метод `Contains` и перечисление групп.

```cs
var users = new[]
{
    new { Name = "Tom", Department = "IT" },
    new { Name = "Bob", Department = "IT" },
    new { Name = "Alice", Department = "HR" }
};

ILookup<string, string> usersByDepartment =
    users.ToLookup(
        user => user.Department,
        user => user.Name);

IEnumerable<string> itUsers = usersByDepartment["IT"];

// Результат: Tom, Bob
```

При обращении по отсутствующему ключу возвращается пустая последовательность

---

## 9. Получение элемента


### 9.1. `ElementAt`

Возвращает элемент по указанному индексу. Индексация начинается с нуля

Перегрузки:

```cs
TSource ElementAt<TSource>(
    this IEnumerable<TSource> source,
    int index)
```

```cs
TSource ElementAt<TSource>(
    this IEnumerable<TSource> source,
    Index index)
```

Перегрузка с `int` принимает индекс от начала последовательности:

```cs
string result = names.ElementAt(1);
```

Перегрузка с `System.Index` позволяет указывать позицию как от начала, так и от конца:

```cs
string last = names.ElementAt(^1);
string secondFromEnd = names.ElementAt(^2);
```


### 9.2. `ElementAtOrDefault`

Возвращает элемент по индексу либо `default(TSource)`, если индекс находится вне границ последовательности

Перегрузки:

```cs
TSource? ElementAtOrDefault<TSource>(
    this IEnumerable<TSource> source,
    int index)
```

```cs
TSource? ElementAtOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Index index)
```


### 9.3. `First`

Возвращает первый элемент последовательности либо первый элемент, удовлетворяющий условию

Перегрузки:

```cs
TSource First<TSource>(
    this IEnumerable<TSource> source)
```

```cs
TSource First<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

```cs
int[] numbers = [10, 15, 20, 25];

int first = numbers.First();
int firstEven = numbers.First(number => number % 2 == 0);

// first: 10
// firstEven: 10
```

Если последовательность пуста или ни один элемент не удовлетворяет условию, выбрасывается `InvalidOperationException`.


### 9.4. `FirstOrDefault`

Возвращает первый подходящий элемент либо значение по умолчанию, если элемент не найден

Перегрузки:

```cs
TSource? FirstOrDefault<TSource>(
    this IEnumerable<TSource> source)
```

```cs
TSource? FirstOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

```cs
TSource FirstOrDefault<TSource>(
    this IEnumerable<TSource> source,
    TSource defaultValue)
```

```cs
TSource FirstOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate,
    TSource defaultValue)
```


### 9.5. `Last`

Возвращает последний элемент последовательности либо последний элемент, удовлетворяющий условию

Перегрузки:

```cs
TSource Last<TSource>(
    this IEnumerable<TSource> source)
```

```cs
TSource Last<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

```
int[] numbers = [10, 15, 20, 25];

int last = numbers.Last();
int lastEven = numbers.Last(number => number % 2 == 0);

// last: 25
// lastEven: 20
```

Если последовательность пуста или ни один элемент не удовлетворяет условию, выбрасывается `InvalidOperationException`.


### 9.6. `LastOrDefault`

Возвращает последний подходящий элемент либо значение по умолчанию, если элемент не найден

Перегрузки:

```cs
TSource? LastOrDefault<TSource>(
    this IEnumerable<TSource> source)
```

```cs
TSource? LastOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

```cs
TSource LastOrDefault<TSource>(
    this IEnumerable<TSource> source,
    TSource defaultValue)
```

```cs
TSource LastOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate,
    TSource defaultValue)
```


### 9.7. `Single`

Возвращает единственный элемент последовательности и одновременно проверяет, что других элементов нет

Перегрузки:

```cs
TSource Single<TSource>(
    this IEnumerable<TSource> source)
```

```cs
TSource Single<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

`Single` выбрасывает `InvalidOperationException`, если:

- последовательность пуста
- последовательность содержит больше одного элемента
- условию не соответствует ни один элемент
- условию соответствует больше одного элемента


### 9.8. `SingleOrDefault`

Возвращает единственный элемент либо значение по умолчанию, если элементов нет. При наличии более одного элемента всё равно выбрасывается `InvalidOperationException`

Перегрузки:

```cs
TSource? SingleOrDefault<TSource>(
    this IEnumerable<TSource> source)
```

```cs
TSource? SingleOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

```cs
TSource SingleOrDefault<TSource>(
    this IEnumerable<TSource> source,
    TSource defaultValue)
```

```cs
TSource SingleOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate,
    TSource defaultValue)
```

```cs
int[] empty = [];

int result = empty.SingleOrDefault();

// Результат: 0
```

Можно передать собственное значение:

```cs
int result = empty.SingleOrDefault(-1);

// Результат: -1
```

При использовании условия значение по умолчанию возвращается, если совпадений нет:

```cs
int[] numbers = [10, 20];

int result = numbers.SingleOrDefault(
    number => number == 30,
    -1);

// Результат: -1
```


### 9.9. `DefaultIfEmpty`

Возвращает исходную последовательность, если она непустая. Для пустой последовательности возвращает один элемент: `default(TSource)` либо переданное значение.

```cs
IEnumerable<TSource> DefaultIfEmpty<TSource>(
    this IEnumerable<TSource> source)

IEnumerable<TSource> DefaultIfEmpty<TSource>(
    this IEnumerable<TSource> source,
    TSource defaultValue)
```

```cs
int[] numbers = [];

var first = numbers.DefaultIfEmpty();
// Результат: 0

var second = numbers.DefaultIfEmpty(-1);
// Результат: -1
```

---

## 10. Проверка последовательности

Методы этой группы проверяют наличие элементов, выполнение условия или равенство последовательностей

Все методы возвращают `bool` и выполняются немедленно. 

### 10.1. `Any`

Проверяет, содержит ли последовательность хотя бы один элемент либо существует ли хотя бы один элемент, удовлетворяющий условию

Перегрузки:

```cs
bool Any<TSource>(
    this IEnumerable<TSource> source)
```

```cs
bool Any<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

Перегрузка без `predicate` проверяет, является ли последовательность непустой:

```cs
int[] numbers = [10, 20, 30];

bool result = numbers.Any();

// Результат: true
```

Перегрузка с `predicate` проверяет, существует ли хотя бы один подходящий элемент:

```cs
int[] numbers = [1, 3, 6, 7];

bool hasEven = numbers.Any(
    number => number % 2 == 0);

// Результат: true
```


### 10.2. `All`

Проверяет, удовлетворяют ли условию все элементы последовательности

```cs
bool All<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

```cs
int[] numbers = [2, 4, 6];

bool allEven = numbers.All(
    number => number % 2 == 0);

// Результат: true
```


### 10.3. `Contains`

Проверяет, содержит ли последовательность указанное значение

Перегрузки:

```cs
bool Contains<TSource>(
    this IEnumerable<TSource> source,
    TSource value)
```

```cs
bool Contains<TSource>(
    this IEnumerable<TSource> source,
    TSource value,
    IEqualityComparer<TSource>? comparer)
```

Пример:

```cs
int[] numbers = [10, 20, 30];

bool containsTwenty = numbers.Contains(20);
bool containsForty = numbers.Contains(40);

// containsTwenty: true
// containsForty: false
```


### 10.4. `SequenceEqual`

Проверяет, равны ли две последовательности

Перегрузки:

```cs
bool SequenceEqual<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second)
```

```cs
bool SequenceEqual<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second,
    IEqualityComparer<TSource>? comparer)
```

Последовательности считаются равными, если одновременно выполняются два условия:

- они содержат одинаковое количество элементов
- элементы на одинаковых позициях равны

```cs
int[] first = [1, 2, 3];
int[] second = [1, 2, 3];

bool result = first.SequenceEqual(second);

// Результат: true
```

## 11. Подсчёт и агрегирование

Методы этой группы вычисляют одно итоговое значение для всей последовательности либо отдельные итоговые значения для каждого ключа

Большинство агрегирующих методов возвращают скалярное значение и выполняются немедленно. Исключение составляют `CountBy` и `AggregateBy`: они возвращают `IEnumerable<KeyValuePair<...>>` и выполняются отложенно, но перед выдачей результатов полностью обрабатывают источник

### 11.1. `Count`

Возвращает количество элементов последовательности либо количество элементов, удовлетворяющих условию

Перегрузки:

```cs
int Count<TSource>(
    this IEnumerable<TSource> source)
```

```cs
int Count<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```

```cs
int[] numbers = [10, 20, 30, 40];

int count = numbers.Count();
int evenCount = numbers.Count(
    number => number % 2 == 0);

// count: 4
// evenCount: 4
```


### 11.2. `LongCount`

Работает аналогично `Count`, но возвращает `long`

Перегрузки:

```cs
long LongCount<TSource>(
    this IEnumerable<TSource> source)
```

```cs
long LongCount<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
```


### 11.3. `TryGetNonEnumeratedCount`

Пытается получить количество элементов без перечисления источника

Сигнатура:

```cs
bool TryGetNonEnumeratedCount<TSource>(
    this IEnumerable<TSource> source,
    out int count)
```

```cs
IEnumerable<int> numbers = new List<int>
{
    10, 20, 30
};

bool success =
    numbers.TryGetNonEnumeratedCount(out int count);

// success: true
// count: 3
```

Метод выполняется немедленно и возвращает:

```cs
true  → количество удалось определить без перечисления
false → количество заранее неизвестно
```

При `false` значение выходного параметра `count` равно `0`, но это не означает, что последовательность пуста

```cs
IEnumerable<int> Generate()
{
    yield return 10;
    yield return 20;
}

IEnumerable<int> numbers = Generate();

bool success =
    numbers.TryGetNonEnumeratedCount(out int count);

// success: false
// count: 0
```


### 11.4. `CountBy`

Подсчитывает количество элементов для каждого ключа

Сигнатура:

```cs
IEnumerable<KeyValuePair<TKey, int>> CountBy<TSource, TKey>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        IEqualityComparer<TKey>? keyComparer = null)
    where TKey : notnull
```

```cs
string[] words =
[
    "cat",
    "dog",
    "apple",
    "car",
    "table"
];

IEnumerable<KeyValuePair<int, int>> result =
    words.CountBy(word => word.Length);

// Результат:
// Key = 3, Value = 3
// Key = 5, Value = 2
```

`Key` содержит ключ группы, а `Value` — количество элементов с этим ключом:

```cs
foreach (KeyValuePair<int, int> pair in result)
{
    Console.WriteLine(
        $"{pair.Key}: {pair.Value}");
}
```


### 11.5. `Sum`

Вычисляет сумму числовых элементов последовательности

Метод имеет перегрузки для:

```cs
int        int?
long       long?
float      float?
double     double?
decimal    decimal?
```

Для каждого типа существуют две формы:

```cs
TNumber Sum(
	this IEnumerable<TNumber> source)
```

```cs
TNumber Sum<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, TNumber> selector)
```

Фактическая сигнатура отдельная для каждого поддерживаемого числового типа

```cs
int[] numbers = [10, 20, 30];

int sum = numbers.Sum();

// Результат: 60
```

Перегрузка с `selector` сначала получает числовое значение из каждого элемента:

```cs
var orders = new[]
{
    new { Id = 1, Price = 100m },
    new { Id = 2, Price = 250m },
    new { Id = 3, Price = 50m }
};

decimal total = orders.Sum(
    order => order.Price);

// Результат: 400
```

Метод выполняется немедленно и перечисляет весь источник

Для пустой последовательности возвращается ноль:

```cs
int[] numbers = [];

int sum = numbers.Sum();

// Результат: 0
```

В nullable-последовательностях значения `null` пропускаются. Если последовательность пуста или содержит только `null`, возвращается nullable-значение, содержащее ноль:

Для `int`, `long` и `decimal` переполнение суммы приводит к `OverflowException`.

### 11.6. `Average`

Вычисляет среднее арифметическое числовых элементов

Метод имеет перегрузки для тех же числовых типов и их nullable-вариантов:

```cs
int        int?
long       long?
float      float?
double     double?
decimal    decimal?
```

Также существуют перегрузки с `selector`:

```cs
double Average(
    this IEnumerable<int> source)
```

```cs
double Average<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, int> selector)
```

Возвращаемый тип зависит от исходного числового типа:

|Исходный тип|Результат|
|---|---|
|`int`|`double`|
|`int?`|`double?`|
|`long`|`double`|
|`long?`|`double?`|
|`float`|`float`|
|`float?`|`float?`|
|`double`|`double`|
|`double?`|`double?`|
|`decimal`|`decimal`|
|`decimal?`|`decimal?`|

Метод выполняется немедленно и должен перечислить всю последовательность

Для пустой последовательности не-nullable значений выбрасывается `InvalidOperationException`.

В nullable-последовательности значения `null` пропускаются. Если значений не осталось, возвращается `null`.

### 11.7. `Min` и `Max`

`Min` возвращает минимальное значение последовательности, а `Max` — максимальное

Основные generic-перегрузки:

```cs
TSource? Min<TSource>(
    this IEnumerable<TSource> source)
```

```cs
TSource? Min<TSource>(
    this IEnumerable<TSource> source,
    IComparer<TSource>? comparer)
```

```cs
TResult? Min<TSource, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, TResult> selector)
```

Для `Max` существуют аналогичные перегрузки:

```cs
TSource? Max<TSource>(
    this IEnumerable<TSource> source)
```

```cs
TSource? Max<TSource>(
    this IEnumerable<TSource> source,
    IComparer<TSource>? comparer)
```

```cs
TResult? Max<TSource, TResult>(
    this IEnumerable<TSource> source,
    Func<TSource, TResult> selector)
```

Перегрузка с `selector` возвращает минимальное или максимальное **проецируемое значение**, а не исходный объект.

Для пустой последовательности не-nullable значимых типов выбрасывается `InvalidOperationException`. Для nullable-типов и ссылочных типов пустая последовательность либо последовательность из одних `null` возвращает `null`.

### 11.8. `MinBy` и `MaxBy`

Возвращают исходный элемент с минимальным или максимальным ключом

Перегрузки `MinBy`:

```cs
TSource? MinBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector)
```

```cs
TSource? MinBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IComparer<TKey>? comparer)
```

Для `MaxBy` существуют аналогичные перегрузки:

```cs
TSource? MaxBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector)
```

```cs
TSource? MaxBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IComparer<TKey>? comparer)
```

Методы выполняются немедленно и перечисляют последовательность полностью. Если несколько элементов имеют одинаковый минимальный или максимальный ключ, возвращается первый из них.

### 11.9. `Aggregate`

Последовательно применяет функцию-аккумулятор ко всем элементам и позволяет реализовать произвольную агрегацию

Имеет три перегрузки

#### Без начального значения

```cs
TSource Aggregate<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, TSource, TSource> func)
```

Первый элемент становится начальным аккумулятором, а обработка начинается со второго элемента:

```cs
int[] numbers = [2, 3, 4];

int product = numbers.Aggregate(
    (accumulator, number) =>
        accumulator * number);

// Шаги:
// accumulator = 2
// 2 * 3 = 6
// 6 * 4 = 24
//
// Результат: 24
```

Для пустой последовательности выбрасывается `InvalidOperationException`, поскольку первого значения для аккумулятора нет

#### С начальным значением

```cs
TAccumulate Aggregate<TSource, TAccumulate>(
    this IEnumerable<TSource> source,
    TAccumulate seed,
    Func<TAccumulate, TSource, TAccumulate> func)
```

```cs
int[] numbers = [2, 3, 4];

int product = numbers.Aggregate(
    1,
    (accumulator, number) =>
        accumulator * number);

// Результат: 24
```

Значение `seed` становится начальным аккумулятором:
Для пустой последовательности возвращается `seed`

Тип аккумулятора может отличаться от типа элементов:

```cs
string result = numbers.Aggregate(
    "",
    (text, number) =>
        text + $"[{number}]");

// Результат: "[2][3][4]"
```

#### С преобразованием результата

```cs
TResult Aggregate<TSource, TAccumulate, TResult>(
    this IEnumerable<TSource> source,
    TAccumulate seed,
    Func<TAccumulate, TSource, TAccumulate> func,
    Func<TAccumulate, TResult> resultSelector)
```

```cs
int[] numbers = [10, 20, 30];

double average = numbers.Aggregate(
    seed: (Sum: 0, Count: 0),
    func: (accumulator, number) =>
    (
        accumulator.Sum + number,
        accumulator.Count + 1
    ),
    resultSelector: accumulator =>
        (double)accumulator.Sum /
        accumulator.Count);

// Результат: 20
```

`func` строит итоговый аккумулятор, а `resultSelector` преобразует его в окончательный результат

Все перегрузки выполняются немедленно и обрабатывают элементы слева направо.

### 11.10. `AggregateBy`

Выполняет отдельную агрегацию для каждого ключа

Перегрузка с одинаковым начальным значением для всех ключей:

```cs
IEnumerable<KeyValuePair<TKey, TAccumulate>>
    AggregateBy<TSource, TKey, TAccumulate>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        TAccumulate seed,
        Func<TAccumulate, TSource, TAccumulate> func,
        IEqualityComparer<TKey>? keyComparer = null)
    where TKey : notnull
```

```cs
var employees = new[]
{
    new { Department = "IT", Salary = 100m },
    new { Department = "HR", Salary = 80m },
    new { Department = "IT", Salary = 120m }
};

var totals = employees.AggregateBy(
    employee => employee.Department,
    seed: 0m,
    (total, employee) =>
        total + employee.Salary);

// Результат:
// IT → 220
// HR → 80
```

Перегрузка с фабрикой начального значения:

```cs
IEnumerable<KeyValuePair<TKey, TAccumulate>>
    AggregateBy<TSource, TKey, TAccumulate>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        Func<TKey, TAccumulate> seedSelector,
        Func<TAccumulate, TSource, TAccumulate> func,
        IEqualityComparer<TKey>? keyComparer = null)
    where TKey : notnull
```

`seedSelector` вызывается отдельно для каждого нового ключа и может создавать начальное значение на основе самого ключа:

```cs
var statistics = employees.AggregateBy(
    employee => employee.Department,
    department => new
    {
        Department = department,
        Total = 0m,
        Count = 0
    },
    (state, employee) => new
    {
        state.Department,
        Total = state.Total + employee.Salary,
        Count = state.Count + 1
    });
```

Выполнение отложенное, но не потоковое. При начале перечисления метод полностью обрабатывает источник и хранит один аккумулятор для каждого ключа

---

## 12. Материализация и преобразование

### 12.1. `ToArray`

Полностью перечисляет источник и создаёт массив `TSource[]`

```cs
TSource[] ToArray<TSource>(
    this IEnumerable<TSource> source)
```

### 12.2. `ToList`

Полностью перечисляет источник и создаёт изменяемый `List<TSource>`

```cs
List<TSource> ToList<TSource>(
    this IEnumerable<TSource> source)
```

### 12.3. `ToDictionary`

Создаёт `Dictionary<TKey, TValue>` из элементов последовательности

Основные перегрузки с выбором ключа:

```cs
Dictionary<TKey, TSource> ToDictionary<TSource, TKey>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector)
    where TKey : notnull
```

```cs
Dictionary<TKey, TSource> ToDictionary<TSource, TKey>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        IEqualityComparer<TKey>? comparer)
    where TKey : notnull
```

Значениями словаря становятся сами исходные элементы:

```cs
var users = new[]
{
    new { Id = 1, Name = "Tom" },
    new { Id = 2, Name = "Bob" }
};

var usersById = users.ToDictionary(
    user => user.Id);

// usersById[1].Name: "Tom"
```

Перегрузки с выбором ключа и значения:

```cs
Dictionary<TKey, TElement>
    ToDictionary<TSource, TKey, TElement>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        Func<TSource, TElement> elementSelector)
    where TKey : notnull
```

```cs
Dictionary<TKey, TElement>
    ToDictionary<TSource, TKey, TElement>(
        this IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        Func<TSource, TElement> elementSelector,
        IEqualityComparer<TKey>? comparer)
    where TKey : notnull
```

Пример: 

```cs
Dictionary<int, string> namesById =
    users.ToDictionary(
        user => user.Id,
        user => user.Name);

// 1 → "Tom"
// 2 → "Bob"
```

Также существуют перегрузки для готовых пар `KeyValuePair<TKey, TValue>`:

```cs
Dictionary<TKey, TValue>
    ToDictionary<TKey, TValue>(
        this IEnumerable<KeyValuePair<TKey, TValue>> source)
    where TKey : notnull
```

```cs
Dictionary<TKey, TValue>
    ToDictionary<TKey, TValue>(
        this IEnumerable<KeyValuePair<TKey, TValue>> source,
        IEqualityComparer<TKey>? comparer)
    where TKey : notnull
```

И для кортежей `(Key, Value)`:

```cs
Dictionary<TKey, TValue>
    ToDictionary<TKey, TValue>(
        this IEnumerable<(TKey Key, TValue Value)> source)
    where TKey : notnull
```

```cs
Dictionary<TKey, TValue>
    ToDictionary<TKey, TValue>(
        this IEnumerable<(TKey Key, TValue Value)> source,
        IEqualityComparer<TKey>? comparer)
    where TKey : notnull
```

Пример:

```cs
IEnumerable<(int Key, string Value)> pairs =
[
    (1, "Tom"),
    (2, "Bob")
];

Dictionary<int, string> dictionary =
    pairs.ToDictionary();
```

### 12.4. `ToHashSet`

Полностью перечисляет источник и создаёт `HashSet<TSource>`

Перегрузки:

```cs
HashSet<TSource> ToHashSet<TSource>(
    this IEnumerable<TSource> source)
```

```cs
HashSet<TSource> ToHashSet<TSource>(
    this IEnumerable<TSource> source,
    IEqualityComparer<TSource>? comparer)
```

### 12.5. `AsEnumerable`

Возвращает тот же объект, представленный через тип `IEnumerable<TSource>`

```cs
IEnumerable<TSource> AsEnumerable<TSource>(
    this IEnumerable<TSource> source)
```

---

## 13. Генераторы последовательностей

Это статические методы `Enumerable`. Генераторы создают последовательности без исходной коллекции. 

### 13.1. `Empty`

Возвращает пустую последовательность указанного типа

```cs
IEnumerable<TResult> Empty<TResult>()
```

```cs
IEnumerable<int> numbers = Enumerable.Empty<int>();
```

Метод не является методом расширения и вызывается через класс `Enumerable`

```
Enumerable.Empty<User>()
```

Для каждого типа используется кэшированная пустая последовательность. Источник не перечисляется и элементы не создаются.

### 13.2. `Range`

Генерирует последовательность целых чисел типа `int`

```cs
IEnumerable<int> Range(
    int start,           // первое число
    int count)           // количество чисел
```

`start` определяет первое число, а `count` — количество чисел, а не последнее значение

```cs
IEnumerable<int> numbers = Enumerable.Range(5, 4);

// Результат: 5, 6, 7, 8
```

Метод возвращает `IEnumerable<int>` и выполняется отложенно: числа генерируются по мере перечисления, массив со всеми значениями заранее не создаётся.

### 13.3. `Repeat`

Создаёт последовательность, в которой одно значение повторяется указанное количество раз

```cs
IEnumerable<TResult> Repeat<TResult>(
    TResult element,
    int count)
```

```cs
IEnumerable<string> values =
    Enumerable.Repeat("hello", 3);

// Результат:
// "hello", "hello", "hello"
```

### 13.4. `Sequence` 

**.NET 10**. Создаёт конечную числовую последовательность от `start` до `endInclusive` с заданным шагом. Конечная граница включается только в том случае, если последовательность попадает в неё точно.

```cs
IEnumerable<T> Sequence<T>(
    T start,
    T endInclusive,
    T step)
    where T : INumber<T>
```

Пример:

```cs
IEnumerable<int> numbers =
    Enumerable.Sequence(1, 10, 3);

// Результат: 1, 4, 7, 10
```

Поддерживается отрицательный шаг:

```cs
var numbers = Enumerable.Sequence(10, 1, -3);

// Результат: 10, 7, 4, 1
```

### 13.5. `InfiniteSequence`

Создаёт бесконечную последовательность, начиная с `start` и прибавляя `step` после каждого элемента.

```cs
IEnumerable<T> InfiniteSequence<T>(
    T start,
    T step)
    where T : IAdditionOperators<T, T, T>
```

Пример:

```cs
IEnumerable<int> numbers =
    Enumerable.InfiniteSequence(1, 2);

var result = numbers.Take(5);

// Результат: 1, 3, 5, 7, 9
```

Метод выполняется отложенно и генерирует элементы по одному.

Так как последовательность бесконечная, обычно её ограничивают через `Take` или `TakeWhile`:

```cs
var result = Enumerable
    .InfiniteSequence(0, 10)
    .TakeWhile(number => number <= 50);

// Результат: 0, 10, 20, 30, 40, 50
```

