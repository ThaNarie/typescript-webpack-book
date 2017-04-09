# redux-actions

The [redux-actions](https://github.com/acdlite/redux-actions) package contain Flux Standard Action utilities for Redux.

```shell
npm i -S redux-actions @types/redux-actions
```

```js
import { createAction } from 'redux-actions';

// has no payload
export const clearScrollTo = createAction(CLEAR_SCROLL_TO);

// usage
dispatch(clearScrollTo());
```

```js
// payload is a number
export type ScrollToPayload = number;

// input and action payload are the same
export const scrollTo = createAction<ScrollToPayload>(SCROLL_TO);

// usage
dispatch(scrollTo(130));
```

```js
// payload is an object with string and number
export type RegisterFixedHeaderElementPayload = {
  elementName: string;
  bottomY: number;
};

// since the input parameters to the actionCreator are transformed to a payload
// using the payloadCreator helper function, we specify their types separately
// first is the Payload, and after that follows the type of each parameter
// the 'string' and 'number' typed are mapped to the (elementName, bottomY) function
export const registerFixedHeaderElement = createAction<
  RegisterFixedHeaderElementPayload,
  string,
  number
>(
  REGISTER_FIXED_HEADER_ELEMENT,
  (elementName, bottomY) => ({ elementName, bottomY }),
);

// usage
dispatch(registerFixedHeaderElement('fooHeader', 150);
```



