Есть несколько способов отрендерить HTML код в React-компоненте¹²³:

- Использовать свойство `dangerouslySetInnerHTML`, которое позволяет вставить HTML код в виде строки внутрь компонента. Этот способ называется опасным, потому что он может привести к атакам XSS, если вы не доверяете источнику HTML кода. Например:

```jsx
<div dangerouslySetInnerHTML={{__html: '<p>Привет, <b>мир</b>!</p>'}} />
```

- Использовать стороннюю библиотеку, которая может преобразовать HTML код в JSX элементы без использования `dangerouslySetInnerHTML`. Например, библиотека `html-to-react` или `react-render-html`. Например:

```jsx
import { Parser } from 'html-to-react';

const html = '<p>Привет, <b>мир</b>!</p>';

const App = () => {
  return (
    <div>
      {Parser().parse(html)}
    </div>
  );
};
```

- Использовать JSX синтаксис для написания HTML кода в виде React элементов. Это самый рекомендуемый способ, так как он позволяет использовать все преимущества React и избежать проблем с безопасностью и производительностью. Например:

```jsx
<div>
  <p>Привет, <b>мир</b>!</p>
</div>
```

\