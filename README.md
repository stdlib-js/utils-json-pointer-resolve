<!--

@license Apache-2.0

Copyright (c) 2026 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# resolve

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Resolve a [JSON Pointer][json-pointer] ([RFC 6901][rfc-6901]) against a document and return the target, key, and value.

<section class="installation">

## Installation

```bash
npm install @stdlib/utils-json-pointer-resolve
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm`][esm-url] branch (see [README][esm-readme]).
-   If you are using Deno, visit the [`deno`][deno-url] branch (see [README][deno-readme] for usage intructions).
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd`][umd-url] branch (see [README][umd-readme]).

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

To view installation and usage instructions specific to each branch build, be sure to explicitly navigate to the respective README files on each branch, as linked to above.

</section>

<section class="usage">

## Usage

```javascript
var resolve = require( '@stdlib/utils-json-pointer-resolve' );
```

#### resolve( document, pointer )

Resolves a [JSON Pointer][json-pointer] against a document and returns an object with `target`, `key`, and `value` properties.

```javascript
var obj = {
    'foo': [ 'bar', 'baz' ]
};
var out = resolve( obj, '/foo/0' );
// returns { 'target': [ 'bar', 'baz' ], 'key': 0, 'value': 'bar' }

obj = {
    'foo': 'bar'
};
out = resolve( obj, '/foo' );
// returns { 'target': { 'foo': 'bar' }, 'key': 'foo', 'value': 'bar' }

out = resolve( obj, '' );
// returns { 'target': null, 'key': null, 'value': { 'foo': 'bar' } }
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   Per [RFC 6901][rfc-6901], an empty string refers to the root of the document.
-   The `-` token on the last segment of a pointer targeting an array resolves to the array's length (i.e., past-the-end index).
-   Tokens `__proto__`, `constructor`, and `prototype` are rejected to prevent prototype pollution.
-   The returned `target` is the parent container (object or array) holding the referenced value. For root pointers, `target` and `key` are both `null`.

</section>

<!-- /.notes -->

<section class="examples">

<!-- eslint no-undef: "error" -->

## Examples

```javascript
var resolve = require( '@stdlib/utils-json-pointer-resolve' );

var doc = {
    'foo': [ 'bar', 'baz' ],
    '': 0,
    'a/b': 1,
    'm~n': 8
};

var out = resolve( doc, '/foo' );
// returns { 'target': { 'foo': [ 'bar', 'baz' ], '': 0, 'a/b': 1, 'm~n': 8 }, 'key': 'foo', 'value': [ 'bar', 'baz' ] }

out = resolve( doc, '/foo/0' );
// returns { 'target': [ 'bar', 'baz' ], 'key': 0, 'value': 'bar' }

out = resolve( doc, '/' );
// returns { 'target': { 'foo': [ 'bar', 'baz' ], '': 0, 'a/b': 1, 'm~n': 8 }, 'key': '', 'value': 0 }

out = resolve( doc, '/a~1b' );
// returns { 'target': { 'foo': [ 'bar', 'baz' ], '': 0, 'a/b': 1, 'm~n': 8 }, 'key': 'a/b', 'value': 1 }

out = resolve( doc, '/m~0n' );
// returns { 'target': { 'foo': [ 'bar', 'baz' ], '': 0, 'a/b': 1, 'm~n': 8 }, 'key': 'm~n', 'value': 8 }

out = resolve( doc, '' );
// returns { 'target': null, 'key': null, 'value': { 'foo': [ 'bar', 'baz' ], '': 0, 'a/b': 1, 'm~n': 8 } }
```

</section>

<!-- /.examples -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

## References

-   [RFC 6901 - JavaScript Object Notation (JSON) Pointer][rfc-6901]

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/utils-json-pointer-resolve.svg
[npm-url]: https://npmjs.org/package/@stdlib/utils-json-pointer-resolve

[test-image]: https://github.com/stdlib-js/utils-json-pointer-resolve/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/utils-json-pointer-resolve/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/utils-json-pointer-resolve/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/utils-json-pointer-resolve?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/utils-json-pointer-resolve.svg
[dependencies-url]: https://david-dm.org/stdlib-js/utils-json-pointer-resolve/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/utils-json-pointer-resolve/tree/deno
[deno-readme]: https://github.com/stdlib-js/utils-json-pointer-resolve/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/utils-json-pointer-resolve/tree/umd
[umd-readme]: https://github.com/stdlib-js/utils-json-pointer-resolve/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/utils-json-pointer-resolve/tree/esm
[esm-readme]: https://github.com/stdlib-js/utils-json-pointer-resolve/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/utils-json-pointer-resolve/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/utils-json-pointer-resolve/main/LICENSE

[json-pointer]: https://datatracker.ietf.org/doc/html/rfc6901

[rfc-6901]: https://datatracker.ietf.org/doc/html/rfc6901

</section>

<!-- /.links -->
