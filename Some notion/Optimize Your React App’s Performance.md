#react #optimize #ОптимизацияReact

### 1. Использовать lighthouse

```bash
npm install -g lighthouse
lighthouse http://localhost:3000

```

### 2. Use React.Suspense and React.Lazy for Lazy Loading Components

#suspense #lazy

```js
import LazyComponent from "./LazyComponent";
const LazyComponent = React.lazy(() => import("./LazyComponent"));
```

```jsx
import React, { Suspense } from "react"; // Import React and the Suspense component
const LazyComponent = React.lazy(() => import("./LazyComponent")); // Import the lazy component
function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading....</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}
```

### 3. Memoising React Components with Memo

#Memo

```js
const Title = React.memo(() => {
  let eventUpdates = React.useRef(0);
  return (
    <div className="black-tile">
      <Updates updates={eventUpdates.current++} />
    </div>
  );
});
```

### 4. Tree-shaking

#Tree-shaking - это техника, используемая в современных приложениях JavaScript для удаления неиспользуемого кода из конечного пакета.

Это делается инструментом bundler, таким как #Webpack, во время процесса сборки. Когда вы импортируете модуль, бандлер будет включать только те части кода, которые действительно используются в вашем приложении.

### 5. Optimizing your images

- **_Compress your images_**
- **_Use the appropriate image format (правильный формат для изображения)_**
- **_Resize your images_**
- **_Lazy load your images_**
- **_Use responsive images_ ->** _Используйте атрибуты **srcset** и **sizes** _
