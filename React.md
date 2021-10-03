# Packages
> - https://styled-components.com
> - https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/
> - https://medium.com/devinder/react-virtual-dom-vs-real-dom-23749ff7adc9
> - https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en

# Virtual DOM
The Virtual DOM is a light-weight abstraction of the DOM. You can think of it as a copy of the DOM, that can be updated without affecting the actual DOM. It has all the same properties as the real DOM object, but doesn’t have the ability to write to the screen like the real DOM. The virtual DOM gains it’s speed and efficiency from the fact that it’s lightweight. In fact, a new virtual DOM is created after every re-render.
Reconciliation is a process to compare and keep in sync the two files (Real and Virtual DOM). Diffing algorithm is a technique of reconciliation which is used by React.

> - https://reactjs.org/docs/reconciliation.html

### Is the Shadow DOM the same as the Virtual DOM?
No, they are different. The Shadow DOM is a browser technology designed primarily for scoping variables and CSS in web components. The virtual DOM is a concept implemented by libraries in JavaScript on top of browser APIs.

### How does updates work in React?
* On the first load, ReactDOM.render() will create the Virtual DOM tree and real DOM tree.

* As React works on Observable patterns, when any event(like key press, left click, api response, etc.) occurred, Virtual DOM tree nodes are notified for props change, If the properties used in that node are updated, the node is updated else left as it is.

* React compares Virtual DOM with real DOM and updates real DOM. This process is called Reconciliation. React uses Diffing algorithm techniques of Reconciliation.

* Updated real DOM is repainted on browser.

# Reconciliation
React compares the Virtual DOM with Real DOM. It finds out the changed nodes and updates only the changed nodes in Real DOM leaving the rest nodes as it is. This process is called Reconciliation.
https://miro.medium.com/max/1400/0*CVH4_wcWYAJBoGGA![image](https://user-images.githubusercontent.com/12700182/134735180-40beb6c1-1d8a-40fd-be90-bd5a6c34c453.png)

Generic Reconciliation methods have complexity of O(n3) . Normally we have thousands of nodes in any application. This will be too expensive to use generic methods.
React implements a heuristic O(n) algorithm based on two assumptions:
* Two elements of different types will produce different trees.
* The developer can hint at which child elements may be stable across different renders with a key prop.

# JSX Limitation 
> * you cant return more than one "root" JSX element(you also cant store more than one root JSX element in a variabel)
> * if we have two or more elements we can use Array instead of wrapping it with HTML tag, but if we use array then we need to add key prop to every array element 
> * In bigger apps you can easliy end up with tons of unnecessary <div>s (or other elements) which add no semantic meaning or structer to the page but are only there because of React's/JSX requirement
> * So that's simply more convenient and therefore typically we use the wrapping div. However with the wrapping div or generally any wrapping element a new problem arises. Now we can end up with div soup. So we can end up with a real DOM that's being rendered where you have many nested React Components and all those Components for various reasons need wrapping divs or have wrapping Components. And you have all these unnecessary divs being rendered into real DOM even though they're only there because of this requirement or this limitation of JSX. And this is not an unrealistic scenario. In bigger applications It's very possible that in your final HTML page which is being served to your end-users you have a lot of unnecessary divs or other elements which are only there because you needed them as wrappers even though they don't add any semantic or structural meaning to your page. Now of course you don't have to care about that you might be fine with that but it could break your styling. If you have a wrapping div somewhere and you use nested CSS selectors that div could break stylings. And even if it doesn't break your styling it's still not a good practice. You're rendering too many HTML elements and ultimately that also makes your application slower because the browser needs to render all those elements and React needs to check all those elements or at least some of those elements if content needs to change. So rendering unnecessary content is generally never a good idea in programming. Hence this wrapping div or this wrapping element approach is okay but not ideal.

 > ## to solve this issue we can create a wrapper component just return props. children to reduce unwanted HTML wrapping tags and to fulfill JSX requirements 
  ```
  const Wrapper = props =>{
    return props.children
  }
  export default Wrapper;
  ```
  
> ## React Fragments
  ```
  <React.Fragment></React.Fragment>
  or 
  <></>
  or 
  import React,{useState,Fragment} from 'react';
  <Fragment></Fragment>
  ```
> ## React Portals
![image](https://user-images.githubusercontent.com/12700182/135516883-a06290a6-ee2e-4d08-a1bd-8aac16e5f64f.png)
![image](https://user-images.githubusercontent.com/12700182/135516912-9a55dd40-dbb3-4357-aa01-12ef8692b9f5.png)
  we can achive this using react portals
![image](https://user-images.githubusercontent.com/12700182/135516943-4193c7d1-6a6c-48de-9b49-505a96ee019b.png)
 ```
  index.html
      <div id="backdrop-root"></div> 
      <div id="overlay-root"></div>
      <div id="root"></div>
 Model.js
  
import ReactDom from "react-dom";
const Backdrop = (props) => {
  return <div className={classes.backdrop} onClick={props.onConfirm}></div>;
};
const ModalOverlay = (props) => {
  return (
    <Card className={classes.modal}>
      <header className={classes.header}>
        <h2>{props.title}</h2>
        <div className={classes.content}>
          <p>{props.message}</p>
        </div>
        <footer className={classes.action}>
          <Button onClick={props.onConfirm}>Okay</Button>
        </footer>
      </header>
    </Card>
  );
};

const ErrorModal = (props) => {
  return (
    <React.Fragment>
      {ReactDom.createPortal(
        <Backdrop onConfirm={props.onConfirm} />,
        document.getElementById("backdrop-root")
      )}

      {ReactDom.createPortal(
        <ModalOverlay
          title={props.title}
          message={props.message}
          onConfirm={props.onConfirm}
        />,
        document.getElementById("overlay-root")
      )}
    </React.Fragment>
  );
};
export default ErrorModal;

 ```
> result in web
<img width="353" alt="image" src="https://user-images.githubusercontent.com/12700182/135518998-3bc4db6c-3bf2-45a2-958c-8299aeade98a.png">

#ref's
> References but the name in React is just ref,
> What do refs do? they allow us to get access to other DOM elements and work with them.
  
 
# What are React controlled components and uncontrolled components?
This relates to stateful DOM components (form elements) and the React docs explain the difference:

* A Controlled Component is one that takes its current value through props and notifies changes through callbacks like onChange. A parent component "controls" it by handling the callback and managing its own state and passing the new values as props to the controlled component. You could also call this a "dumb component".
 
* A Uncontrolled Component is one that stores its own state internally, and you query the DOM using a ref to find its current value when you need it. This is a bit more like traditional HTML.

Most native React form components support both controlled and uncontrolled usage:
```
// Controlled:
<input type="text" value={value} onChange={handleChange} />

// Uncontrolled:
<input type="text" defaultValue="foo" ref={inputRef} />
// Use `inputRef.current.value` to read the current value of <input>
```

 
# Diffing Algorithm
React first compares the two root elements. The behavior is different depending on the types of the root elements.

React compared the root DOM Elements Types.
* Elements of different types: Whenever the root elements have different types, React will tear down the old tree and build the new tree from scratch. Going from <a> to <img>, or from <Article> to <Comment>, or from <Button> to <div> — any of those will lead to a full rebuild. This will lead to component unmount and mount lifecycle calls too.
* DOM Elements Of The Same Type: When comparing two React DOM elements of the same type, React looks at the attributes of both, keeps the same underlying DOM node, and only updates the changed attributes.After handling the DOM node, React then recurses on the children. This will lead to component update lifecycle calls.

> A declarative style, like what react has, allows you to control flow and state in your application by saying "It should look like this". An imperative style turns that around and allows you to control your application by saying "This is what you should do".

## Recommended way to structure React projects?

> - https://www.robinwieruch.de/react-folder-structure
### Grouping by features or routes
One common way to structure projects is to locate CSS, JS, and tests together inside folders grouped by feature or route.
```
common/
  Avatar.js
  Avatar.css
  APIUtils.js
  APIUtils.test.js
feed/
  index.js
  Feed.js
  Feed.css
  FeedStory.js
  FeedStory.test.js
  FeedAPI.js
profile/
  index.js
  Profile.js
  ProfileHeader.js
  ProfileHeader.css
  ProfileAPI.js
  ```
  
### Grouping by file type
Another popular way to structure projects is to group similar files together, for example:
```
api/
  APIUtils.js
  APIUtils.test.js
  ProfileAPI.js
  UserAPI.js
components/
  Avatar.js
  Avatar.css
  Feed.js
  Feed.css
  FeedStory.js
  FeedStory.test.js
  Profile.js
  ProfileHeader.js
  ProfileHeader.css
```
  
## JSX Represents Objects
>Babel compiles JSX down to React.createElement() calls.
These two examples are identical:
```
  const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
  ```
  ```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
  ```
>React.createElement() performs a few checks to help you write bug-free code but essentially it creates an object like this:
>// Note: this structure is simplified
```
  const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
  ```
>These objects are called “React elements”. You can think of them as descriptions of what you want to see on the screen. React reads these objects and uses them to construct the DOM and keep it up to date.

  
  
 
Dynamic styling 
```
  <div className={`form-control ${!isValid ? 'invalid':''}`}> 
  
  & input {
  display: block;
  width: 100%;
  border: 1px solid ${props => props.invalid ? 'red':'#ccc'};
  font: inherit;
  line-height: 1.5rem;
  padding: 0 0.25rem;
}
  
  
  import styles from './Button.module.css';

const Button = props => {
  return (
    <button type={props.type} className={styles.button} onClick={props.onClick}>
      {props.children}
    </button>
  );
};
  
<div className={`${style['form-control']} ${!isValid && style.invalid}`}>

```
 
 
# useEffect
 ![image](https://user-images.githubusercontent.com/12700182/135762039-72fa0c50-705b-41e8-bed9-251e750f2e50.png)
## What does useEffect do? 
 > By using this Hook, you tell React that your component needs to do something after render. React will remember the function you passed (we’ll refer to it as our “effect”), and call it later after performing the DOM updates. In this effect, we set the document title, but we could also perform data fetching or call some other imperative API.

## Why is useEffect called inside a component? 
 > Placing useEffect inside the component lets us access the count state variable (or any props) right from the effect. We don’t need a special API to read it — it’s already in the function scope. Hooks embrace JavaScript closures and avoid introducing React-specific APIs where JavaScript already provides a solution.

## Does useEffect run after every render? 
 > Yes! By default, it runs both after the first render and after every update. Instead of thinking in terms of “mounting” and “updating”, you might find it easier to think that effects happen “after render”. React guarantees the DOM has been updated by the time it runs the effects.

### What to add & Not to add as Dependencies

In the previous lecture, we explored useEffect() dependencies.

You learned, that you should add "everything" you use in the effect function as a dependency - i.e. all state variables and functions you use in there.

That is correct, but there are a few exceptions you should be aware of:

    You DON'T need to add state updating functions (as we did in the last lecture with setFormIsValid): React guarantees that those functions never change, hence you don't need to add them as dependencies (you could though)

    You also DON'T need to add "built-in" APIs or functions like fetch(), localStorage etc (functions and features built-into the browser and hence available globally): These browser APIs / global functions are not related to the React component render cycle and they also never change

    You also DON'T need to add variables or functions you might've defined OUTSIDE of your components (e.g. if you create a new helper function in a separate file): Such functions or variables also are not created inside of a component function and hence changing them won't affect your components (components won't be re-evaluated if such variables or functions change and vice-versa)

So long story short: You must add all "things" you use in your effect function if those "things" could change because your component (or some parent component) re-rendered. That's why variables or state defined in component functions, props or functions defined in component functions have to be added as dependencies!

Here's a made-up dummy example to further clarify the above-mentioned scenarios:
```
    import { useEffect, useState } from 'react';
     
    let myTimer;
     
    const MyComponent = (props) => {
      const [timerIsActive, setTimerIsActive] = useState(false);
     
      const { timerDuration } = props; // using destructuring to pull out specific props values
     
      useEffect(() => {
        if (!timerIsActive) {
          setTimerIsActive(true);
          myTimer = setTimeout(() => {
            setTimerIsActive(false);
          }, timerDuration);
        }
      }, [timerIsActive, timerDuration]);
    };
```
In this example:

    timerIsActive is added as a dependency because it's component state that may change when the component changes (e.g. because the state was updated)

    timerDuration is added as a dependency because it's a prop value of that component - so it may change if a parent component changes that value (causing this MyComponent component to re-render as well)

    setTimerIsActive is NOT added as a dependency because it's that exception: State updating functions could be added but don't have to be added since React guarantees that the functions themselves never change

    myTimer is NOT added as a dependency because it's not a component-internal variable (i.e. not some state or a prop value) - it's defined outside of the component and changing it (no matter where) wouldn't cause the component to be re-evaluated

    setTimeout is NOT added as a dependency because it's a built-in API (built-into the browser) - it's independent from React and your components, it doesn't change
