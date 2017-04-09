# Adding Typescript to the project

The first step is to add TypeScript to the project, by installing it trough npm:

```sh
npm i -D typescript
```

After that we want to create a `tsconfig.json` to tell the compiler what settings to use:

```json
{
  "compilerOptions": {
    "sourceMap": true,
    "noImplicitAny": false,
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "moduleResolution": "Node",
    "target": "es2017",
    "lib": [
      "DOM",
      "ES6",
      "DOM.Iterable",
      "ScriptHost"
    ],
    "baseUrl": ".",
    "paths": {
      "vendor": ["vendor"],
    }
  },
  "include": [
    "./src/**/*.ts"
    "declarations.d.ts"
  ]
}
```

The `"noImplicitAny": false` flag is mainly set so we can import any npm module without having to explicitly add or define typings. Using this flag they will be typed as any.

The `"allowJs": true` flag is set to allow us to import JavaScript files from TypeScript files, which makes the whole integration work nicely.

The `"allowSyntheticDefaultImports": true` flag tells typescript that even though modules are exported directly, we can still use them as if it were exported as a default export. Normally this isn't legal, since direct `module.exports = ...;` used in NodeJS aren't legal in es2016 modules, but babel takes care of that inconsistency for us.

The `"target": "es2017"` flag is set to transpile as less as possible, since we want babel to take care of that.

Because of the flag above, we must specify the used internal definitions ourselves using the `"lib": [...]` flag.

With the `"paths": { ... }` flag we can set resolve aliasses that we can configure in webpack, and will now understood by the TypeScript compiler as well. For that to work we also need to set the `"baseUrl": "."` flag to let the TypeScript compiler know where to resolve the paths from.

The `"inlcude": [ ... ]` section tells the TypeScript compiler which files to compile. In this case we have included all `.ts` files in our `src` folder, and added a general declarations file for custom global declarations:

```javascript
// declarationsd.ts
declare const WP_DEFINE_IS_NODE:any;
declare const WP_DEFINE_DEVELOPMENT:any;
```

The above declarations are set by the `webpack.DefinePlugin`.



