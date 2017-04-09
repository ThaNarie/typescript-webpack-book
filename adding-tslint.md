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

To use the linting in our build script or git hooks we have set up a npm script:

```js
// package.json
{
    "scripts" {
        "lint:ts": "tslint \"src/**/*.ts\" -t stylish --type-check -p ./tsconfig.json -e \"node_modules/**/*.ts\" -e \"**/*.d.ts\"",
    }
}
```

With the `-t stylish` we match the output to ESLint, with `--typecheck` and `-p ./tsconfig.json` we add typeschecking to the linter, and with the `-e` flags we exclude patterns that we don't want to have linted. Unfortunately TSLint doesn't have a replacement for `.eslintignore` yet.

After this setup we can enable TSLint in our IDE, and run `npm run lint:ts` from the command-line to test our setup.



