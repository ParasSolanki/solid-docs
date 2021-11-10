Мы видели, что всякий раз, когда мы обращаемся к `Сигналу` в JSX, он автоматически обновляет UI при изменении этого `Сигнала`. Но сама функция компонента выполняется только один раз.

Мы можем создавать новые выражения, которые зависят от `Сигналов`, оборачивая его в функцию. Функция, которая обращается к `Сигналу`, сама является `Сигналом`: когда внутренний `Сигнал` изменяется, обновляются и его считыватели.

Введем функцию `doubleCount`, удваивающую наш счетчик:

```jsx
const doubleCount = () => count() * 2;
```

Затем мы можем вызвать `doubleCount` точно так же, как `Cигнал` в нашем JSX:

```jsx
return <div>Count: {doubleCount()}</div>;
```

Мы называем подобные функции `производными Сигналами` (`deferred Signal`), потому что они получают свою реактивность от `Сигнала`, к которому они обращаются. Сами они не хранят значение (если вы создаете производный `Сигнал`, но никогда не вызываете его, он будет удален из компилированного кода Solid, как и любая неиспользуемая функция), но они обновят любые `Эффекты`, которые зависят от них, и вызовут ьь, если эти `Сигналы` включены в представление.