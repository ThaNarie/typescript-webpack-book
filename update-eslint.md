# Update ESLint for TypeScript

To allow our ESLint `import` plugin stop complaining about TypeScript files, we have to configure it properly:

```js
// .eslintrc update
{
    "rules": {
        "import/extensions": ["error", "always", {
          "js": "never",
          "ts": "never",
        }],
    }
}
```



