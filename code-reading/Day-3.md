# Day 3

## Options

yesterday we saw this line of code : 

```js
if (options.vnode) options.vnode(vnode);
```

and also on top of page we saw that they import it : 

```js
import options from './options';
```

now it's time to look at the `option` :

```js
/** @type {import('./internal').Options}  */
const options = {
	_catchError
};
```
Now I can't see andy `vnode` function. so I should find some clues. one clue is I think the comment : 

```js
/** @type {import('./internal').Options}  */
```
 Ok , I find that , if we look at `internal.d.ts` we find that it's an interface. and in this interface we can look at the `VNode` section : 

 ```js
 export interface VNode<P = {}> extends preact.VNode<P> {
	// Redefine type here using our internal ComponentFactory type
	type: string | ComponentFactory<P>;
	props: P & { children: preact.ComponentChildren };
	_children: Array<VNode<any>> | null;
	_parent: VNode | null;
	_depth: number | null;
	/**
	 * The [first (for Fragments)] DOM child of a VNode
	 */
	_dom: PreactElement | Text | null;
	/**
	 * The last dom child of a Fragment, or components that return a Fragment
	 */
	_lastDomChild: PreactElement | Text | null;
	_component: Component | null;
	constructor: undefined;
}
 ```

 also another thing is that it extend `preact.VNode` , preact imported in this file from `./index.js` and in `index.js` we can see this line of code : 

 ```js
 	interface VNode<P = {}> {
		type: ComponentType<P> | string;
		props: P & { children: ComponentChildren };
		key: Key;
		ref: Ref<any> | null;
		/**
		 * The time this `vnode` started rendering. Will only be set when
		 * the devtools are attached.
		 * Default value: `0`
		 */
		startTime?: number;
		/**
		 * The time that the rendering of this `vnode` was completed. Will only be
		 * set when the devtools are attached.
		 * Default value: `-1`
		 */
		endTime?: number;
	}
 ```

 the above line is an interface ,another interface that comes with Options is this line of code : 

 ```js
 interface Options {
		/** Attach a hook that is invoked whenever a VNode is created. */
		vnode?(vnode: VNode): void;
 ```

 still `options.vnode` is a little black box for me. so I decide to search throught the whole **Preact** directory. and I find some `options.vnode` in different places. one of options are located in **https://github.com/preactjs/preact-compat** packages. this package as they described are useing for compabillity with React. most of definations of `options.vnode` are located in **compact** and **debug** directory.