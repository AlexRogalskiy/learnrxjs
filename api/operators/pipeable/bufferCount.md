# BufferCount

## Сигнатура

```typescript
bufferCount<T>(bufferSize: number, startBufferEvery: number = null): OperatorFunction<T, T[]>
```

## Описание
Буферизует значения потока-источника, до тех пор, пока их количество не достигнет максимального значения, заданного в bufferSize. После выдачи значений буфер очищается. Новый буфер создается через каждые startBufferEvery значений. Если startBufferEvery не задан или равен null, новый буфер создается на старте входного потока и после каждого закрытия и выдачи прошлого буфера.



## Параметры

| Название | Описание |
|-|-|
| `bufferSize` | Максимальный размер выдаваемого буфера. |
| `startBufferEvery` | Интервал между созданием нового буфера. Например, если startBufferEvery равен 2, тогда новый буфер будет создаваться через одно значение из входного потока. Новый буфер по умолчанию создается при старте входного потока. |


## Примеры

### Пример 1

Выдавать последние два клика в виде массива

```typescript
// RxJS v6+
import { fromEvent } from 'rxjs';
import { bufferCount } from 'rxjs/operators';

const clicks = fromEvent(document, 'click');
const buffered = clicks.pipe(bufferCount(2));
buffered.subscribe(x => console.log(x));
```

### Пример 2

На каждый клик выдавать последние два клика в виде массива

```typescript
// RxJS v6+
import { fromEvent } from 'rxjs';
import { bufferCount } from 'rxjs/operators';

const clicks = fromEvent(document, 'click');
const buffered = clicks.pipe(bufferCount(2, 1));
buffered.subscribe(x => console.log(x));
```

## Полезные ссылки

- 📰 Официальная документация: [bufferCount](https://rxjs.dev/api/operators/bufferCount)
- 📁 Исходный код: https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/bufferCount.ts
 
