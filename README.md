# ES6 (ES2015) Modules Cheatsheet

This document is adapted from an [excellent proposal by leebyron](https://github.com/leebyron/ecmascript-more-export-from).

### Imports and Exports:

Import Statement Form               | [[ModuleRequest]] | [[ImportName]] | [[LocalName]]
---------------------               | ----------------- | -------------- | -------------
`import v from "mod";`              | `"mod"`           | `"default"`    | `"v"`
`import {default as v} from "mod";` | `"mod"`           | `"default"`    | `"v"`
`import * as ns from "mod";`        | `"mod"`           | `"*"`          | `"ns"`
`import {x} from "mod";`            | `"mod"`           | `"x"`          | `"x"`
`import {x as v} from "mod";`       | `"mod"`           | `"x"`          | `"v"`
`import "mod";`                     |                   |                |


Export Statement Form               | [[ModuleRequest]] | [[ImportName]] | [[LocalName]] | [[ExportName]]
---------------------               | ----------------- | -------------- | ------------- | --------------
`export var v;`                     | **null**          | **null**       | `"v"`         | `"v"`
`export default function f(){};`    | **null**          | **null**       | `"f"`         | `"default"`
`export default function(){};`      | **null**          | **null**       | `"*default*"` | `"default"`
`export default 42;`                | **null**          | **null**       | `"*default*"` | `"default"`
`export {x}`;                       | **null**          | **null**       | `"x"`         | `"x"`
`export {x as v}`;                  | **null**          | **null**       | `"x"`         | `"v"`
`export {x as default}`;            | **null**          | **null**       | `"x"`         | `"default"`
`export {x} from "mod"`;            | `"mod"`           | `"x"`          | **null**      | `"x"`
`export {x as v} from "mod"`;       | `"mod"`           | `"x"`          | **null**      | `"v"`
`export {default as v} from "mod";` | `"mod"`           | `"default"`    | **null**      | `"v"`
`export * from "mod"`;              | `"mod"`           | `"*"`          | **null**      | **null**


### Symmetry between import and export

There's a syntactic symmetry between the export-from statements and the import
statements they resemble. There is also a semantic symmetry; where import
creates a locally named binding, export-from creates an export entry.

As an example:

```js
export {v} from "mod";
```

Is symmetric to:

```js
import {v} from "mod";
```

#### Table showing symmetry

Statement Form                          | [[ModuleRequest]] | [[ImportName]] | [[LocalName]]  | [[ExportName]]
--------------                          | ----------------- | -------------- | -------------- | --------------
`import v from "mod";`                  | `"mod"`           | `"default"`    | `"v"`          |
`import * as ns from "mod";`            | `"mod"`           | `"*"`          | `"ns"`         |
`import {x} from "mod";`                | `"mod"`           | `"x"`          | `"x"`          |
`export {x} from "mod";`                | `"mod"`           | `"x"`          | **null**       | `"x"`
`import {x as v} from "mod";`           | `"mod"`           | `"x"`          | `"v"`          |
`export {x as v} from "mod";`           | `"mod"`           | `"x"`          | **null**       | `"v"`
`export * from "mod";`                  | `"mod"`           | `"*"`          | **null**       | **null** (many)

### Compound statements

You can also import the default value and named values in a compound statement:

```js
import v, {x, y as w} from "mod";
// which is the same as:
import {default as v, x, y as w} from "mod";
```

As well as

```js
import v, * as ns from "mod";
```
