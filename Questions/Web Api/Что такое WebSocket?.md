WebSocket - это протокол связи поверх TCP-соединения, предназначенный для обмена сообщениями между браузером и веб-сервером, используя постоянное соединение³. WebSocket позволяет создавать и управлять веб-сокет-подключением к серверу, а также отправлять и получать данные в этом подключении². WebSocket поддерживает полнодуплексную коммуникацию, то есть данные могут передаваться в обоих направлениях одновременно⁴.

Для создания WebSocket-объекта используется конструктор WebSocket(), который принимает URL-адрес сервера и необязательный параметр протоколов². Например:

```javascript
const socket = new WebSocket('ws://localhost:8080');
```

WebSocket-объект имеет ряд свойств и методов, таких как:

- **binaryType** - тип двоичных данных, которые будут переданы по соединению¹.
- **bufferedAmount** - количество байтов данных, которые были поставлены в очередь, но ещё не переданные в сеть².
- **close()** - закрывает соединение².
- **onclose** - обработчик события, вызываемый при закрытии соединения².
- **onerror** - обработчик события, вызываемый при возникновении ошибки².
- **onmessage** - обработчик события, вызываемый при получении сообщения с сервера².
- **onopen** - обработчик события, вызываемый при открытии соединения².
- **protocol** - имя подпротокола, выбранного сервером².
- **readyState** - текущее состояние подключения².
- **send()** - отправляет данные на сервер².
- **url** - абсолютный URL сервера².

WebSocket имеет четыре константы состояния готовности:

- **WebSocket.CONNECTING** (0) - соединение ещё не установлено².
- **WebSocket.OPEN** (1) - соединение установлено и готово к обмену данными².
- **WebSocket.CLOSING** (2) - соединение закрывается².
- **WebSocket.CLOSED** (3) - соединение закрыто или не было установлено².


```jsx
import React, { useState, useRef, useEffect } from "react";

const AppWs = () => {
    const [isPaused, setIsPaused] = useState(false);
    const [data, setData] = useState(null);
    const [status, setStatus] = useState("");
    const ws = useRef(null);

    useEffect(() => {
        const gettingData = (e) => {
            if (isPaused) return;
            const message = JSON.parse(e.data);
            setData(message);
        };

        if (!isPaused) {
            ws.current = new WebSocket("wss://ws.kraken.com/"); // создаем ws соединение
            ws.current.onopen = () => setStatus("Соединение открыто");  // callback на ивент открытия соединения
            ws.current.onclose = () => setStatus("Соединение закрыто"); // callback на ивент закрытия соединения
            ws.current.onmessage = gettingData; //подписка на получение данных по вебсокету
        }

        return () => {
            if (ws.current) {
                ws.current.close(); // кода меняется isPaused - соединение закрывается
            }
        };
    }, [isPaused]);

    return (
        <>
            {!!data &&
                <div>
                    <div>
                        <h2>{status}</h2>
                        <p>{`connection ID: ${data?.connectionID}`}</p>
                        <p>{`event: ${data?.event}`}</p>
                        <p>{`status: ${data?.status}`}</p>
                        <p>{`version: ${data?.version}`}</p>
                    </div>
                    <button onClick={() => {
                        if (ws.current) {
                            ws.current.close();
                        }
                        setIsPaused(!isPaused)
                    }}>{!isPaused ? 'Остановить соединение' : 'Открыть соединение' }</button>
                </div>
            }
        </>
    )
}

export default AppWs;

```