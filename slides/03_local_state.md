# Local State

We want to make a page interactive. How can React know that the page needs to be re-rendered because
for example some displayed data has changed after the user clicked on a button?
How can React "remember" data when a component renders again?

Such data is called state. You can add it to any component with a special function `useState()`.

### Usage of `useState()`
```
const [counter, setCounter] = useState<number>(0);
```

* The initial value of the state is passed as an argument to `useState`. This is optional, if you don't pass in an argument the state will initially be undefined.
* The function returns an array with two elements, the current state and a setter function to update the state.
    * Hint: The syntax `const [counter, setCounter] = ...` is called *array destructuring* and means that we assign the first
      element of the array to a variable `counter` and the second one to a variable called `setCounter`. It is a shorter way of
      writing:
       ```
       const useStateReturnValue = useState<number>(0);
       const counter = useStateReturnValue[0];
       const setCounter = useStateReturnValue[1]
       ```
* You can freely choose a name for the state variable and the setter. It is a convention to name the setter like the state but prefixed with `set`.
* If you use TypeScript, you can specify the state's type in angle brackets.

### Updating the state

* Do not modify state directly as it will not trigger a rerender. Always use the setter function returned by `useState()`.
    ```
    ❌ counter = 1;
    ✅ setCounter(1);
    ```
* State updates can be asynchronous.
    * If you require the state's previous value to calculate the new value, do not rely on the value of the state variable. It might not yet include other updates you have in your code. State updates can be asynchronous as multiple setter calls may be batched by React.
    * For this case, there is a second way to use the setter function. Instead of passing a value, you can pass in an *updater function*, which is a callback to calculate the new value from the previous value.
  ```
  ❌ setCounter(counter + 1);
  
  ✅ function increaseByOne(previousValue: number): number {
         return previousValue + 1;
      }
      setCounter(increaseByOne);
  ```

Full example:
```
function App() {
  const [counter, setCounter] = useState<number>(0);

  function increaseByOne(previousValue: number): number {
    return previousValue + 1;
  }

  function handleClick() {
    setCounter(increaseByOne);
  }

  function handleDoubleClick() {
    setCounter(increaseByOne);
    setCounter(increaseByOne);
  }

  function handleResetClick() {
    setCounter(0);
  }

  return (
    <div className="App">
      <h1>Number of clicks: {counter}</h1>
      <button onClick={handleClick}>Click</button>
      <button onClick={handleDoubleClick}>Double click</button>
      <button onClick={handleResetClick}>Reset counter</button>
    </div>
  );
}
```
You can try this out yourself in our CodeSandbox examples: 
* [Example that doesn't work because it relies on the value of the state variable having been updated already](https://codesandbox.io/s/react-state-why-does-double-click-not-work-ou3hnl?file=/src/App.tsx)
* [Fixed example that works because it passes an updater function to the setter function](https://codesandbox.io/s/react-state-double-click-fixed-vttbtf?file=/src/App.tsx)
* [Working example from above with both ways of using the setter function - updater function and value not depending on current state](https://codesandbox.io/s/react-state-full-example-rbct6z?file=/src/App.tsx)

### Passing state to child components

A component's state is not accessible to any other component. But a component may explicitly pass its state down to its child components via props (unidirectional data flow).

Example:

```
function ClickDisplay(props: { numberOfClicks: number }) {
  return <h1>Number of clicks: {props.numberOfClicks}</h1>;
}

function ClickButton(props: { handleClick: () => void }) {
  return <button onClick={props.handleClick}>Click here!</button>;
}

export default function App() {
  const [counter, setCounter] = useState<number>(0);

  function increaseByOne(previousValue: number) {
    return previousValue + 1;
  }

  function handleClick() {
    setCounter(increaseByOne);
  }

  return (
    <div className="App">
      <ClickDisplay numberOfClicks={counter} />
      <ClickButton handleClick={handleClick} />
    </div>
  );
}
```
[Link to Example in CodeSandbox](https://codesandbox.io/s/react-state-passing-state-to-child-components-458ubu?file=/src/App.tsx:58-693)

## Resources
[General concept of state in React](https://react.dev/learn/state-a-components-memory)

[useState hook](https://react.dev/reference/react/useState)