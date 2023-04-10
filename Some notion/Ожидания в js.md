
### Таймер
#setTimeout
```js
console.log("first call!");

setTimeout(function() {
	console.log("in 5 sec");
}, 5000);


clearTimeout(name_of_setTimeout)
```

### Повторяющийся вызов
#setInterval
```js
setInterval(function() {
	console.log("Spawn New Enemy!");
}, 3000);

setInterval(function() {
	console.log("Spawn Power Up!");
}, 4000);


clearInterval(nameOfInterval)

```

### Функция ожидания 
#waitInJs
```js
function wait(t) {
 return new Promise((resolve) => {
	  setTimeout(resolve, 1000 * t);
	  });
}


console.log("1");
wait(2)
	.then(() => console.log("3"))
	.then(() => wait(2))
	.then(() => console.log("4"));

console.log("2");
```


### setTimeout in React
#setTimeout #react 
```js

useEffect(() => { 
	const timer = setTimeout(() => { console.log('This will run after 1 second!') }, 1000); 
	return () => clearTimeout(timer); }
	, []);

```




### setInterval in React
#setInterval #react 
```js
 useEffect(() => { 
	const interval = setInterval(() => { 
		setSeconds(seconds => seconds + 1); 
	}, 1000); 
	return () => clearInterval(interval); }
, []);
	```


debounce - > ожидает допустим 5 секунд, после последнего нажатия кнопки

throttle  -> вызывается допустим каждый 5 секунд