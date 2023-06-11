# hono-jsx-types

Enhanced type definitions for Hono's JSX intrinsic elements (WIP)

## Motivation

While Hono's JSX middleware is great for templating HTML, its type definition has a small flaw.
Since the intrinsic elements are defined as `{ [tagName: string]: Record<string, any>; }`, it accepts arbitrary attributes and values.
This potentially leads to incorrect markup and lacks autocompletion for attribute keys.

This package aims to fill the gap. Providing proper type definitions can help users catch incorrect attribute values and give them a nice autocompletion experience as shown in the pictures below.

<!-- picture here -->
![compile error says 0x1d cannot be passed to id attribute of a <p> element](./img/compile-error.png)

![alt attribute and others are suggested in autocompletion in a <img> element](./img/autocompletion.png)

## Usage

Install the package from GitHub:

```console
npm install --save-dev yudai-nkt/hono-jsx-types
```

Then, add it to the `compilerOptions.types` array:

```diff
 {
   "compilerOptions": {
     "types": [
+      "hono-jsx-types"
     ],
   }
 }
```

## FAQ
### Why not contribute to Hono's core?

This package relies on the type definitions for DOM API from the DefinitelyTyped's [`@types/web`](https://www.npmjs.com/package/@types/we) package, which is also included in the TypeScript standard library.
I believe Hono, as a edge/server side multi-runtime library, should depend only on TC39 and WinterCG standardization, not on WHATWG's DOM Living Standard even if the dependency is only type-level.

### Why not use the built-in `dom` library?

If this package adds it to the `compilerOptions.lib` array, types in `lib.dom.d.ts` would leak into your application and the same can be said for the declaration files under `@types` scope.
That's why I installed `@types/web` under a custom alias, patch the package to make it into a module, and explicitly import types from it.

### Why not publish to NPM registry?

This package is more of a POC right now.
In addition to the package status, installing from GitHub should just work out-of-the-box as it only provides a type declaration file.
I'll be dogfooding the package with [my project](https://github.com/yudai-nkt/awesome-hono) before publishing.

## License

This repository is distributed under the MIT License.
See [LICENSE.md](./LICENSE.md) for details.
