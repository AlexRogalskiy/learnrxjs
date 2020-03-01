# Concat

## Сигнатура

```typescript
concat<O extends ObservableInput<any>, R>(...observables: (SchedulerLike | O)[]): Observable<ObservedValueOf<O> | R>
```

## Описание

Объединяет переданные Observable-ы в один. `concat` подписывается на пришедшие Observable-ы по очереди и в том же порядке отправляет данные, `concat` подписывается на первый Observable в списке и шлет данные во внешний Observable пока тот не закроется, после чего `concat` переходит к следующему и так до последнего, когда последний закрывается сам `concat` закрывается.

Запомните, в случае если один из Observable-ов никогда не закроется, то `concat` не перейдет к следующему Observable-у. А вот если один из Observable-ов закроется как только на него подпишутся не испуская никаких значений, то `concat` просто перейдет к следующему Observable.

Если в одном из Observable-ов произойдет ошибка, то `concat` закроется с ошибкой и Observable-ы которые были после Observable с ошибкой будут проигнорированы.

Если в `concat` передавать один и тот же Observable много раз, то его значения будут дублированы, это означает что один и тот же Observable можно "повторять" столько раз сколько вы хотите, только наример, в ручную 1000 раз передавать один и тот же Observalbe в `concat` может быть утомительно, поэтому для этого есть оператор `repeat`

## Параметры

- `observables`

  Список Observable-ов

## Примеры

### Пример 1: Объединение `interval` и `range`

```typescript
import { concat, interval, range } from 'rxjs';
import { take } from 'rxjs/operators';

const timer = interval(1000).pipe(take(4));
const sequence = range(1, 10);
const result = concat(timer, sequence);
result.subscribe(x => console.log(x));

// results in:
// 0 -1000ms-> 1 -1000ms-> 2 -1000ms-> 3 -immediate-> 1 ... 10
```

### Пример 2: Объединение 3-х Observable-ов

```typescript
import { concat, interval } from 'rxjs';
import { take } from 'rxjs/operators';

const timer1 = interval(1000).pipe(take(10));
const timer2 = interval(2000).pipe(take(6));
const timer3 = interval(500).pipe(take(10));

const result = concat(timer1, timer2, timer3);
result.subscribe(x => console.log(x));

// results in the following:
// (Prints to console sequentially)
// -1000ms-> 0 -1000ms-> 1 -1000ms-> ... 9
// -2000ms-> 0 -2000ms-> 1 -2000ms-> ... 5
// -500ms-> 0 -500ms-> 1 -500ms-> ... 9
```

## Полезные ссылки

- 📰 Официальная документация: [concat](https://rxjs.dev/api/index/function/concat)
- 📁 Исходный код: https://github.com/ReactiveX/rxjs/blob/6.5.4/src/internal/observable/concat.ts
