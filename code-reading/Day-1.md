# Day 1 
one thing that I want to said is until now I don't hae any experience with `Preact` and I only want to dive into the codes. first I install `Preact` as dev dependency so I can keep code reading in node_modules directory.

## Starting Point
Normally I start from index.js or main.js but for this time I choose to start from [getting-started](https://preactjs.com/guide/v10/getting-started) , and this is the code that I think is good for startig point :

```js
import { h, Component, render } from 'https://unpkg.com/preact?module';

// Create your app
const app = h('div', null, 'Hello World!');

// Inject your application into the an element with the id `app`.
// Make sure that such an element exists in the dom ;)
render(app, document.getElementById('app'));
```

at the first line they import three thing , `h` , `Component` and `render`. and the they create an app with the `h` and then render the created app with `render`. for me `h` is like `createElement` in React. also render is like `ReactDOM.render()`. for me it's interesting to start with `h` and `render`

## h

In _src/index.js_ they import h like this : 
```js
export {
	createElement,
	createElement as h,
	Fragment,
	createRef,
	isValidElement
} from './create-element';
```

so , actually _h_ is _createElement_ and I think it's good idea to look into _createElement_ so I Open _./create-element_ file.
