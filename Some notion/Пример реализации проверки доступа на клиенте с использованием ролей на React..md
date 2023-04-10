#withAuth #аутентификация 
В React для защиты маршрутов можно использовать компоненты высшего порядка (Higher Order Components, HOC) и hooks. Например, для проверки прав доступа на клиентской стороне можно создать HOC, который будет проверять, имеет ли текущий пользователь права доступа к маршруту. Вот пример реализации HOC на React
```jsx
import React from 'react';
import { Redirect } from 'react-router-dom';
import authService from './authService';

export const withAuth = (Component, roles) => {
  return class extends React.Component {
    render() {
      const currentUser = authService.getCurrentUser();
      if (currentUser && (!roles || roles.some(role => currentUser.roles.includes(role)))) {
        return <Component {...this.props} />;
      } else {
        return <Redirect to={{ pathname: '/login', state: { from: this.props.location } }} />;
      }
    }
  };
};

```

Здесь мы создаем HOC `withAuth`, который принимает компонент, который нужно защитить, и массив ролей, которым разрешен доступ к маршруту. Если пользователь авторизован и его роли соответствуют разрешенным, то HOC возвращает компонент. В противном случае он перенаправляет пользователя на страницу авторизации с помощью компонента `Redirect` из `react-router-dom`.

Затем мы можем использовать этот HOC для защиты нужных маршрутов. Например, если у нас есть маршрут `/admin`, доступный только пользователям с ролью `admin`, мы можем создать компонент `AdminPage` и защитить его с помощью HOC `withAuth`:
```jsx
import React from 'react';
import { withAuth } from './withAuth';

const AdminPage = (props) => {
  return (
    <div>
      <h1>Admin Page</h1>
      <p>Welcome, {props.currentUser.username}!</p>
    </div>
  );
};

export default withAuth(AdminPage, ['admin']);

```

Здесь мы экспортируем компонент `AdminPage`, обернутый в HOC `withAuth`. Мы также передаем массив ролей, которым разрешен доступ к этому маршруту (в данном случае только роль `admin`). Внутри компонента мы можем использовать информацию о текущем пользователе, переданную через пропсы.

Вместо HOC также можно использовать hooks для проверки прав доступа на клиентской стороне. Например, с помощью хука `useEffect` мы можем проверять права доступа при каждом изменении маршрута и перенаправлять пользователя, если он не авторизован или не имеет нужных прав доступа.