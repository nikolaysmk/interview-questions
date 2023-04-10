#redux

# Три принципа

Redux можно описать в трех фундаментальных принципах:

### Единый источник истины

### Состояние доступно только для чтения
### Изменения вносятся с помощью чистых функций


```js
type State = any
type Action = Object
type Reducer<S, A> = (state: S, action: A) => S

type BaseDispatch = (a: Action) => Action
type Dispatch = (a: Action | AsyncAction) => any

type MiddlewareAPI = { dispatch: Dispatch, getState: () => State }
type Middleware = (api: MiddlewareAPI) => (next: Dispatch) => Dispatch


type Store = {  
	dispatch: Dispatch  
	getState: () => State  
	subscribe: (listener: () => void) => () => void  
	replaceReducer: (reducer: Reducer) => void  
}
	
type StoreCreator = (reducer: Reducer, preloadedState: ?State) => Store

type StoreEnhancer = (next: StoreCreator) => StoreCreator
```

_**Store**_ — это состояние веб-компонента, которое хранит в себе всю информацию (или ту которую вы решили сохранить в него). В дальнейшем стор будет доступен из любого компонента вашего приложения.

_**Action**_ — действие, описывает что нужно сделать. Согласно принципам функционального программирования, мы не можем изменять объект напрямую, поэтому нам нужны экшены, чтобы передать их в диспатчер и «сказать», что нужно сделать.

_**Dispatcher**_ — сообщает хранилищу о каком-то действии (action) и передает ему обновленную информацию.

Основные методы для работы со store

-   _store.dispatch()_ — диспатч какого-либо экшена
-   _store.getState()_ — получение данных, которые хранятся в store
-   _store.subscribe()_ — подписка на изменения store.

-   useDispatch() — замена для mapDispatchToProps(). Этот хук возвращает dispatch метод. С его помощью мы потом можем диспатчить нужные экшены.
-   useSelector() — аналог mapStateToProps() — Этот хук принимает колбэк, который в качестве аргумента принимает текущий state. Вы можете вернуть весь state или какие-то определенные данные из него.
-   useStore() — этот хук возвращает ссылку на тот же state, который был передан в <Provider>. В документации редакса говорится о том, что лучше этот хук не использовать часто, а лучше пользоваться useSelector()

