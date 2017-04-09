# Mixing TypeScript with babel projects

Going full-force with TypeScript in projects is awesome, but sometimes it can complicate things and not everyone is comfortable using it. Things like React and Vue components might be easier done in JavaScript. Other times you might want to use new language features that are available in babel \(as a stage-x preset\), but not yet implemented in TypeScript.

To give developers more freedom I think it's a good idea to support both babel and TypeScript in a single project, where you can just rename any file from `.js` to `.ts` and start adding types.

This book goes into detail about setting up both babel and TypeScript with webpack, how to set up the linting for both files, and other things.

