1 Configure development environment:

- Install ESLint, Prettier and EditorConfig.

---

2 Configure the application routes:

- Install the react-router-dom library:
  ```sh
  yarn add react-router-dom
  ```
- Create the pages folder: src/pages

- Create the file that will contain the routes component: src/routes.js

---

3 - Add library for writing styled in javascript:

```sh
yarn add polished
```

We gonna use it to make a color brighter/darken, etc.

---

4 Add a library to simulate an API from a json file:

```sh
yarn add json-server -D
```

To execute the fake API run the following command:

```sh
yarn json-server server.json -p 3333 -w
```

---

5 Loading API products:

- To format the product price create the file src/utils/format.js

---

6 Redux installation and configuration:

- Install the Redux library and the react integration lib:

  ```sh
  yarn add redux react-redux
  ```

- Create a folder `src/store` to keep Redux files

  - Create a file index.js to keep the redux settings:

    > createStore to create the global state (needs a reducer at creation time)
    > Provider makes the Redux store available to the components through connect() calls

- Create a folder `src/store/modules` to keep the reducers and modules related to redux:
  - Create the file `src/store/modules/cart/reducer.js` for the cart reducer
- When the project has many reducers its necessary to create a file/module to combine them, so:
  - Create the file `src/store/modules/rootReducer.js` to combine the reducers. When you create a new reducer (i.e: user reducer) import it in the rootReducer and use the combineReducers method from redux library togheter with the other reducers.

---

7 Add item to cart

**Redux gist**:

> The whole state of your app is stored in an object tree inside a single store. The only way to change the state tree is to emit an action, an object describing what happened. To specify how the actions transform the state tree, you write pure reducers

- When the user click in add to cart, the object is passed to the cart reducer.
  For this the `connect()` method from react-redux will be used. The method allows the component to connect to the redux store state (remember we added the Provider component in the App as a wrapper of the application components, the provider makes the connect method actually works).
  Each component connected to redux has a `dispatch` prop, this method allows to send the actions to the reducer/redux (When a dispatch method is executed, all the reducers listen to all the actions. They proccess the action according to the action type supported).
  The values can be retrivied in the reducer using its arguments: state and action. Use a switch inside the reducer to check the action type and decide hich action to realize.

  PS: In Redux the State Tree uses the Singleton pattern and the connect method uses the Observer pattern.
  In Redux, the convention is to have a single store per application, usually separated into data domains internally (you can create more than one Redux store if needed for more complex scenarios). Flux has a single dispatcher and all actions have to pass through that dispatcher. It's a singleton object.

Ok, you saved the data in the redux store,
but how to retrieve this data in another component?

- Each reducer is a Redux store (state) property and can be acessed using the `connect` method from react-redux.
  Pass a function as a parameter to the connect method to
  get the current global state and then return the respective reducer property.
  The reducer property is received as a prop in the component.

  - Another option is to create a method to map state to props;

  **When the reducer updates the state, guess what? it triggers a render to all the components that have the connect method (Observer pattern), that will update the values in the respectives components that depend on the respective state.**

---

8 Configure Reactotron + Redux (for debug):

- Install Reactron and its react integration module:

```sh
yarn add reactotron-react-js reactotron-redux
```

- Integrates reactotron to redux in the store index.js file, then import the
  reactotron config in the App.js before the store configuration;

---

9 List items in the cart component:

---

10 Duplicated product:

- Install immer (Immer is a tiny package that allows you to work with immutable state in a more convenient way. It is based on the copy-on-write mechanism. The basic idea is that you will apply all your changes to a temporary draftState, which is a proxy of the currentState. Once all your mutations are completed, Immer will produce the nextState based on the mutations to the draft state. This means that you can interact with your data by simply modifying it while keeping all the benefits of immutable data.)
  ```sh
  yarn add immer
  ```

---

11 remove product from Cart

---

12 Refactor Actions:

- Create an actions.js file for each reducer;

---

13 Update quantity

---

14 Redux Saga configuration:

- In this class we learned how to use middlewares in Redux.
  Middlewares are usually intercepters, Redux Saga intercepts actions
  and generates a side effect (like an async call to API, retrieve data from
  storage/DB, etc).
  An use case example is when it is necessary to retrieve additional information
  of a product from the API.

- Install Redud Saga:

  ```sh
  yarn add redux-saga
  ```

- Create a `sagas.js` file for each reducer/module, i.e, for the the cart module
  create the file `src/store/modules/cart/sagas.js`, it will contain the generators
  that will be processed by sagas;

- Create a file `src/store/modules/rootSaga.js` that will handle all the sagas middlewares
  (like the rootReducer.js). It is necessary to import and apply the sagas middlewares
  in the Redux store (`src/store/index.js`).

---

15 Reactotron + Saga:

- Install and configure the reactotron plugin for Redux Saga, it helps for debugging:
  ```sh
  yarn add reactotron-redux-saga
  ```

---

16 React Toastify:

- Install the lib:

```sh
yarn add react-toastify
```

- Import the lib in the App.js file.
- Import the React Toastify styling in the global.js styles file.

---

17 Navigation with Redux Saga:

- Sometimes its necessary to let the user navigate or redirect him to a page after
  realizing some data processing (like for example after a saga's middleware execution),
  but can not be possible to use this.props.history.push(/page), so its necessary
  to navigate with sagas.

- Install the lib history to control the history API of the browser:

  ```sh
  yarn add history
  ```

- Create a file `src/services/history.js` to contain the history configuration;
- Import the history in the App.js and change the BrowserRouter component to Router.
  Then pass the history property to it.
- Import the history in the respective file/module is the sagas file

---

18 React Hooks and Redux:

- Now instead of using the `connect()`, we gonna use the `useSelector()` method
  And now instead of using `dispath()`, we gonna use `useDispatch` method.
