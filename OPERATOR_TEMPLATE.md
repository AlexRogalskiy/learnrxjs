# Название оператора

## Сигнатура

```typescript
hello(str: string, scheduler)
```

## Описание

## Параметры

- `str`
  
  Пример описания оператора

- ~~`scheduler`~~ *Depricated*

  Параметр с флагом depricated

## Примеры

### Пример 1: краткое описани

```typescript
// RxJS v6+
import { endWith } from 'rxjs/operators';
import { of } from 'rxjs';

const source$ = of('Hello', 'Friend');

source$
  // emit on completion
  .pipe(endWith('Goodbye', 'Friend'))
  // 'Hello', 'Friend', 'Goodbye', 'Friend'
  .subscribe(console.log(val));
```

## Полезные ссылки

- 📰 Официальная документация: [OPERATOR_NAME](OPERATOR_URL)
- 📁 Исходный код: https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/OPERATOR_NAME.ts

