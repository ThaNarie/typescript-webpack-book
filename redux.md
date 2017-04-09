# redux

Redux is a predictable state container for JavaScript apps. You can use Redux together with React, or with any other view library.

## compose

[Composes functions](http://redux.js.org/docs/api/compose.html) from right to left.

```js
import { connect } from 'react-redux';
import { compose } from 'redux';

import Checkout from './Checkout';

const enhanced = enhancedReduxForm(...);

const connected = connect(
  state => ...
);

const prepared = withPrepare(...);

export default compose<any, any, any, any>(
  prepared,
  connected,
  enhanced,
)(Checkout);
```

When dealing with a single input parameter \(in this case `Checkout`\) the amount of generic types passed are 1 greater than the number of passed functions.

Since we are dealing with JavaScript react components, we don't have proper typings for them. We would also need to type any of the HoC functions. If you are up to it, the generic works as follows:

```js
compose<A, B, T1, R>
```

`R` will be the return type of the composed function, in this case the enhanced React component.

`T1` will be the input type of the resulting function, and in that case also the input type of the last compose argument. In this case it's the original `Checkout` component.

`A` and `B` are intermediate types during composition. In this case the result from `enhanced` will be passed to `connected` and the result from `connected` will be passed to `prepared`. When looking at the type definitions, the order of generics is a bit weird. The default compose doesn't expect any input parameters, and the generics define the passing of the last to the previous function \(remember, compose is basically a reduceRight, so it works from right to left\). This is best illustrated with a default 4-function compose:

```js
compose<A, B, C, R>(f1, f2, f3, f4)();
```

Here `A` is the result from `f4` passed to f3, `B` is the result from `f3` passed to `f2`, and `C` from `f2` to `f1`, and `R` is the return type from `f1`. Nicely in backwards order.

When we introduce an input to the resulting function, this `T1` is placed at a weird spot. Instead of the beginning \(where you might expect it, it is placed right before the return type, to group it nicely with the resulting function type:

```js
compose<A, B, C, T1, R>(f1, f2, f3, f4)(foo);
```



