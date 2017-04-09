# Eslint

For linting our JavaScript files, we use eslint. You can define the rules in a config file, specify files to ignore in an ignore file, and Webstorm has integrated support so you can see linting errors in your IDE.

Your `.eslintrc` file might look something like this:

```json
{
  "parser": "babel-eslint",
  "extends": "airbnb",
  "plugins": [
    "import",
    "react"
  ],
  "settings": {
    "import/resolver": {
      "webpack": {
        "config": "./build-tools/config/webpack/webpack.config.resolve.js"
      }
    }
  },
  "env": {
    "browser": true
  },
  "rules": {
    "linebreak-style": 0,
    "no-use-before-define": 0,
    "no-empty-pattern": 0,
    "no-unused-expressions": ["error", {
      "allowShortCircuit": true,
      "allowTernary": true
    }],
    "import/no-extraneous-dependencies": ["error", {
      "devDependencies": ["**/test/**/*.js"]
    }],
    "no-plusplus": ["error", {
      "allowForLoopAfterthoughts": true
    }]
  }
}
```

The `parser` key tells eslint to use the babel parser, since we are using stage 3 of 4 plugins that haven't made it in the spec yet, and are not supported by the eslint parser itself.

The `import/resolver` part tells the eslint import plugin to use webpack to resolve imports, so it can properly display errors, without false positives, when imports are wrong.

We also have an `.eslintignore` file to exclude things we don't want to have linted:

```
build/**
scripts/**
node_modules/**
```

To use the linting in our build script or git hooks we have set up a npm script:

```js
// package.json
{
    "scripts" {
        "lint:js": "eslint .",
    }
}
```



