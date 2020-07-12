# Distinct

## Краткое описание

Пропускает только уникальные значения за все время жизни потока

## Сигнатура

```typescript
distinct<T, K>(
  keySelector?: (value: T) => K,
  flushes?: Observable<any>
): MonoTypeOperatorFunction<T>
```

## Параметры

| Название оператора | Описание |
|-|-|
| keySelector | Функция возвращает значение по которому будет происходить фильтрация |
| flushes | Поток, `next` которого очищает внутренний Set в котором хранятся все предыдущие значения  |

### Описание

Если функция `keySelector` объявлена, то в качестве значений для фильтрации будет использоваться то что возвращает эта функция, иначе фильтроваться будут сами значения.

Для повышения производительности работы фильтрации используется [`Set`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Set). В случае если он не поддерживается используется массив в связке с `indexOf`, что несколько медленнее, чем Set. Но даже в современных браузерах, долгое использование этого оператора может привести к утечкам памяти. Чтобы избежать этого вы можете использовать `flushes`, для очистки Set-а.

## Примеры

### Пример 1: фильтрация чисел

```typescript
// RxJS v6+
import { of } from 'rxjs';
import { distinct } from 'rxjs/operators';

of(1, 1, 2, 2, 2, 1, 2, 3, 4, 3, 2, 1).pipe(
    distinct(),
  )
  .subscribe(x => console.log(x)); // 1, 2, 3, 4
```

### Пример 2: использование `keySelector` функции

```typescript
import { of } from 'rxjs';
import { distinct } from 'rxjs/operators';

interface Person {
   age: number,
   name: string
}

of<Person>(
  { age: 4, name: 'Foo'},
  { age: 7, name: 'Bar'},
  { age: 5, name: 'Foo'},
).pipe(
  distinct((p: Person) => p.name),
)
.subscribe(x => console.log(x));

// displays:
// { age: 4, name: 'Foo' }
// { age: 7, name: 'Bar' }
```

## Полезные ссылки

- 📰 Официальная документация: [dictinct](https://rxjs.dev/api/operators/distinct)
- 📁 Исходный код: https://github.com/reactivex/rxjs/tree/6.5.5/src/internal/operators/distinct.ts

