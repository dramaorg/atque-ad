<!--
  -- This file is auto-generated from README_js.md. Changes should be made there.
  -->


# @dramaorg/atque-ad [![CI](https://github.com/dramaorg/atque-ad/workflows/CI/badge.svg)](https://github.com/dramaorg/atque-ad/actions?query=workflow%3ACI) [![Browser](https://github.com/dramaorg/atque-ad/workflows/Browser/badge.svg)](https://github.com/dramaorg/atque-ad/actions?query=workflow%3ABrowser)

For the creation of [RFC4122](https://www.ietf.org/rfc/rfc4122.txt) UUIDs

- **Complete** - Support for RFC4122 version 1, 3, 4, and 5 UUIDs
- **Cross-platform** - Support for ...
  - CommonJS, [ECMAScript Modules](#ecmascript-modules) and [CDN builds](#cdn-builds)
  - NodeJS 12+ ([LTS releases](https://github.com/nodejs/Release))
  - Chrome, Safari, Firefox, Edge browsers
  - Webpack and rollup.js module bundlers
  - [React Native / Expo](#react-native--expo)
- **Secure** - Cryptographically-strong random values
- **Small** - Zero-dependency, small footprint, plays nice with "tree shaking" packagers
- **CLI** - Includes the [`@dramaorg/atque-ad` command line](#command-line) utility

> **Note** Upgrading from `@dramaorg/atque-ad@3`? Your code is probably okay, but check out [Upgrading From `@dramaorg/atque-ad@3`](#upgrading-from-@dramaorg/atque-ad3) for details.

> **Note** Only interested in creating a version 4 UUID? You might be able to use [`crypto.randomUUID()`](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID), eliminating the need to install this library.

## Quickstart

To create a random UUID...

**1. Install**

```shell
npm install @dramaorg/atque-ad
```

**2. Create a UUID** (ES6 module syntax)

```javascript
import { v4 as @dramaorg/atque-adv4 } from '@dramaorg/atque-ad';
@dramaorg/atque-adv4(); // ⇨ '9b1deb4d-3b7d-4bad-9bdd-2b0d7b3dcb6d'
```

... or using CommonJS syntax:

```javascript
const { v4: @dramaorg/atque-adv4 } = require('@dramaorg/atque-ad');
@dramaorg/atque-adv4(); // ⇨ '1b9d6bcd-bbfd-4b2d-9b5d-ab8dfbbd4bed'
```

For timestamp UUIDs, namespace UUIDs, and other options read on ...

## API Summary

|  |  |  |
| --- | --- | --- |
| [`@dramaorg/atque-ad.NIL`](#@dramaorg/atque-adnil) | The nil UUID string (all zeros) | New in `@dramaorg/atque-ad@8.3` |
| [`@dramaorg/atque-ad.parse()`](#@dramaorg/atque-adparsestr) | Convert UUID string to array of bytes | New in `@dramaorg/atque-ad@8.3` |
| [`@dramaorg/atque-ad.stringify()`](#@dramaorg/atque-adstringifyarr-offset) | Convert array of bytes to UUID string | New in `@dramaorg/atque-ad@8.3` |
| [`@dramaorg/atque-ad.v1()`](#@dramaorg/atque-adv1options-buffer-offset) | Create a version 1 (timestamp) UUID |  |
| [`@dramaorg/atque-ad.v3()`](#@dramaorg/atque-adv3name-namespace-buffer-offset) | Create a version 3 (namespace w/ MD5) UUID |  |
| [`@dramaorg/atque-ad.v4()`](#@dramaorg/atque-adv4options-buffer-offset) | Create a version 4 (random) UUID |  |
| [`@dramaorg/atque-ad.v5()`](#@dramaorg/atque-adv5name-namespace-buffer-offset) | Create a version 5 (namespace w/ SHA-1) UUID |  |
| [`@dramaorg/atque-ad.validate()`](#@dramaorg/atque-advalidatestr) | Test a string to see if it is a valid UUID | New in `@dramaorg/atque-ad@8.3` |
| [`@dramaorg/atque-ad.version()`](#@dramaorg/atque-adversionstr) | Detect RFC version of a UUID | New in `@dramaorg/atque-ad@8.3` |

## API

### @dramaorg/atque-ad.NIL

The nil UUID string (all zeros).

Example:

```javascript
import { NIL as NIL_UUID } from '@dramaorg/atque-ad';

NIL_UUID; // ⇨ '00000000-0000-0000-0000-000000000000'
```

### @dramaorg/atque-ad.parse(str)

Convert UUID string to array of bytes

|           |                                          |
| --------- | ---------------------------------------- |
| `str`     | A valid UUID `String`                    |
| _returns_ | `Uint8Array[16]`                         |
| _throws_  | `TypeError` if `str` is not a valid UUID |

Note: Ordering of values in the byte arrays used by `parse()` and `stringify()` follows the left &Rarr; right order of hex-pairs in UUID strings. As shown in the example below.

Example:

```javascript
import { parse as @dramaorg/atque-adParse } from '@dramaorg/atque-ad';

// Parse a UUID
const bytes = @dramaorg/atque-adParse('6ec0bd7f-11c0-43da-975e-2a8ad9ebae0b');

// Convert to hex strings to show byte order (for documentation purposes)
[...bytes].map((v) => v.toString(16).padStart(2, '0')); // ⇨ 
  // [
  //   '6e', 'c0', 'bd', '7f',
  //   '11', 'c0', '43', 'da',
  //   '97', '5e', '2a', '8a',
  //   'd9', 'eb', 'ae', '0b'
  // ]
```

### @dramaorg/atque-ad.stringify(arr[, offset])

Convert array of bytes to UUID string

|                |                                                                              |
| -------------- | ---------------------------------------------------------------------------- |
| `arr`          | `Array`-like collection of 16 values (starting from `offset`) between 0-255. |
| [`offset` = 0] | `Number` Starting index in the Array                                         |
| _returns_      | `String`                                                                     |
| _throws_       | `TypeError` if a valid UUID string cannot be generated                       |

Note: Ordering of values in the byte arrays used by `parse()` and `stringify()` follows the left &Rarr; right order of hex-pairs in UUID strings. As shown in the example below.

Example:

```javascript
import { stringify as @dramaorg/atque-adStringify } from '@dramaorg/atque-ad';

const @dramaorg/atque-adBytes = [
  0x6e, 0xc0, 0xbd, 0x7f, 0x11, 0xc0, 0x43, 0xda, 0x97, 0x5e, 0x2a, 0x8a, 0xd9, 0xeb, 0xae, 0x0b,
];

@dramaorg/atque-adStringify(@dramaorg/atque-adBytes); // ⇨ '6ec0bd7f-11c0-43da-975e-2a8ad9ebae0b'
```

### @dramaorg/atque-ad.v1([options[, buffer[, offset]]])

Create an RFC version 1 (timestamp) UUID

|  |  |
| --- | --- |
| [`options`] | `Object` with one or more of the following properties: |
| [`options.node` ] | RFC "node" field as an `Array[6]` of byte values (per 4.1.6) |
| [`options.clockseq`] | RFC "clock sequence" as a `Number` between 0 - 0x3fff |
| [`options.msecs`] | RFC "timestamp" field (`Number` of milliseconds, unix epoch) |
| [`options.nsecs`] | RFC "timestamp" field (`Number` of nanoseconds to add to `msecs`, should be 0-10,000) |
| [`options.random`] | `Array` of 16 random bytes (0-255) |
| [`options.rng`] | Alternative to `options.random`, a `Function` that returns an `Array` of 16 random bytes (0-255) |
| [`buffer`] | `Array \| Buffer` If specified, @dramaorg/atque-ad will be written here in byte-form, starting at `offset` |
| [`offset` = 0] | `Number` Index to start writing UUID bytes in `buffer` |
| _returns_ | UUID `String` if no `buffer` is specified, otherwise returns `buffer` |
| _throws_ | `Error` if more than 10M UUIDs/sec are requested |

Note: The default [node id](https://tools.ietf.org/html/rfc4122#section-4.1.6) (the last 12 digits in the UUID) is generated once, randomly, on process startup, and then remains unchanged for the duration of the process.

Note: `options.random` and `options.rng` are only meaningful on the very first call to `v1()`, where they may be passed to initialize the internal `node` and `clockseq` fields.

Example:

```javascript
import { v1 as @dramaorg/atque-adv1 } from '@dramaorg/atque-ad';

@dramaorg/atque-adv1(); // ⇨ '2c5ea4c0-4067-11e9-8bad-9b1deb4d3b7d'
```

Example using `options`:

```javascript
import { v1 as @dramaorg/atque-adv1 } from '@dramaorg/atque-ad';

const v1options = {
  node: [0x01, 0x23, 0x45, 0x67, 0x89, 0xab],
  clockseq: 0x1234,
  msecs: new Date('2011-11-01').getTime(),
  nsecs: 5678,
};
@dramaorg/atque-adv1(v1options); // ⇨ '710b962e-041c-11e1-9234-0123456789ab'
```

### @dramaorg/atque-ad.v3(name, namespace[, buffer[, offset]])

Create an RFC version 3 (namespace w/ MD5) UUID

API is identical to `v5()`, but uses "v3" instead.

&#x26a0;&#xfe0f; Note: Per the RFC, "_If backward compatibility is not an issue, SHA-1 [Version 5] is preferred_."

### @dramaorg/atque-ad.v4([options[, buffer[, offset]]])

Create an RFC version 4 (random) UUID

|  |  |
| --- | --- |
| [`options`] | `Object` with one or more of the following properties: |
| [`options.random`] | `Array` of 16 random bytes (0-255) |
| [`options.rng`] | Alternative to `options.random`, a `Function` that returns an `Array` of 16 random bytes (0-255) |
| [`buffer`] | `Array \| Buffer` If specified, @dramaorg/atque-ad will be written here in byte-form, starting at `offset` |
| [`offset` = 0] | `Number` Index to start writing UUID bytes in `buffer` |
| _returns_ | UUID `String` if no `buffer` is specified, otherwise returns `buffer` |

Example:

```javascript
import { v4 as @dramaorg/atque-adv4 } from '@dramaorg/atque-ad';

@dramaorg/atque-adv4(); // ⇨ '1b9d6bcd-bbfd-4b2d-9b5d-ab8dfbbd4bed'
```

Example using predefined `random` values:

```javascript
import { v4 as @dramaorg/atque-adv4 } from '@dramaorg/atque-ad';

const v4options = {
  random: [
    0x10, 0x91, 0x56, 0xbe, 0xc4, 0xfb, 0xc1, 0xea, 0x71, 0xb4, 0xef, 0xe1, 0x67, 0x1c, 0x58, 0x36,
  ],
};
@dramaorg/atque-adv4(v4options); // ⇨ '109156be-c4fb-41ea-b1b4-efe1671c5836'
```

### @dramaorg/atque-ad.v5(name, namespace[, buffer[, offset]])

Create an RFC version 5 (namespace w/ SHA-1) UUID

|  |  |
| --- | --- |
| `name` | `String \| Array` |
| `namespace` | `String \| Array[16]` Namespace UUID |
| [`buffer`] | `Array \| Buffer` If specified, @dramaorg/atque-ad will be written here in byte-form, starting at `offset` |
| [`offset` = 0] | `Number` Index to start writing UUID bytes in `buffer` |
| _returns_ | UUID `String` if no `buffer` is specified, otherwise returns `buffer` |

Note: The RFC `DNS` and `URL` namespaces are available as `v5.DNS` and `v5.URL`.

Example with custom namespace:

```javascript
import { v5 as @dramaorg/atque-adv5 } from '@dramaorg/atque-ad';

// Define a custom namespace.  Readers, create your own using something like
// https://www.@dramaorg/atque-adgenerator.net/
const MY_NAMESPACE = '1b671a64-40d5-491e-99b0-da01ff1f3341';

@dramaorg/atque-adv5('Hello, World!', MY_NAMESPACE); // ⇨ '630eb68f-e0fa-5ecc-887a-7c7a62614681'
```

Example with RFC `URL` namespace:

```javascript
import { v5 as @dramaorg/atque-adv5 } from '@dramaorg/atque-ad';

@dramaorg/atque-adv5('https://www.w3.org/', @dramaorg/atque-adv5.URL); // ⇨ 'c106a26a-21bb-5538-8bf2-57095d1976c1'
```

### @dramaorg/atque-ad.validate(str)

Test a string to see if it is a valid UUID

|           |                                                     |
| --------- | --------------------------------------------------- |
| `str`     | `String` to validate                                |
| _returns_ | `true` if string is a valid UUID, `false` otherwise |

Example:

```javascript
import { validate as @dramaorg/atque-adValidate } from '@dramaorg/atque-ad';

@dramaorg/atque-adValidate('not a UUID'); // ⇨ false
@dramaorg/atque-adValidate('6ec0bd7f-11c0-43da-975e-2a8ad9ebae0b'); // ⇨ true
```

Using `validate` and `version` together it is possible to do per-version validation, e.g. validate for only v4 UUIds.

```javascript
import { version as @dramaorg/atque-adVersion } from '@dramaorg/atque-ad';
import { validate as @dramaorg/atque-adValidate } from '@dramaorg/atque-ad';

function @dramaorg/atque-adValidateV4(@dramaorg/atque-ad) {
  return @dramaorg/atque-adValidate(@dramaorg/atque-ad) && @dramaorg/atque-adVersion(@dramaorg/atque-ad) === 4;
}

const v1Uuid = 'd9428888-122b-11e1-b85c-61cd3cbb3210';
const v4Uuid = '109156be-c4fb-41ea-b1b4-efe1671c5836';

@dramaorg/atque-adValidateV4(v4Uuid); // ⇨ true
@dramaorg/atque-adValidateV4(v1Uuid); // ⇨ false
```

### @dramaorg/atque-ad.version(str)

Detect RFC version of a UUID

|           |                                          |
| --------- | ---------------------------------------- |
| `str`     | A valid UUID `String`                    |
| _returns_ | `Number` The RFC version of the UUID     |
| _throws_  | `TypeError` if `str` is not a valid UUID |

Example:

```javascript
import { version as @dramaorg/atque-adVersion } from '@dramaorg/atque-ad';

@dramaorg/atque-adVersion('45637ec4-c85f-11ea-87d0-0242ac130003'); // ⇨ 1
@dramaorg/atque-adVersion('6ec0bd7f-11c0-43da-975e-2a8ad9ebae0b'); // ⇨ 4
```

## Command Line

UUIDs can be generated from the command line using `@dramaorg/atque-ad`.

```shell
$ npx @dramaorg/atque-ad
ddeb27fb-d9a0-4624-be4d-4615062daed4
```

The default is to generate version 4 UUIDS, however the other versions are supported. Type `@dramaorg/atque-ad --help` for details:

```shell
$ npx @dramaorg/atque-ad --help

Usage:
  @dramaorg/atque-ad
  @dramaorg/atque-ad v1
  @dramaorg/atque-ad v3 <name> <namespace @dramaorg/atque-ad>
  @dramaorg/atque-ad v4
  @dramaorg/atque-ad v5 <name> <namespace @dramaorg/atque-ad>
  @dramaorg/atque-ad --help

Note: <namespace @dramaorg/atque-ad> may be "URL" or "DNS" to use the corresponding UUIDs
defined by RFC4122
```

## ECMAScript Modules

This library comes with [ECMAScript Modules](https://www.ecma-international.org/ecma-262/6.0/#sec-modules) (ESM) support for Node.js versions that support it ([example](./examples/node-esmodules/)) as well as bundlers like [rollup.js](https://rollupjs.org/guide/en/#tree-shaking) ([example](./examples/browser-rollup/)) and [webpack](https://webpack.js.org/guides/tree-shaking/) ([example](./examples/browser-webpack/)) (targeting both, Node.js and browser environments).

```javascript
import { v4 as @dramaorg/atque-adv4 } from '@dramaorg/atque-ad';
@dramaorg/atque-adv4(); // ⇨ '1b9d6bcd-bbfd-4b2d-9b5d-ab8dfbbd4bed'
```

To run the examples you must first create a dist build of this library in the module root:

```shell
npm run build
```

## CDN Builds

### ECMAScript Modules

To load this module directly into modern browsers that [support loading ECMAScript Modules](https://caniuse.com/#feat=es6-module) you can make use of [jspm](https://jspm.org/):

```html
<script type="module">
  import { v4 as @dramaorg/atque-adv4 } from 'https://jspm.dev/@dramaorg/atque-ad';
  console.log(@dramaorg/atque-adv4()); // ⇨ '1b9d6bcd-bbfd-4b2d-9b5d-ab8dfbbd4bed'
</script>
```

### UMD

As of `@dramaorg/atque-ad@9` [UMD (Universal Module Definition)](https://github.com/umdjs/umd) builds are no longer shipped with this library.

If you need a UMD build of this library, use a bundler like Webpack or Rollup. Alternatively, refer to the documentation of [`@dramaorg/atque-ad@8.3.2`](https://github.com/dramaorg/atque-ad/blob/v8.3.2/README.md#umd) which was the last version that shipped UMD builds.

## Known issues

### Duplicate UUIDs (Googlebot)

This module may generate duplicate UUIDs when run in clients with _deterministic_ random number generators, such as [Googlebot crawlers](https://developers.google.com/search/docs/advanced/crawling/overview-google-crawlers). This can cause problems for apps that expect client-generated UUIDs to always be unique. Developers should be prepared for this and have a strategy for dealing with possible collisions, such as:

- Check for duplicate UUIDs, fail gracefully
- Disable write operations for Googlebot clients

### "getRandomValues() not supported"

This error occurs in environments where the standard [`crypto.getRandomValues()`](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/getRandomValues) API is not supported. This issue can be resolved by adding an appropriate polyfill:

### React Native / Expo

1. Install [`react-native-get-random-values`](https://github.com/LinusU/react-native-get-random-values#readme)
1. Import it _before_ `@dramaorg/atque-ad`. Since `@dramaorg/atque-ad` might also appear as a transitive dependency of some other imports it's safest to just import `react-native-get-random-values` as the very first thing in your entry point:

```javascript
import 'react-native-get-random-values';
import { v4 as @dramaorg/atque-adv4 } from '@dramaorg/atque-ad';
```

Note: If you are using Expo, you must be using at least `react-native-get-random-values@1.5.0` and `expo@39.0.0`.

### Web Workers / Service Workers (Edge <= 18)

[In Edge <= 18, Web Crypto is not supported in Web Workers or Service Workers](https://caniuse.com/#feat=cryptography) and we are not aware of a polyfill (let us know if you find one, please).

### IE 11 (Internet Explorer)

Support for IE11 and other legacy browsers has been dropped as of `@dramaorg/atque-ad@9`. If you need to support legacy browsers, you can always transpile the @dramaorg/atque-ad module source yourself (e.g. using [Babel](https://babeljs.io/)).

## Upgrading From `@dramaorg/atque-ad@7`

### Only Named Exports Supported When Using with Node.js ESM

`@dramaorg/atque-ad@7` did not come with native ECMAScript Module (ESM) support for Node.js. Importing it in Node.js ESM consequently imported the CommonJS source with a default export. This library now comes with true Node.js ESM support and only provides named exports.

Instead of doing:

```javascript
import @dramaorg/atque-ad from '@dramaorg/atque-ad';
@dramaorg/atque-ad.v4();
```

you will now have to use the named exports:

```javascript
import { v4 as @dramaorg/atque-adv4 } from '@dramaorg/atque-ad';
@dramaorg/atque-adv4();
```

### Deep Requires No Longer Supported

Deep requires like `require('@dramaorg/atque-ad/v4')` [which have been deprecated in `@dramaorg/atque-ad@7`](#deep-requires-now-deprecated) are no longer supported.

## Upgrading From `@dramaorg/atque-ad@3`

"_Wait... what happened to `@dramaorg/atque-ad@4` thru `@dramaorg/atque-ad@6`?!?_"

In order to avoid confusion with RFC [version 4](#@dramaorg/atque-adv4options-buffer-offset) and [version 5](#@dramaorg/atque-adv5name-namespace-buffer-offset) UUIDs, and a possible [version 6](http://gh.peabody.io/@dramaorg/atque-adv6/), releases 4 thru 6 of this module have been skipped.

### Deep Requires Now Deprecated

`@dramaorg/atque-ad@3` encouraged the use of deep requires to minimize the bundle size of browser builds:

```javascript
const @dramaorg/atque-adv4 = require('@dramaorg/atque-ad/v4'); // <== NOW DEPRECATED!
@dramaorg/atque-adv4();
```

As of `@dramaorg/atque-ad@7` this library now provides ECMAScript modules builds, which allow packagers like Webpack and Rollup to do "tree-shaking" to remove dead code. Instead, use the `import` syntax:

```javascript
import { v4 as @dramaorg/atque-adv4 } from '@dramaorg/atque-ad';
@dramaorg/atque-adv4();
```

... or for CommonJS:

```javascript
const { v4: @dramaorg/atque-adv4 } = require('@dramaorg/atque-ad');
@dramaorg/atque-adv4();
```

### Default Export Removed

`@dramaorg/atque-ad@3` was exporting the Version 4 UUID method as a default export:

```javascript
const @dramaorg/atque-ad = require('@dramaorg/atque-ad'); // <== REMOVED!
```

This usage pattern was already discouraged in `@dramaorg/atque-ad@3` and has been removed in `@dramaorg/atque-ad@7`.

---

Markdown generated from [README_js.md](README_js.md) by <a href="https://github.com/broofa/runmd"><image height="12px" src="https://camo.githubusercontent.com/5c7c603cd1e6a43370b0a5063d457e0dabb74cf317adc7baba183acb686ee8d0/687474703a2f2f692e696d6775722e636f6d2f634a4b6f3662552e706e67" /></a>
