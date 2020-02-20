# TakeUntil

Отправляет значения пока прокинутый Observable не закрыт

> 💡Если вам нужно указать определенное количество значений используйте [take](take.md)

## Сигнатура

```ts
takeUntil<T>(notifier: Observable<any>): MonoTypeOperatorFunction<T>
```

## Описание

Подписывается на Observable `notifier` и как только `notifier` сообщает о том что он закрыт (то есть вызывает `complete`), `takeUntil` вызывает `complete` у исходного Observable.


