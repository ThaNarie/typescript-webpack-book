# redux-actions

The [redux-actions](https://github.com/acdlite/redux-actions) package contain Flux Standard Action utilities for Redux.

```shell
npm i -S redux-actions @types/redux-actions
```

## createAction

Wraps an action creator so that its return value is the payload of a Flux Standard Action.

**Note**: The examples below only work with changes proposed in the [following issue](https://github.com/DefinitelyTyped/DefinitelyTyped/issues/15697).

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

## handleActions

Wraps a reducer so that it only handles Flux Standard Actions of a certain type.

**Note:** There are several ways to use reducers with TypeScript.

* The default `switch/case` has the advantage to reduce some TypeScript boilerplate by incorperating Union Types and Type Guards.
* The same is possible using `handleActions` \(with some tweaks to the type definitions\), but it requires you to specify the type keys as strings instead of reference the exported action types.
* This example will showcase the default implementation using this function.

```js
import {Action, handleActions} from 'redux-actions';

// import the ActionTypes and the typed Payloads
import {
  CLEAR_SCROLL_TO,
  SCROLL_TO,
  REGISTER_FIXED_HEADER_ELEMENT,
  UNREGISTER_FIXED_HEADER_ELEMENT,
  ScrollToPayload,
  RegisterFixedHeaderElementPayload,
  UnregisterFixedHeaderElementPayload,
} from '../actions/scrollActions';

// type the local redux State
type State = {
  scrollTo: Array<number>;
  fixedHeaderElements: {
    [key: string]: number;
  };
};

const initialState = {
  scrollTo: [],
  fixedHeaderElements: {},
};

// add union type for all possible action payloads
type CombinedPayloads = ScrollToPayload | RegisterFixedHeaderElementPayload | UnregisterFixedHeaderElementPayload;

// create the reducerMap (now empty)
const scrollManagerReducer = handleActions<State, CombinedPayloads>({
  [...]: (state, action) => { ... },
}, initialState);
```

The individual reducer functions will be explained below. The first handles the action without any payload, which is straightforward:

```js
// input state is handled by the handleActions generic, so only type the output state
[CLEAR_SCROLL_TO]: (state):State => ({
  ...state,
  scrollTo: [],
}),
```

The following case also types the action:

```js
// type the action parameter explicitly (since the generic uses the CombinedPayloads)
// the destructuring of action now gets type information
[SCROLL_TO]: (state, { payload }: Action<ScrollToPayload>): State => ({
  ...state,
  scrollTo: [
    ...state.scrollTo,
    payload,
  ],
}),
```

When destructuring more, we might want to break it over multiple lines:

```js
[REGISTER_FIXED_HEADER_ELEMENT]: (
  state,
  { payload: { elementName, bottomY } }: Action<RegisterFixedHeaderElementPayload>,
): State => ({
  ...state,
  fixedHeaderElements: {
    ...state.fixedHeaderElements,
    [elementName]: bottomY,
  },
}),
```



