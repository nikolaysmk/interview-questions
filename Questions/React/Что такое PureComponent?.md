PureComponent – это базовый класс для компонентов React, основанных на классах. 
Он реализует метод жизненного цикла **shouldComponentUpdate** таким образом
, что он пропускает повторные рендеры для одинаковых пропсов и состояния. Это означает, что компонент считается чистым, если он рендерит одинаковый вывод для одинаковых пропсов и состояния **PureComponent** может улучшить производительность React-приложения, избегая ненужных рендеров
Однако **PureComponent** не подходит для всех случаев, так как он использует поверхностное сравнение пропсов и состояния, которое может пропустить некоторые изменения.


Вот несколько примеров использования PureComponent в React:

- Создание компонента Greeting, который пропускает повторные рендеры, если пропс name не меняется¹:

```jsx
import { PureComponent } from 'react';

class Greeting extends PureComponent {
  render() {
    return <h1>Привет, {this.props.name}!</h1>;
  }
}
```

- Создание компонента Counter, который обновляет своё состояние при клике на кнопку²:

```jsx
import { PureComponent } from 'react';

class Counter extends PureComponent {
  constructor(props) {
    super(props);
    this.state = { count: 1 };
  }

  render() {
    return (
      <button
        color={this.props.color}
        onClick={() => this.setState(state => ({ count: state.count + 1 }))}
      >
        Счётчик: {this.state.count}
      </button>
    );
  }
}
```

- Создание компонента App, который передаёт пропс name компоненту Greeting и пропс address компоненту Address. Заметьте, что Greeting не рендерится заново, если меняется только address¹:

```jsx
import { PureComponent, useState } from 'react';

class Greeting extends PureComponent {
  render() {
    console.log('Greeting was rendered at', new Date().toLocaleTimeString());
    return <h3>Привет{this.props.name && ', '}{this.props.name}!</h3>;
  }
}

class Address extends PureComponent {
  render() {
    console.log('Address was rendered at', new Date().toLocaleTimeString());
    return <p>Адрес: {this.props.address}</p>;
  }
}

export default function App() {
  const [name, setName] = useState('');
  const [address, setAddress] = useState('');

  return (
    <>
      <label>
        Имя: <input value={name} onChange={e => setName(e.target.value)} />
      </label>
      <label>
        Адрес: <input value={address} onChange={e => setAddress(e.target.value)} />
      </label>
      <Greeting name={name} />
      <Address address={address} />
    </>
  );
}
```


Аналогом PureComponent для функциональных компонентов, использующих хуки, является React.memo. Эта функция оборачивает функциональный компонент и возвращает новый компонент, который пропускает повторные рендеры, если пропсы не изменились¹². React.memo принимает второй аргумент — функцию сравнения пропсов, которая позволяет определить, нужно ли рендерить компонент или нет¹. Например:

```jsx
import React, { memo } from 'react';

function Greeting(props) {
  return <h1>Привет, {props.name}!</h1>;
}

// Оборачиваем компонент в React.memo
export default memo(Greeting);
```

В этом случае компонент Greeting не будет рендериться заново, если пропс name останется тем же. Если же мы хотим сравнивать пропсы по-другому, мы можем передать функцию сравнения вторым аргументом:

```jsx
import React, { memo } from 'react';

function Greeting(props) {
  return <h1>Привет, {props.name}!</h1>;
}

// Оборачиваем компонент в React.memo и передаём функцию сравнения
export default memo(Greeting, (prevProps, nextProps) => {
  // Возвращаем true, если пропсы равны по длине
  return prevProps.name.length === nextProps.name.length;
});
```

В этом случае компонент Greeting не будет рендериться заново, если длина пропса name не изменится. Это может быть полезно для оптимизации производительности в некоторых ситуациях.
