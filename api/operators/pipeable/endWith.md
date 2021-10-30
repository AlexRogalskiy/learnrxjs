# endWith

## Сигнатура

```typescript
endWith<T>(...values: (SchedulerLike | T)[]): MonoTypeOperatorFunction<T>
```

## Описание

Завершает поток с переданным значением или значенимями.

## Параметры

| Название | Описание |
|-|-|
| `values` | Список значения, с которыми нужно завершить поток |

ЗАМЕТКА: Использование шедулера как последнего параметра считает устаревшим и может нарушить типизацию Typescript.

## Примеры

Отправляет строку «тик» каждые 5 секунд, пока пользователь не кликнет на страницу, завершив поток со значением «интервал завершился по клику».

```typescript
import { interval, fromEvent } from 'rxjs';
import { map, startWith, takeUntil, endWith } from 'rxjs/operators';

const ticker$ = interval(5000).pipe(
  map(() => 'тик'),
);

const documentClicks$ = fromEvent(document, 'click');

ticker$.pipe(
  startWith('интервал создался'),
  takeUntil(documentClicks$),
  endWith('интервал завершился по клику'),
)
.subscribe(
  x = console.log(x);
)

// Результат (предполагая что пользователь кликнет через 15 сек.)
// "интервал создался"
// "тик"
// "тик"
// "тик"
// "интервал завершился по клику"
```

## Полезные ссылки

- 📰 Официальная документация: [endWith](https://rxjs.dev/api/operators/endWith)
- 📁 Исходный код: https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/endWith.ts
