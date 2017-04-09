# Adding TSLint

TSLint can be compared to ESLint, but works with TypeScript files instead. Besides the normal JavaScript linting rules, it also adds some TypeScript specific rules to improve your code quality and catch errors.

There is also a TypeScript parser for ESLint \(similar to the babel parser\), but it's currently still in the experimental stage, and doesn't work correctly with all ESLint rules.

The main benefit of using TSLint is the IDE integration for Webstorm and others.

To start using TSLint we have to install the package, and also the default configuration we will be using:

```shell
npm i -D tslint tslint-config-airbnb
```

The `tslint-config-airbnb` preset will mimic the ESLint airbnb config as closely as possible with the TSLint rules that are available, which is a perfect starting point to make JavaScript and TypeScript linting as similar as possible.

To configure TSLint we will add a `tslint.json`

```js
// tslint.json
{
  "extends": [
    "tslint-config-airbnb"
  ],
  "rules": {
    // This rule mixes up the JS Array() and TS Array<string>
    "prefer-array-literal": [ true, { "allow-type-parameters": true } ],
    // We might disable this rule in the future when too much custom maps are included
    "import-name": [ true, { "react": "React", "debug": "debugLib" }],
    // Doesn't take strings into account like ESlint does
    "max-line-length": [ false ],
    // We often pass references to Classes around that need to start with an uppercase
    "variable-name": [ true, "allow-pascal-case" ]
  }
}
```



