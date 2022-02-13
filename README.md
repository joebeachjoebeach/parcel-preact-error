## Error building preact with parcel in dev

Parcel fails to resolve [`preact/jsx-dev-runtime`](https://github.com/preactjs/preact/blob/master/package.json#L55-L60) when running in development. It appears not to properly resolve this module as specified in `"exports"` in Preact's `package.json`.

## How to reproduce

1. Clone this repo
2. `yarn install`
3. `yarn start`

You'll get the following:

```
Server running at http://localhost:1234
🚨 Build failed.

@parcel/core: Failed to resolve 'preact/jsx-dev-runtime' from './src/app.jsx'

  /Users/joe/code/playground/parcel-preact-error/src/app.jsx:1:1
  > 1 | export default function App() {
  >   | ^
    2 |   return <div>This is content</div>;
    3 | }
```

## Workaround

You can get around this issue by adding an entry for `preact/jsx-dev-runtime` in `package.json`'s `alias` field. For example:

```
"alias": {
    "preact/jsx-dev-runtime": "preact/jsx-runtime/dist/jsxRuntime.module.js"
}
```
