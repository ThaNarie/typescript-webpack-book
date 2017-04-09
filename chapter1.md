# Webpack setup

Before we start integrating typescript, we will explain the current webpack setup we have for transpiling our JavaScript files with babel.

```js
// webpack resolve config
resolve : {
    extensions : ['.js', '.json'],
}
```

The above will tell webpack to look for files with those extensions when importing a path without an extension.

```js
// webpack module config
module: {
  rules: [
    {
      test: /\.js$/,
      include: [
        /src/,
      ],
      use: [{
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
      }],
    },
  ],
},
```

The above will enable the `babel-loader` for files with the `.js` extension, and pass along some options to babel.

```js
plugins: [
  new webpack.DefinePlugin({
    'process.env' : {'NODE_ENV': JSON.stringify(dev ? 'development' : 'production')}
    'WP_DEFINE_IS_NODE': false,
    'WP_DEFINE_DEVELOPMENT': dev,
  }
]
```

The will set compile time constants that are available in all the files.

