# buffer

## Сигнатура

```typescript
buffer<T>(closingNotifier: Observable<any>): OperatorFunction<T, T[]>
```

## Описание
Собирает элементы внутреннего потока в массив, пока внешний поток `closingNotifier` не отправит новое значение, как только это происходит внутренний поток отправляет в качестве значения массив всех буферезированных значений.
 
## Параметры

| Название | Описание |
|-|-|
| `closingNotifier` | Объект класса Observable который сигнализирует какой буфер будет использован для вывода |

## Возвращаемое значение
OperatorFunction<T, T[]>: объект Observable содержащий буферы, которые являются массивами значений

## Примеры

### Пример 1

На каждый клик поток `buffered` отправляет массив значений собранный из потока `intervalEvents`

```typescript
// RxJS v6+
import { fromEvent, interval } from 'rxjs';
import { buffer } from 'rxjs/operators';

const clicks = fromEvent(document, 'click');
const intervalEvents = interval(1000);
const buffered = intervalEvents.pipe(buffer(clicks));
buffered.subscribe(x => console.log(x));
```

## Полезные ссылки

- [bufferCount](api/operators/pipeable/bufferTime.md)
- [bufferTime](api/operators/pipeable/bufferTime.md)
- [bufferToggle](api/operators/pipeable/bufferToggle.md)
- [bufferWhen](api/operators/pipeable/bufferWhen.md)
- [window](api/operators/pipeable/window.md)

- 📰 Официальная документация: [OPERATOR_NAME](OPERATOR_URL)
- 📁 Исходный код: https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/OPERATOR_NAME.ts
