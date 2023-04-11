# React Overview and Components

## Traditional web development
* HTML, CSS and Javascript in separate files
* See example: https://codesandbox.io/s/inspiring-matsumoto-cv15w8?file=/index.html

### Problems
* Complexity and readability

    * Distributed logic (CSS, HTML, JS)

* Duplication of code and logic
* Hard to maintain

    * Difficult to understand the data flow within

### More complex website
<figure style="width: 100%">
  <img src="img/facebookTng.jpg" style="width: 100%; box-shadow: none"/>
</figure>

Would be better to:
* Structure the page in logical **components**
* Have file per component, including styling and interactivity
* Re-use components as needed

=> Those are (some of) the goals of React

## What is React?

JavaScript library (or toolkit) to build user interfaces

### Timeline

* 2011 developed at Facebook
* 2012 used at Instagram
* 2013 Open Source
* current version (2023): React 18
* still actively developed


### Main concepts
* components
    * nested, styled, configurable & reusable
* unidirectional data flow
    * data flows only from parent to child components via props
* virtual DOM
    * DOM
        * Document Object Model = internal representation of the webpage
        * independent of platform or language
    * virtual:
        * Dynamically generated from JS, not a static HTML file
* JSX / TSX
    * Javascript (Typescript) Syntax Extension
    * looks like HTML
    * produces elements for the DOM


## My first React component

Example code:
https://codesandbox.io/s/romantic-pine-uin9dl?file=/src/App.tsx

React component *Hello World*
```tsx
function HelloWorld() {
  return <h1>Hello World!</h1>;
}
```
as a so-called *functional component*


### Inclusion in DOM
```tsx
ReactDOM.render(<HelloWorld />, document.getElementById('root'));
```

* element tagged as `root` in DOM (index.html)
* entry point for React to render translated result


### Browser Output
<figure style="width: 100%">
  <img src="img/codeExamples/HelloWorld.jpg" style="width: 100%; box-shadow: none; border: 5px solid black"/>
</figure>


## **Exercise 1**: Create Code Sandbox

(see exercise slide)

----

## What files do you see?

**public**
* **index.html** entry point of web page

**src**
* **App.tsx** The main React component
* **index.tsx** inclusion of component in DOM
* **styles.css** style sheet

**root folder**
* **package.json** dependencies to packages
* **tsconfig.json** typescript configuration


----

## React components

*What we know now:*
* building blocks of the application

*What we will learn:*
* **JSX** syntax
* configuration via **props**
* can have their own (local) **state**

*Further information*
* styling using Inline-Styles or **css**

## JSX Syntax

* expressions with HTML-like syntax
```tsx
    <h1>Hello World!</h1> 
```

* using components (like HTML tags)
```tsx
    <div className="App">
      <HelloWorld />
      <p>Some other text</p>
    </div>
```

* Inline Typescript expressions
```tsx
    const name = 'John Doe';
    
    return <h1>Hello {name}!</h1>;
```

* Conditional and functional expressions (no if/else or for-loops)
```tsx
    return <h1>Hello {name !== undefined ? <b>{name}</b> : <b>unknown</b>}!</h1>;
```

* Another example: Flip a coin
```tsx
function CoinFlip() {
    const randomValue = Math.random();

    return <div>The coin landed on {randomValue > 0.5 ? 'head' : 'tail'}.</div>;
}
```
Include in the main application:
```tsx
    <div className="App">
      <CoinFlip />
    </div>
```

----

To remember:
* Everything before the `return` is Typescript
* Inside the `return`, it's HTML-like syntax
* Use braces `{}` to include Typescript inside the HTML-like part
