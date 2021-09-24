
> - https://medium.com/devinder/react-virtual-dom-vs-real-dom-23749ff7adc9

# Virtual DOM
The Virtual DOM is a light-weight abstraction of the DOM. You can think of it as a copy of the DOM, that can be updated without affecting the actual DOM. It has all the same properties as the real DOM object, but doesn’t have the ability to write to the screen like the real DOM. The virtual DOM gains it’s speed and efficiency from the fact that it’s lightweight. In fact, a new virtual DOM is created after every re-render.
Reconciliation is a process to compare and keep in sync the two files (Real and Virtual DOM). Diffing algorithm is a technique of reconciliation which is used by React.


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
