`Action` -> `Dispatch` -> `Thunk` -> `Reducer` -> `Store`

Рассмотрим пример использования `Redux Thunk`. Допустим, мы хотим получить список пользователей из удаленного API и сохранить его в состоянии приложения. Вот как это можно сделать:

1.  Создаем `Action Creator`, который будет отправлять запрос на сервер и диспетчеризовать соответствующие `Action`'ы в зависимости от результата запроса:
```js
import axios from 'axios';

export const fetchUsers = () => {
  return async (dispatch) => {
    dispatch({ type: 'FETCH_USERS_REQUEST' });

    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/users');
      dispatch({ type: 'FETCH_USERS_SUCCESS', payload: response.data });
    } catch (error) {
      dispatch({ type: 'FETCH_USERS_FAILURE', payload: error.message });
    }
  };
};

```

2.  Диспетчеризуем этот `Action Creator` в компоненте React:
```jsx
import React, { useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { fetchUsers } from './actions';

const UserList = () => {
  const dispatch = useDispatch();
  const users = useSelector(state => state.users);

  useEffect(() => {
    dispatch(fetchUsers());
  }, [dispatch]);

  return (
    <div>
      {users.loading ? (
        <h2>Loading...</h2>
      ) : users.error ? (
        <h2>{users.error}</h2>
      ) : (
        <div>
          <h2>User List</h2>
          <div>
            {users && users.data && users.data.map(user => (
              <p key={user.id}>{user.name}</p>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default UserList;

```
В этом компоненте мы используем `useDispatch` из `react-redux` для диспетчеризации `Action`'а `fetchUsers` и `useSelector` для получения списка пользователей из состояния приложения. Мы вызываем `fetchUsers` в функции `useEffect`, чтобы получить список пользователей при загрузке компонента.

3.  Обрабатываем `Action` в `Reducer`'е:
```js
const initialState = {
  loading: false,
  data: [],
  error: '',
};

const usersReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'FETCH_USERS_REQUEST':
      return {
        ...state,
        loading: true,
      };
    case 'FETCH_USERS_SUCCESS':
      return {
        loading: false,
        data: action.payload,
        error: '',
      };
    case 'FETCH_USERS_FAILURE':
      return {
        loading: false,
        data: [],
        error: action.payload,
      };
    default:
      return state;
  }
};

export default usersReducer;

```

Здесь мы определяем начальное состояние `initialState` и обрабатываем три типа `Action`: `FETCH_USERS_REQUEST`, `FETCH_USERS_SUCCESS`, и `FETCH_USERS_FAILURE`. В зависимости от типа `