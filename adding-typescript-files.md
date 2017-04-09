# Adding TypeScript files to your project

This part is super simple, just rename an existing JavaScript file to `.ts` or create a blank file and start typing. Webpack will just pick it up, and linting works as well.

You can decide your own pace; only do util functions in TypeScript, also pick up the business logic like models and API calls, or go overboard and convert everything. If some files give you trouble or you want to use a stage-1 babel preset that is not yet supported by TypeScript, you can always switch back to JavaScript.

After you created your TypeScript files, you can gradually start add types. Even without adding explicit type information, TypeScript can already infer a lot. To make things a bit more explicit, you can begin with typing your API bounderies; the input parameters and the return type of your functions.

If you want to go totally overboard you can of course start typing every variable and function, and even turn off `"noImplicitAny"` and other flags to make it more strict. It's important to create the right setup that fits your project and developers working on it.

