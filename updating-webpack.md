# Updating webpack with TypeScript

In the previous step we added TypeScript configuration to the project, but we still need to update webpack to compile the files. We do this by adding a second loader to target the `.ts` files, and reusing the `babel-loader` to transipile the output from TypeScript to make them useful for \(older\) browsers; the same as we do with normal JavaScript files.

So the only thing that the TypeScript compiler does, is compile-time type-checking and stripping the TypeScript specific syntax so babel can understand it.

We start by moving the babel loader config into a function so we can use them for both loaders:

```js
const getBabelLoader = buildOption => (

```



