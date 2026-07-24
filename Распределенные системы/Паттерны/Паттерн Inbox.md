
[[#1. Основная идея Inbox]]
[[#2. Алгоритм обработки]]
[[#3. Пример]]
[[#4. Очистка Inbox]]

---

**Inbox** — паттерн обеспечения идемпотентной обработки входящих сообщений получателем.

# 1. Основная идея Inbox

Consumer хранит идентификаторы обработанных сообщений в отдельной таблице в одной СУБД с бизнес-таблицей. Атомарность гарантируется на уровне СУБД.

---

# 2. Алгоритм обработки

```
Сообщение пришло

Проверить MessageId в Inbox

начать транзакцию

Если MessageId существует
    сообщение уже обработано
    бизнес-операцию не выполнять
    ACK брокеру

Если MessageId отсутствует
    сохранить MessageId в Inbox
    выполнить бизнес-операцию
    ACK брокеру
```

## Блок схема
~~~mermaid
%%{init: {"flowchart": {"useMaxWidth": true}, "themeVariables": {"fontSize": "14px"}}}%%
flowchart TD
    A[Получить сообщение] --> B[BEGIN]
    B --> C[INSERT MessageId в Inbox]

    C --> D{MessageId уже существует?}

    D -->|Да| E[ROLLBACK]
    E --> F[ACK]
    F --> G[Дубликат пропущен]

    D -->|Нет| H[Изменить бизнес-данные]
    H --> I{Операция успешна?}

    I -->|Да| J[COMMIT]
    J --> K[ACK]
    K --> L[Сообщение обработано]

    I -->|Нет| M[ROLLBACK]
    M --> N[Не отправлять ACK]
    N --> O[Повторная доставка]
    O --> A
~~~

---

# 3. Пример

## Таблица Inbox

Минимальная структура:

```SQL
CREATE TABLE inbox_messages
(
    message_id UUID PRIMARY KEY,      -- уникальный id входящего сообщения
    processed_at TIMESTAMP NOT NULL   -- время успешной обработки сообщения
);
```

## Бизнес-таблица

```sql
CREATE TABLE users
(
    id BIGINT PRIMARY KEY,
    bonus_points INTEGER NOT NULL
);
```

## SQL-транзакция

```sql
BEGIN;

INSERT INTO inbox_messages
(
    message_id,                -- ошибка при существующем id
    processed_at
)
VALUES
(
    :message_id,
    CURRENT_TIMESTAMP
);

UPDATE users
SET bonus_points = bonus_points + 1
WHERE id = :user_id;

COMMIT;
```

После успешного `COMMIT` consumer отправляет ACK брокеру

---

# 4. Очистка Inbox

Таблица Inbox постоянно растёт

Старые записи необходимо удалять:

```sql
DELETE FROM inbox_messages
WHERE processed_at < CURRENT_TIMESTAMP - INTERVAL '30 days';
```

Срок хранения должен учитывать:

- максимальное время повторной доставки сообщения
- срок хранения сообщений в брокере
- возможность ручного replay
- длительность аварийного восстановления
- срок хранения сообщений в dead-letter queue

Если запись удалить слишком рано, старое сообщение может быть обработано повторно







