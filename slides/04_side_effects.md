# Side Effects

### useEffect Hook

- Runs after every render by default (initial mount and updates)
- Example use cases

  - Data fetching
  - Setting up a subscription
  - Manually changing the DOM

----

## useEffect Hook

#### Example: event listener

```tsx
import { useEffect, useState } from "react";
import CatSvg from "./CatSvg";

export default function CursorCat() {
  const [position, setPosition] = useState<{ x: number; y: number }>();
  useEffect(() => {
    const eventListener = function (event: MouseEvent) {
      setPosition({
        x: event.clientX + 10,
        y: event.clientY + 10
      });
    };
    document.addEventListener("mousemove", eventListener);
    return () => document.removeEventListener("mousemove", eventListener);
  });

  return position ? <CatSvg x={position.x} y={position.y} /> : null;
}
```

[CodeSandbox example](https://codesandbox.io/s/proud-morning-ot5f8p?file=/src/App.js)

----

## useEffect Hook

#### Example: document modification

```tsx
import { useEffect, useState } from "react";

const HelloWorld = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div onClick={() => setCount((previous) => previous + 1)}>
      <h1>Hello World!</h1>
      <p>Click count: {count}</p>
    </div>
  );
};
```

[CodeSandbox example](https://codesandbox.io/s/serene-swartz-4olw34?file=/src/App.js)

----

## useEffect Hook

#### Example: fetch data

```tsx
import { useEffect, useState } from "react";
import "./styles.css";
import {Beer} from "./types";

export default function App() {
  const [beer, setBeer] = useState<Beer>();
  useEffect(() => {
    const fetchBeer = async () => {
      const response = await window.fetch(
              "https://random-data-api.com/api/v2/beers"
      );
      const parsedResponse = (await response.json()) as Beer;
      setBeer(parsedResponse);
    };
    fetchBeer();
  }, []);

  return (
          <div>
            <h1>Today's beer </h1>
            {beer ?
                    Object.entries(beer).map(([key, val]) => (
                            <div>
                              <b>{key}: </b>
                              <span>{val}</span>
                            </div>
                    )) : null}
          </div>
  );
}

```

[CodeSandbox example](https://codesandbox.io/s/frosty-microservice-sjzh00?file=/src/App.js)

----

## Component Lifecycle

- **Mount**
  - new component should be rendered
  - first call to function component
- **Update**
  - when props or local state changes
  - subsequent call to function component
- **Unmount**
  - component should be removed

----

## Component Lifecycle - Mount

<figure>
  <img src="img/ComponentLifecycle-mount.png" style="box-shadow: none" alt="component mount"/>
</figure>

[CodeSandbox example](https://codesandbox.io/s/quizzical-tree-ueyvzm?file=/src/App.tsx)
----

## Component Lifecycle - Update

<figure>
  <img src="img/ComponentLifecycle-update.png" style="box-shadow: none" alt="component update"/>
</figure>

[CodeSandbox example](https://codesandbox.io/s/quizzical-tree-ueyvzm?file=/src/App.tsx)
----

## Component Lifecycle - Unmount

<figure>
  <img src="img/ComponentLifecycle-unmount.png" style="box-shadow: none" alt="component unmount"/>
</figure>

[CodeSandbox example](https://codesandbox.io/s/quizzical-tree-ueyvzm?file=/src/App.tsx)
----

## Rules of Hooks

- Hooks are JavaScript functions coupled to the lifecycle of a React component
- Their implementation imposes two important rules:
  - **Calls to Hooks are only allowed inside**
    - Function components
    - other (custom) hooks (named `use...`)
  - **All Hooks must be called on every render, and always in the same order**
    - Do not call hooks conditionally (if, early returns, loops, ...)
- These rules can be enforced via automatic code checks (linting)

----

## Supplementary

### Custom Hooks

- Existing hooks (basic or other custom ones) can be used to compose a custom hook.
- Custom Hooks may have input parameters and any return value
- Allow us to reuse logic and keep components simple and clean
- Plethora of custom hooks are already out there waiting to be _use_-d

  - Example: https://github.com/streamich/react-use
