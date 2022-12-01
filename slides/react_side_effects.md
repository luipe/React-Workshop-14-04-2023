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
import { useEffect } from "react";

const AnnoyMe = () => {
  useEffect(() => {
    const eventListener = function () {
      window.alert("You clicked!");
    };
    document.addEventListener("click", eventListener);
    return () => document.removeEventListener("click", eventListener);
  });

  return null;
};
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

const HelloExternalWorld = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch(
        "https://external-click-counter.com/howmanyofthoseclickswegot"
      );
      const parsedResponse = await response.json();
      setCount((previous) => previous + parsedResponse.numberOfClicks);
    };
    fetchData();
  }, []);

  return (
    <div onClick={() => setCount((previous) => previous + 1)}>
      <h1>Hello World!</h1>
      <p>Click count: {count}</p>
    </div>
  );
};
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

----

## Component Lifecycle - Update

<figure>
  <img src="img/ComponentLifecycle-update.png" style="box-shadow: none" alt="component update"/>
</figure>

----

## Component Lifecycle - Unmount

<figure>
  <img src="img/ComponentLifecycle-unmount.png" style="box-shadow: none" alt="component unmount"/>
</figure>

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

## Memory Game - with cat pics!

### VI. Card Images

- Instead of a boring text, memory cards should show cute cats
- Images can be rendered in HTML as `img` tag with image URL
  - example: `<img src="https://cataas.com/cat/A55LPR38NHRPPQhU" />`
- We can retrieve image URLs of cats from https://cataas.com
  - API documentation: https://cataas.com/doc.html
  - `https://cataas.com/cat?json=true`
    - returns a JSON object with a `"url"` property, e.g. `"cat/A55LPR38NHRPPQhU"`
- _Optional_: explore further query parameters and tag options (e.g. `cute`) of the API

----

## Memory Game - with cat pics!

### Hint - asynchronous fetching method

```tsx
const catProviderUrl = "https://cataas.com";

const fetchCatUrl = async (): Promise<string> => {
  const rawResponse = await fetch(`${catProviderUrl}/cat?json=true`);
  const jsonResponse = await rawResponse.json();
  return catProviderUrl + jsonResponse.url;
};
```

----

## Supplementary

### Custom Hooks

- Existing hooks (basic or other custom ones) can be used to compose a custom hook.
- Custom Hooks may have input parameters and any return value
- Allow us to reuse logic and keep components simple and clean
- Plethora of custom hooks are already out there waiting to be _use_-d

  - Example: https://github.com/streamich/react-use
