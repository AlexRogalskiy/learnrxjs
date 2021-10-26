# subscribeOn

## Сигнатура

```typescript
subscribeOn<T>(scheduler: SchedulerLike, delay: number = 0): MonoTypeOperatorFunction<T>
```

## Описание

Создает подписку через переданный шедулер

## Параметры

| Название | Описание |
|-|-|
| `scheduler` | Шедулер, который нужно использовать |
| `delay` | Количество миллисекунд, указывающее, с какой задержкой следует перенести каждое уведомление |

Через этот оператор вы можете контролировать момент создания подписки

## Пример

У нас есть следующий код

```typescript
import { of, merge } from 'rxjs';

const a = of(1, 2, 3);
const b = of(4, 5, 6);

merge(a, b).subscribe(console.log);

// Вывод
// 1
// 2
// 3
// 4
// 5
// 6
```

Оба потока `a` и `b` отправляют их значения синхронно по мере того как на них подписываются.

Теперь давайте посмотрим что будет если использовать оператор `subscribeOn` с шедулером `asyncScheduler`:

```typescript
import { of, merge, asyncScheduler } from 'rxjs';
import { subscribeOn } from 'rxjs/operators';

const a = of(1, 2, 3).pipe(subscribeOn(asyncScheduler));
const b = of(4, 5, 6);

merge(a, b).subscribe(console.log);

// Outputs
// 4
// 5
// 6
// 1
// 2
// 3
```

Это происходит потому что `asyncScheduler` планирует макро-задачу, а она ждет пока стек выполнения очистится и только после этого выполняет задачу.

## Полезные ссылки

- 📰 Официальная документация: [subscribeOn](https://rxjs.dev/api/operators/subscribeOn)
- 📁 Исходный код: https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/subscribeOn.ts

