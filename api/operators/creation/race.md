# race

## Сигнатура

```typescript
race<T>(...sources: (Observable<T> | InteropObservable<T> | AsyncIterable<T> | PromiseLike<T> | ArrayLike<T> | Iterable<...> | ReadableStreamLike<...> | ObservableInput<...>[])[]): Observable<any>
```

## Описание

Оператор `race` создает состояние гонки, кто первый приедет к финишу тот и победил. То есть он выбирает из всех переданных потоков, того кто первым отправит значение и работает только с ним.

## Параметры

| Название | Описание |
|-|-|
| `sources` | Список потоков, за которыми нужно следить |

![Оператор race](https://rxjs.dev/assets/images/marble-diagrams/race.png)

`race` подписывается на все переданные потоки и как только один из них отправит хотя бы одно значение, то он отписывается ото всех потоков и отправляет все значения этого потока дальше.

Если один из потоков кинет ошибку, то `race` так же кинет эту ошибку.

## Примеры

```typescript
import { race, interval } from 'rxjs';
import { mapTo } from 'rxjs/operators';

const obs1 = interval(1000).pipe(mapTo('Привет'));
const obs2 = interval(3000).pipe(mapTo('Hello'));
const obs3 = interval(5000).pipe(mapTo('Hola'));

race(obs3, obs1, obs2)
.subscribe(
  winner => console.log(winner)
);

// Выведет
// поток строк 'Привет'
```

## Полезные ссылки

- 📰 Официальная документация: [race](https://rxjs.dev/api/index/function/race)
- 📁 Исходный код: https://github.com/ReactiveX/rxjs/blob/master/src/internal/observable/race.ts#L11-L57
