# Adding TSLint

TSLint can be compared to ESLint, but works with TypeScript files instead. Besides the normal JavaScript linting rules, it also adds some TypeScript specific rules to improve your code quality and catch errors.

There is also a TypeScript parser for ESLint \(similar to the babel parser\), but it's currently still in the experimental stage, and doesn't work correctly with all ESLint rules.

The main benefit of using TSLint is the IDE integration for Webstorm and others.

To start using TSLint we have to install the package, and also the default configuration we will be using:

```shell
npm i -D tslint tslint-config-airbnb
```

The `tslint-config-airbnb` preset will mimic the ESLint airbnb config as closely as possible with the TSLint rules that are available, which is a perfect starting point to make JavaScript and TypeScript linting as similar as possible.

