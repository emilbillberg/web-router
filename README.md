# web-router
A simple and opinionated client side router built with web components.

## Example

### Web-router
Web-router shows and hides the children by comparing the current url and the `pattern` attribute of each children. The `pattern` attribute needs to be a valid regex - the first matching child will be visible. Also, web-router will lazy load the currently selected element if it has the `import` attribute. The `import` attribute should be a relative path to the element.

```html
<web-router>
  <app-home pattern="^/$" import="app-home.html"></app-home>
  <app-about pattern="^/about$" import="app-about.html"></app-about>
  <app-contact pattern="^/contact$" import="app-contact.html"></app-contact>
  <app-404 pattern=".*" import="app-404.html"></app-404>
</web-router>
```

### Web-reducer
The `WebReducer` mixin is responsible to handle the state of the app. A class that implements `WebReducer` needs to implement the function `reduceHandler`. The `reduceHandler` takes three arguments:
* state (Object) - the previous state object
* type (String) - the name of the action
* data (Any) - the data from the action. Can be any arbitary value.

```html
<script>
  class MyApp extends WebReducer(Polymer.Element) {

    static get is() {
      return 'my-app';
    }

    constructor() {
      super();
      this.setInitialState({
        todos: [
          { text: 'Buy groceries', completed: true },
          { text: 'Buy a car', completed: false },
        ],
        random: Math.random(),
      });
    }

    reduceHandler(state, type, data) {
      return {
        todos: this.todosReducer(state.todos, type, data),
        random: this.randomReducer(state.random, type, data),
      };
    }

    todosReducer(state, type, data) {
      switch (type) {
      case 'TODO_ADD':
        return state.concat(data);
      default:
        return state;
      }
    }

    randomReducer(state, type, data) {
      switch (type) {
      case 'RANDOM_NUMBER':
        return data;
      default:
        return state;
      }
    }

  }

  window.customElements.define(MyApp.is, MyApp);

</script>
```

### Web-subscriber
Allows an element to get updated as soon as the state of the app changes. An element that implements the `WebSubscriber` mixin will have a `state` object that will hold the app's shared state. Only the web-router's visible element will update its properties and the changes will be batched.

```html
<template>
  <dom-repeat items="[[state.todos]]" as="item">
    <template>
      <div>[[item.text]]</div>
    </template>
  </dom-repeat>
</template>

<script>
  class AppTodos extends WebSubscriber(Polymer.Element) {
    static get is() {
      return 'app-todos';
    }
  }
  window.customElements.define(AppTodos.is, AppTodos);
</script>
```

## Development
1. Download and install [NodeJS](https://nodejs.org).

2. Clone the source code from Github.

  ```sh
  git clone git@github.com:emilbillberg/web-router.git
  ```

3. Start local server.

  ```sh
  npm run dev
  ```

## Tests

  ```sh
  npm test
  ```
