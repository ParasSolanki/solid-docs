События в Solid это атрибуты с префиксом `on`. Они являются особенными в своем поведении. Во-первых, они не включаются в реактивные обертки. Во многих случаях очень тяжело объяснить разницу между `Сигналом` и слушателем события (`event handler`). В случае с событиями они вызываются и им не нужна реактивность они прикрепляются (`bound`) только единожды. Вы всегда можете сделать так, чтобы ваш слушатель выполнял различные операции, в зависимости от текущего состояния вашего приложения.

Стандартные UI события (которые всплывают и композируются (`composed`)) автоматически делегируются документу. Для улучшения перформанса при делегации Solid поддерживает синтаксис в виде массива, чтобы вызывать слушателя без создания дополнительных замыканий (`closures`):

```jsx
const handler = (data, event) => /*...*/

<button onClick={[handler, data]}>Click Me</button>
```

Например, давайте прикрепим слушатель на событие `mousemove`:

```jsx
<div onMouseMove={handleMouseMove}>
  The mouse position is {pos().x} x {pos().y}
</div>
```

Все `on` атрибуты не зависят от регистра, однако для сверки вы должны ориентироваться на названия с нижним регистром. Например, `onMouseMove` будет отслеживать событие `mousemove`. Если вам нужна поддержка других регистров или вы не хотите использовать делегацию событий, то вы можете использовать префикс `on:` чтобы использовать названия событий после двоеточия:

```jsx
<button on:DOMContentLoaded={() => /* Любое действие */} >Click Me</button>
```