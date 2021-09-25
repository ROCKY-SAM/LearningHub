
> - https://medium.com/devinder/react-virtual-dom-vs-real-dom-23749ff7adc9

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
