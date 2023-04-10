Допустим, у нас есть компонент `Counter`, который отображает счетчик и имеет две кнопки: одну для увеличения значения счетчика, другую для уменьшения значения счетчика. Вот пример кода компонента `Counter`:

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const incrementCount = () => {
    setCount(count + 1);
  };

  const decrementCount = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <h2>Counter</h2>
      <p>Count: {count}</p>
      <button onClick={incrementCount}>+</button>
      <button onClick={decrementCount}>-</button>
    </div>
  );
};

export default Counter;

```

Теперь давайте напишем тест для этого компонента с использованием Jest. Наш тест будет проверять, что счетчик увеличивается при нажатии на кнопку "+", и уменьшается при нажатии на кнопку "-". Вот пример кода теста:

```js
import React from 'react';
import { render, fireEvent } from '@testing-library/react';
import Counter from './Counter';

describe('Counter component', () => {
  it('increments count when the + button is clicked', () => {
    const { getByText, getByRole } = render(<Counter />);
    const incrementButton = getByText('+');
    const countDisplay = getByRole('heading', { level: 2 });
    fireEvent.click(incrementButton);
    expect(countDisplay).toHaveTextContent('Count: 1');
  });

  it('decrements count when the - button is clicked', () => {
    const { getByText, getByRole } = render(<Counter />);
    const decrementButton = getByText('-');
    const countDisplay = getByRole('heading', { level: 2 });
    fireEvent.click(decrementButton);
    expect(countDisplay).toHaveTextContent('Count: -1');
  });
});

```

В первом тесте мы получаем кнопку "+" и элемент, содержащий значение счетчика, затем имитируем клик на кнопке "+" и проверяем, что значение счетчика увеличилось на 1. Во втором тесте мы делаем то же самое, только с кнопкой "-" и проверяем, что значение счетчика уменьшилось на 1.