---
title: "Adding a Redux Store"
---

[Redux](https://redux.js.org/) helps you write applications that behave consistently, run in different environments (client, server, and native), and are easy to test; that’s why Gatsby uses it as a core technology under the hood. On top of that, Redux provides a great developer experience, such as [live code editing combined with a time-traveling debugger](https://github.com/reduxjs/redux-devtools).


In order to use Redux for **custom** state management in a Gatsby site, there are two methods to use.

### Method: 1

let's install the redux and react-redux packages in you project:
```bash
npm install --save redux react-redux
```

Yarn
```bash
yarn add redux react-redux
```
once the installation is done, the next step is to create a file called `index.js` inside `src/state` folder, there we'll create write our reducer and dispatch method.
```js
const initialState = {
  gatsbyRedux: true,
};

export default (state = initialState, action) => {
  // Your code goes here.
  return state;
};
```

in order provide the state to  React, create a new file inside `src/state` folder named `wrapRedux.js` and put the below code:
```js
import React from 'react';
import { Provider } from 'react-redux';
import { createStore as reduxCreateStore } from 'redux';
import rootReducer from './index';

const createStore = () => reduxCreateStore(rootReducer);

export default ({ element }) => (
  <Provider store={createStore()}>{element}</Provider>
);
```

Now wrap the root element in the gatsby config file both on server-side and client-side. put the below code on `gatsby-ssr.js` and `gatsby-browser.js` 
```js
export { default as wrapRootElement } from './src/state/ReduxWrapper';
```


Learn more about [wrapRootElement](https://www.gatsbyjs.org/docs/browser-apis/#wrapPageElement)

Check out the Using Redux example with [./gatsby-ssr.js](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-redux/gatsby-ssr.js) and [./gatsby-browser.js](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-redux/gatsby-browser.js) files to see how this is implemented. You can also check out more information on the official [Redux](https://redux.js.org/introduction/getting-started) docs.

### Method: 2
In this method, you don't need to do anything else. You just need to install the  [gatsby-plugin-redux](https://www.gatsbyjs.org/packages/gatsby-plugin-react-redux/) and go.
