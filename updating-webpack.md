# Updating webpack with TypeScript

In the previous step we added TypeScript configuration to the project, but we still need to update webpack to compile the files. We do this by adding a second loader to target the `.ts` files, and reusing the `babel-loader` to transipile the output from TypeScript to make them useful for \(older\) browsers; the same as we do with normal JavaScript files.

So the only thing that the TypeScript compiler does, is compile-time type-checking and stripping the TypeScript specific syntax so babel can understand it.

We start by moving the babel loader config into a function so we can use them for both loaders:

```js
const getBabelLoader = () => (
  {
    loader :'babel-loader',
    options: {
      presets: [['es2015', { "modules": false }]],
      plugins: [
        'transform-runtime',
        'transform-class-properties',
        'transform-object-rest-spread',
        'transform-strict-mode',
        ["babel-plugin-transform-builtin-extend", {
          globals: ["Error", "Array"]
        }],
        'transform-es2015-destructuring',
        'transform-es2015-parameters'
      ],
      cacheDirectory: ''
    }
  }
);
```

The we update the `.js` rule and add the `.ts` rule:

```js
// webpack module config
module: {
  rules: [
    {
      test: /\.js$/,
      include: [
        /src/,
      ],
      use: [getBabelLoader()],
    },
  ],
  rules: [
    {
      test: /\.ts$/,
      include: [
        /src/,
      ],
      use: [
        getBabelLoader(),
        {
          loader: 'awesome-typescript-loader',
          options: {
            silent: true,
            configFileName: path.resolve(__dirname, '../../../tsconfig.json')
          }
        }
      ],
    },
  ],

},
```

For that to work we need to install the `awesome-typescript-loader`:

```shell
npm i -D awesome-typescript-loader
```

We configure the awesome-typescript-loader to use the `tsconfig.json` in the root of our project.

