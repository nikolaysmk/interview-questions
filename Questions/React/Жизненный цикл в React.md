
### Методы жизненного цикла

1.  `componentWillMount()` - вызывается перед тем, как компонент будет отображен на странице. Этот метод может быть использован для инициализации каких-то данных, которые требуются компоненту.
2.  `componentDidMount()` - вызывается после того, как компонент был отображен на странице. Этот метод может быть использован для выполнения каких-то действий после того, как компонент был установлен.
3.  `componentWillReceiveProps(nextProps)` - вызывается, когда компонент получает новые свойства (props). Этот метод может быть использован для обновления состояния компонента на основе новых свойств.
4.  `shouldComponentUpdate(nextProps, nextState)` - вызывается перед обновлением компонента и позволяет определить, нужно ли обновлять компонент. Этот метод может быть использован для оптимизации производительности, чтобы избежать ненужных перерисовок компонента.
5.  `componentWillUpdate(nextProps, nextState)` - вызывается перед обновлением компонента. Этот метод может быть использован для подготовки компонента к обновлению.
6.  `componentDidUpdate(prevProps, prevState)` - вызывается после обновления компонента. Этот метод может быть использован для выполнения каких-то действий после обновления компонента.
7.  `componentWillUnmount()` - вызывается перед тем, как компонент будет удален. Этот метод может быть использован для очистки каких-то ресурсов, которые были заняты компонентом.
