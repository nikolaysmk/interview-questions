#debug #react #hook

#useRenderCount
```jsx
export default function useRenderCount() {
    const renderCount = useRef(1)
    useEffect(() => {
        renderCount.current = renderCount.current + 1;
        return (() => {
            console.warn(`cleanup after renderCount ${renderCount.current}`);
        });
    });
    return renderCount.current;
}
```

How use
```jsx
const renderCount = useRenderCount();
console.warn(`Render count: ${renderCount}`);
```
