
**Unit of Work** — паттерн, который объединяет набор изменений данных в одну логическую операцию и координирует их сохранение как единого целого.

```cs
var order = await orders.GetAsync(id);

order.Confirm();
payments.Add(payment);

await unitOfWork.CommitAsync();
```

Идея:

- изменить несколько объектов
- накопить изменения
- сохранить их одной операцией / транзакцией

Unit of Work отвечает за:

- отслеживание изменений
- координацию нескольких Repository
- фиксацию изменений
- rollback при ошибке

В EF Core роль Unit of Work в значительной степени выполняет `DbContext`:

```cs
await dbContext.SaveChangesAsync();
```

Он собирает изменения отслеживаемых Entity и сохраняет их одной транзакцией.