# Adding type definitions to your project

There used to be a time where adding type definitions to your project required third party tools, or before that even some manual work. The thing that hasn't changed is the popular DefinitelyTyped github repo. It started as a place where type definitions were aggregated in a single place so people could more easily look them up. After the `tsd` cli was created to more easily install those definitions, and locking them into a `tsd.json` in your project. At that time all definitions were global \(ambient\) which could cause conflicts. A while later the `typings` project started to be a layer on top of DefinitelyTyped by also adding an option to install definitions from other places like the npm repository.

Luckily Microsoft stepped up by allowing the TypeScript compiler to read typings from the `node_modules` folder, and automatically publish definitions from the DefinitelyTyped github repo to the `@types` npm scope.

At the moment that leaves us with three options:

1. A package author can include type definitions in their package by adding a `d.ts` file and referring to it from the `"typings"` field in the `package.json`.
2. When the package author doesn't include typings, someone else can add the typings to DefinitelyTyped where it will be published under the `@types` scope.
3. Or the type definitions can be added to npm in a separate package \(e.g. `library-name-types`\) and you have to manually add it to the `tsconfig.json`.

So when I want to add type definitions for React, I just do:

```shell
npm i -S @types/react
```

If you want to know more about how the TypeScript compiler looks up type definitions, check out [this section](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html#types-typeroots-and-types).

