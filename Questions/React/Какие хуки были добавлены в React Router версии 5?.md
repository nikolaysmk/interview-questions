В React Router версии 5 были добавлены четыре хука, которые вы можете использовать в своих приложениях на React¹²³⁴:

- **useHistory** - позволяет получить доступ к объекту history, который содержит информацию о переходах между страницами.
- **useParams** - позволяет получить доступ к параметрам пути, например, /user/:id.
- **useLocation** - позволяет получить доступ к объекту location, который содержит информацию о текущем URL и состоянии маршрутизатора.
- **useRouteMatch** - позволяет проверить, соответствует ли текущий URL какому-либо пути, и получить информацию о совпадении.

Для использования этих хуков вам нужно импортировать их из пакета react-router-dom:

```js
import { useHistory, useParams, useLocation, useRouteMatch } from 'react-router-dom';
```

Затем вы можете вызывать их внутри своих функциональных компонентов и работать с возвращаемыми значениями. Например:

```js
function User() {
  const history = useHistory();
  const params = useParams();
  const location = useLocation();
  const match = useRouteMatch();

  return (
    <div>
      <h1>Пользователь {params.id}</h1>
      <p>Текущий URL: {location.pathname}</p>
      <p>Совпадение с путем /user/:id: {match ? 'да' : 'нет'}</p>
      <button onClick={() => history.goBack()}>Назад</button>
    </div>
  );
}
```

