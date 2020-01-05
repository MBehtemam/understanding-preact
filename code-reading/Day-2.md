# Day 2

## h , createElement
In day 1 I find `createElement`  function that exported as a `h` and you can create new element or I don't know may be component with . `createElement` accept 3 arguments and they are `type` ,`props` and `children`, ok, after look at the getting-started I find this line of code : 

```js
const app = h('div', null, 'Hello World!');
```

so it seems `type` is one of html-tags like div,span or base on my experience with React, maybe a component. after that we have `props` , it seems `props` is object because they ittrate over props like an object
```js
for (i in props) {
```

also I find some normalization : 
```js
let normalizedProps = {},
		i;
	for (i in props) {
		if (i !== 'key' && i !== 'ref') normalizedProps[i] = props[i];
	}
```

what they do here is they extract `key` and `ref` from props, means _normalizedProps_ contains all the props key except `key` and `ref`.
after that they assume everything as children, wheter we pass 3 arguments to `createElement` or more.
```js
if (arguments.length > 3) {
		children = [children];
		// https://github.com/preactjs/preact/issues/1916
		for (i = 3; i < arguments.length; i++) {
			children.push(arguments[i]);
		}
	}
	if (children != null) {
		normalizedProps.children = children;
	}
```
and they the pass the created children as a children key in `normalizedProps`. after that they create `vnode` :

```js
return createVNode(
		type,
		normalizedProps,
		props && props.key,
		props && props.ref
	);
```
I think `VNode` is something like virtual node , something that like virtual DOM. I think it's a good idea to look at the `createVNode` function.


## createVNode function 
seems that `createVNode` create some type of virtual element.also the comment can describe this function very good :

```js
 * Create a VNode (used internally by Preact)
 ```
 so `createVNode` is only for internally used. I try to import `createVNode` with **import { createVNode } from 'preact'** but I can't so it really used internally. if we look at the `createVNode` function the arguments is look like below : 

 ```js
 export function createVNode(type, props, key, ref) {
 ```
 before looking at the comment let's back to the `createElement` function when that function call the `createVNode` :

 ```js
 return createVNode(
		type,
		normalizedProps,
		props && props.key,
		props && props.ref
	);
 ```
 as we saw before `type` is a tag name or a component, the we have `props` that actually is `normalizedProps`. so props is all the props and children except `key` and `ref`. the last two thing for createing `VNode`are `key` and `ref`. at the end they create an object that name is `vnode` :
 
 ```js
 const vnode = {
		type,
		props,
		key,
 ```
 at the end the return the `vnode` and also the call `vnode` function in options.

 ```js
 if (options.vnode) options.vnode(vnode);
 ```

 corrently `options` is black box for me but they import that at the top of page : 

 ```js
 import options from './options';
 ```
 it's a good point to loot into it at tomorrow but now I want to move forward in this file. in this file we have tow other function. one is `createRef` that seems that create a reference like ref in React, this funciton just return and empty object, maybe they fill this later with reference to parent or , I don't know. the other function is `Fragment` that create a fragment, if we assume it's like a React Fragment, they it should only return children because `Fragment` is only a wrapper that dosen't accept any props or style or ect.

 ```js
 export function Fragment(props) {
	return props.children;
}
```