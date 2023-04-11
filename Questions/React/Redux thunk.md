`Action` -> `Dispatch` -> `Thunk` -> `Reducer` -> `Store`

`Redux Thunk` - это средство, которое позволяет в `Redux` создавать `Action Creator`'ы, которые возвращают не только объекты `Action`, но и функции. Возвращаемая функция может выполнять асинхронные операции и диспетчеризовать один или несколько объектов `Action`, когда операция завершена.

Для работы с `Redux Thunk` нужно добавить `redux-thunk` в приложение и применить middleware в `store`. Middleware - это функция, которая обрабатывает `Action`, прежде чем он дойдет до `Reducer`. Middleware может изменять `Action`, пропускать его дальше или диспетчеризовать несколько `Action`'ов. `Redux Thunk` - это middleware, который позволяет обрабатывать функции `Action Creator`.

Рассмотрим пример. Пусть у нас есть приложение, которое получает данные о пользователе из API и затем обновляет состояние приложения с полученными данными. Мы можем создать `Action Creator`, который получает данные из API и диспетчеризует `Action`, когда данные получены:

javascriptCopy code

```js
import axios from 'axios';

export const fetchUser = (userId) => {
  return (dispatch) => {
    dispatch({ type: 'FETCH_USER_REQUEST' });
    axios.get(`https://jsonplaceholder.typicode.com/users/${userId}`)
      .then(response => {
        dispatch({ type: 'FETCH_USER_SUCCESS', payload: response.data });
      })
      .catch(error => {
        dispatch({ type: 'FETCH_USER_FAILURE', payload: error });
      });
  };
};

```

Здесь мы определяем функцию `fetchUser`, которая принимает `userId` в качестве параметра. Функция возвращает функцию, которая принимает `dispatch` в качестве параметра. Эта возвращаемая функция делает запрос к API, используя библиотеку `axios`, и диспетчеризует объекты `Action` в зависимости от результата запроса. В данном случае, когда данные получены успешно, мы диспетчеризуем объект `Action` с типом `FETCH_USER_SUCCESS` и передаем в него полученные данные в свойстве `payload`. Если запрос не удался, мы диспетчеризуем объект `Action` с типом `FETCH_USER_FAILURE` и передаем в него ошибку.

Теперь мы можем использовать этот `Action Creator` для получения данных о пользователе из API и обновления состояния приложения:

scssCopy code

```js
dispatch(fetchUser(userId));
```

В результате этого вызова будут выполнены запросы к API, и когда данные будут получены, соответствующий объект `Action` будет отправлен в `Reducer` для обновления состояния приложения.

Таким образом, `Redux Thunk` позволяет создавать `Action Creator`'ы, которые могут выполнять асинхронные операции и диспетчер



