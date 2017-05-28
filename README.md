# web-router

A simple and opinionated client side router built with web components.

## Example

```html
<web-router>
  <app-home pattern="^/$" import="app-home.html"></app-home>
  <app-about pattern="^/about$" import="app-about.html"></app-about>
  <app-contact pattern="^/contact$" import="app-contact.html"></app-contact>
  <app-404 pattern=".*" import="app-404.html"></app-404>
</web-router>
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
