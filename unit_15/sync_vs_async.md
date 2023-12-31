# Синхронность vs асинхронность

Синхронное (`Sync`) и асинхронное (`Async`) программирование может выполняться как в одном, так и в нескольких потоках.
Основное различие в том, что при синхронном программирования мы выполняем одну задачу за раз, а при асинхронном программировании — несколько задач выполняются одновременно.

Например:

- `Синхронность`
  - `Однопоточность`: я начинаю варить яйцо. После того как оно сварится, я могу начать поджаривать хлеб. Мне приходится ждать завершения одной задачи, чтобы начать другую.
  - `Многопоточность`: я начинаю варить яйцо, а после того как оно сварится, моя мама поджарит хлеб. Задачи выполняются одна за другой и разными лицами (потоками).
- `Асинхронность`:
  - `Однопоточность`: я ставлю яйцо вариться и устанавливаю таймер, кладу хлеб в тостер и запускаю другой таймер, а когда время выйдет — я буду есть. В асинхронном режиме мне не нужно ждать завершения задачи, чтобы начать еще одну.
  - `Многопоточность`: я нанимаю двух поваров, чтобы они сварили для меня яйцо и поджарили хлеб. Они могут делать это одновременно, и один не должен ждать другого, чтобы начать.

---

### [Назад к оглавлению](./README.md)