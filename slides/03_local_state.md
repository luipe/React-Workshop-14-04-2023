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
  ✅ setCounter((previousCounter) => previousCounter + 1);
  ```

Full example:
```
const App = () => {
  const [counter, setCounter] = useState<number>(0);

  return (
    <div>
      <h1>Number of clicks: {counter}</h1>
      <button onClick={() => {
        setCounter((previousCounter) => previousCounter + 1); 
        setCounter((previousCounter) => previousCounter + 1); 
        }}>Double click!</button>
      <button onClick={() => setCounter(0)}>Reset counter</button>
    </div>
  );
}
```

### Passing state to child components

A component's state is not accessible to any other component. But a component may explicitly pass its state down to its child components via props (unidirectional data flow).

Example:

```
const ClickDisplay = (props: {numberOfClicks: number}) => (
  <h1>Number of clicks: {props.numberOfClicks}</h1>
);

const ClickButton = (props: {handleClick: () => void}) => (
  <button onClick={props.handleClick}>Click here!</button>
);

const App = () => {
  const [counter, setCounter] = useState<number>(0);

  return (
    <div>
      <ClickDisplay numberOfClicks={counter}/>
      <ClickButton handleClick={() => setCounter((previousCounter) => previousCounter + 1)}/>
    </div>
  );
}
```

## Resources
[General concept of state in React](https://react.dev/learn/state-a-components-memory)

[useState hook](https://react.dev/reference/react/useState)