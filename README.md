# Code Convention

This repository describes SitePen code conventions and provides a compatible [.jshintrc](.jshintrc).

## Code conventions

1. All code names and comments MUST be written in English.

### Naming

The following naming conventions MUST be used:

<table>
  <tr>
    <th>Construct</th><th>Convention</th>
  </tr>
  <tr>
    <td>package</td><td>lowerCamelCase</td>
  </tr>
  <tr>
    <td>module returning constructor (“class”)</td><td>UpperCamelCase</td>
  </tr>
  <tr>
    <td>all other modules</td><td>lowerCamelCase</td>
  </tr>
  <tr>
    <td>constants</td><td>UPPER_CASE_WITH_UNDERSCORES</td>
  </tr>
  <tr>
    <td>variables</td><td>lowerCamelCase or _lowerCamelCase</td>
  </tr>
  <tr>
    <td>parameters</td><td>lowerCamelCase or _lowerCamelCase</td>
  </tr>
  <tr>
    <td>public properties</td><td>lowerCamelCase</td>
  </tr>
  <tr>
    <td>protected/private properties</td><td>_lowerCamelCase</td>
  </tr>
</table>

<table>
  <tr>
    <th>Variable type</th><th>Convention</th>
  </tr>
  <tr>
    <td>Deferred</td><td>dfd</td>
  </tr>
  <tr>
    <td>Promise</td><td>promise</td>
  </tr>
  <tr>
    <td>Identifier</td><td>id</td>
  </tr>
  <tr>
    <td>Numeric iterator</td><td>i, j, k, l</td>
  </tr>
  <tr>
    <td>String iterator (for-in)</td><td>k, key</td>
  </tr>
  <tr>
    <td>Event</td><td>event</td>
  </tr>
  <tr>
    <td>Remover handle</td><td>handle</td>
  </tr>
  <tr>
    <td>Error object</td><td>error</td>
  </tr>
  <tr>
    <td>Keyword arguments object</td><td>kwArgs</td>
  </tr>
  <tr>
    <td>Origin, source, from</td><td>source</td>
  </tr>
  <tr>
    <td>Destination, target, to</td><td>target</td>
  </tr>
  <tr>
    <td>Coordinates</td><td>x, y, z, width, height, depth</td>
  </tr>
  <tr>
    <td>All others</td><td>Do not abbreviate</td>
  </tr>
</table>

1. All names SHOULD be as clear as necessary, SHOULD NOT be contracted just for
   the sake of less typing, and MUST avoid unclear shortenings and
   contractions (e.g. `MouseEventHandler`, not `MseEvtHdlr` or `hdl` or
   `h`).
1. Abbreviations and acronyms MUST NOT be uppercase when used as a name (i.e.
   `getXml` not `getXML`).
1. Collections MUST be named using a plural form.
1. Names representing boolean states SHOULD start with `is`, `has`, `can`, or
   `should`.
1. Names representing boolean states MUST NOT be negative (i.e. `isNotFoo` is
   unacceptable).
1. Names representing a count of a number of objects SHOULD start with `num`.
1. Names representing methods SHOULD be verbs or verb phrases (i.e.
   `getValue()`, not `value()`).
1. Non-constructor methods that generate new objects SHOULD use the verb
   “create”.
1. Magic numbers MUST either be represented using a constant or be prefixed
   with a comment representing the literal value of the number (e.g.
   `if (event.keyCode === Keys.KEY_A)` or
   `if (event.keyCode === /* "a" */ 97)`).

### Style

Most style convention matters are addressed by the mandated jshint options.
Those that are not are listed here:

1. Opening bracket of a code block MUST be written on the same line as its
   statement:

   ```javascript
   // right
   if (foo) {

   }

   // wrong
   if (foo)
   {

   }
   ```

1. Blocks with a single statement MUST NOT be written on the same line as the
   opening bracket.

   ```javascript
   // right
   if (foo) {
       bar;
   }

   // wrong
   if (foo) { bar; }
   ```

1. The opening and closing brackets on objects and arrays MUST be surrounded by
   whitespace on the inside of the object literal:

   ```javascript
   // right
   var obj = { foo: 'foo' },
       arr = [ obj, 'foo' ];

   // wrong
   var obj = {foo: 'foo'},
       arr = [obj, 'foo'];
   ```

1. `case` statements inside switches that are intended to fall through to the
   next statement MUST end with a line containing a single comment
   `// fall through`.
1. `else` and `while` keywords must be on their own line, not cuddled with the
   closing bracket of the previous `if`/`do` block. This is consistent with the
   use of all other block statements and allows comments to be placed
   consistently before conditional statements, rather than sometimes-before,
   sometimes-inside.
1. `var` declarations that declare multiple variables at once must always put
   each variable identifier on its own line. This prevents variable
   declarations being lost inside long lists that may also include immediate
   assignments.
1. The most appropriate data types SHOULD be used in all cases (i.e. boolean for
   booleans, not number).
1. Files MUST end with an empty line.


## Documentation

1. All public APIs MUST be commented using
   [jsdoc](https://code.google.com/p/jsdoc-toolkit/wiki/TagReference), following the
   [Closure Compiler type expressions syntax](https://developers.google.com/closure/compiler/docs/js-for-compiler)
   for type definitions.
1. Comments MUST be added when intentionally making a change to code that
   appears wrong or inefficient.
1. Code SHOULD be written to be as self-documenting as possible. Comments
   SHOULD be used to explain *why* a particular piece of code was written (or
   why it was written the way it was), not *what* the code does. If code is so
   confusing that it is not clear on its own, it SHOULD be rewritten to be
   clearer.
1. Shorthand reference to a property of a module MUST use dot notation.
   e.g. `foo/module/id.fooFunction`.
2. Shorthand reference to a property of a prototype MUST use hash notation.
   e.g. `foo/module/Constructor#fooFunction`.


## Linting

Code committed to this repository should follow the jshint rules given in the
`.jshintrc` file. Unless otherwise noted, these options MUST NOT be overridden
using `/*jshint*/`.

### Rationales

* `asi`: Relying on ASI is sloppy and leads to inadvertent code breakage in
  edge cases. Using semicolons only in these edge cases requires all authors
  to be aware of them and means semicolons are used inconsistently.
* `bitwise`: Bitwise operators are useful in a wide variety of code and should
  not generally be restricted. Code reviews ensure bitwise operators are not
  accidentally used instead of logical operators.
* `boss`: Intentional assignment within conditionals should be done by wrapping
  the assignment in an extra set of parens.
* `browser`: Most Dojo Toolkit code is designed to run within browser
  environments, so predefining browser globals is desirable. Code that should
  never run within a browser environment should use
  `/*jshint browser:false */`.
* `camelcase`: This option is enabled to ensure consistent variable naming
  conventions that match those defined by the language.
* `couch`: Dojo Toolkit code is not usually designed to run within CouchDB
  environments. This may be set true with a `/*jshint*/` comment for files
  designed to run within CouchDB.
* `curly`: This options is enabled to ensure codebase consistency.
* `debug`: This option is disabled because no code should be committed to the
  repository with debugger statements.
* `devel`: This option is enabled because all platforms supported by the
  toolkit have the global `console` object, and the build system can strip
  console calls for production deployments. `console` methods are used to
  inform developers that they may not be using the toolkit properly.
* `dojo`: This option is disabled because it defines global `dojo`, `dijit`,
  and `dojox` objects, but these objects should never be used by new code.
  The two globals used by the toolkit, `define` and `require`, are defined
  in the `predef` array.
* `eqeqeq`: Even extremely experienced JavaScript programmers do not understand
  all the type coercion rules of JavaScript, which leads to subtle programming
  errors in edge cases. Additionally, non-strict equality can sometimes lead to
  confusion as to what types of input are intended to be accepted by a given
  statement. If type coercion is desired when performing a direct equality
  check, it should be done manually (e.g. `"" + foo === "" + bar`).
* `eqnull`: Non-strict equality to `null` may still be performed as this is the
  cleanest way to check whether a value is either `null` or `undefined`.
* `es3`: All code in version 2 of the toolkit runs only in EcmaScript 5
  environments.
* `esnext`: Code in version 2 of the toolkit should not use ES6 syntaxes.
* `evil`: In order to discourage the incorrect use of `eval` in codebases that
  follow the Dojo code conventions, this option is false by default. However,
  there are situations where the use of `eval` is necessary. In these cases,
  this option may be set to true using `/*jshint*/`.
* `expr`: The use of an expression statement to conditionally evaluate code is
  often clearer than wrapping the code inside a true conditional.
* `forin`: The toolkit requires an ES5 environment, which means users may
  augment `Object.prototype` with non-enumerable properties without breaking
  for-in loops. Therefore, there is no reason to filter these loops.
* `funcscope`: When authoring code, declaring variables as close to the point
  where they are first used is preferred as it helps to cluster groups of code
  together instead of spreading them throughout a function.
* `gcl`: These are our standards, not Google’s.
* `globalstrict`: Global `"use strict"` breaks third-party code. Since Dojo
  code is never executed in global scope, this should not matter, but is
  provided for completeness.
* `immed`: Immediately invoked function expressions should be wrapped in parens
  for consistency and to ensure that readers of the code understand that the
  value being assigned is the output of the function and not the function
  itself.
* `iterator`: The use of non-standard JavaScript engine properties violates
  cross-platform compatibility and future-proofness, so is forbidden.
* `jquery`: Dojo Toolkit does not access global objects of other libraries.
* `lastsemic`: For consistency, semicolons are required at the end of all
  statements.
* `latedef`: Define after use is a very common pattern that occurs when
  two functions defined within a scope reference one-another through closure.
* `laxbreak`: This has caused enough false positives in the past that it is
  currently disabled.
* `laxcomma`: Comma-first coding style is forbidden by the Dojo style
  guidelines.
* `loopfunc`: XXX rationale
* `mootools`: Dojo Toolkit does not access global objects of other libraries.
* `moz`: Dojo Toolkit code is not usually designed to run within Mozilla JS
  extensions. This may be set true with a `/*jshint*/` comment for files
  designed to run within Mozilla extensions.
* `multistr`: The use of multi-line string syntax virtually always results in
  incorrect code indentation, so is disallowed.
* `newcap`: An uppercase first letter is the only way to notate an object as
  being a constructor that requires the `new` keyword, so this convention is
  enforced.
* `noarg`: In order to discourage the incorrect use of `arguments` in codebases
  that follow the Dojo code conventions, this option is false by default.
  However, there are situations where the use of `arguments.callee` is
  necessary. In these cases, this option may be set to false using
  `/*jshint*/`.
* `node`: The majority of toolkit code is designed to run in the browser, so
  this option is false by default to avoid accidental use of Node.js globals
  in the most common cases. Files that are designed to run in Node.js and
  access its global objects may set this to true using `/*jshint*/`.
* `noempty`: Empty blocks are occasionally useful when iterating using `while`
  or when writing complex conditionals to be easier to understand, so are
  allowed. In the case of conditionals, it is recommended that a comment
  `// do nothing` be added to the empty block to make clear it is intended to
  do nothing.
* `nonew`: XXX rationale
* `nonstandard`: The only two non-standard globals are `escape` and `unescape`;
  the standard `encodeURIComponent` and `decodeURIComponent` should be used
  instead.
* `nomen`: For consistency, dangling underscores at the ends of variables are
  disallowed.
* `onecase`: A switch with one case should be written as an if or if/else
  statement for consistency. *n.b. This option is obsolete in jshint.*
* `onevar`: Same rationale as `funcscope`.
* `passfail`: Stopping at one error simply obfuscates other errors.
* `phantom`: Dojo Toolkit code is not usually designed to run within
  PhantomJS environments. This may be set true with a `/*jshint*/` comment for
  files designed to run within PhantomJS.
* `plusplus`: Unary increment/decrement operators are extremely useful,
  widely used, and widely understood.
* `proto`: The `__proto__` object is not available on all supported platforms,
  so may not be used.
* `prototypejs`: Dojo Toolkit does not access global objects of other
  libraries.
* `regexdash`: Unescaped dash at the end of a character group is common and
  harmless. *n.b. This option is obsolete in jshint.*
* `regexp`: Dot in regular expressions is common and harmless. *n.b. This
  option is obsolete in jshint.*
* `rhino`: Dojo Toolkit code is not usually designed to run within Rhino
  environments. This may be set true with a `/*jshint*/` comment for files
  designed to run within Rhino.
* `scripturl`: It’s extremely unlikely anyone would ever do this. If they
  do, it’s probably for a good reason.
* `shadow`: Variable shadowing is common and is preferable to generating new
  verbose identifier names just to avoid shadowing, especially in cases where
  variables from the closure are not used.
* `shelljs`: Dojo Toolkit code is not usually designed to run within ShellJS
  environments. This may be set true with a `/*jshint*/` comment for files
  designed to run within ShellJS.
* `smarttabs`: While the toolkit uses hard tabs for indentation, it is
  still important to be able to sometimes align sections of indented code
  precisely using spaces to improve readability. Additionally, jshint has
  historically triggered on code comments that mix spaces and tabs, which is
  not desirable in any scenario.
* `strict`: Strict mode is not supported across all platforms supported by the
  toolkit, which means that code will execute differently on different
  platforms if `"use strict"` is enabled. Furthermore, certain frameworks like
  .NET walk call chains using `arguments.callee` and will break if any function
  within the call chain uses `"use strict"`. Since strict mode provides no
  substantial benefit when code is already being passed through a linter, its
  use within the toolkit is forbidden.
* `sub`: Rarely, array notation is used instead of dot notation to prevent
  build tools from processing or mangling certain sections of code. This should
  be extremely uncommon in new toolkit code, however, so the more efficient dot
  notation is preferred for the sake of consistency. In a situation where array
  notation is necessary, this option may be set to true using `/*jshint*/`.
* `supernew`: As the toolkit uses AMD modules, the creation of singletons
  will generally never require the use of `new function` syntax. However, if
  a situation arises where this is necessary, this option may be set to true
  using `/*jshint*/`.
* `trailing`: Trailing whitespace makes the code look unprofessional.
* `undef`: This option prevents the accidental creation or use of global
  variables.
* `unused`: This option prevents the accidental creation of unused variables.
* `validthis`: Since strict mode is verboten, the value of this setting does
  not matter, so it defaults to `true` (the default for jshint).
* `withstmt`: The `with` statement prevents minification of code blocks and
  ruins JIT performance and so is verboten.
* `white`: Because the toolkit is written by a wide variety of contributors, a
  mechanism for programmatically ensuring whitespace consistency is strongly
  needed in order to ensure that the codebase looks and feels cohesive. This is
  the only mechanism for ensuring whitespace consistency that is available, and
  its rules are not unreasonable. Therefore, it is enabled.
* `worker`: Dojo Toolkit code is not usually designed to run within Web Worker
  environments. This may be set true with a `/*jshint*/` comment for files
  designed to run within Web Workers.
* `wsh`: Dojo Toolkit code is not usually designed to run within WSH
  environments. This may be set true with a `/*jshint*/` comment for files
  designed to run within WSH.
* `yui`: Dojo Toolkit does not access global objects of other libraries.
* `maxlen`: Lines should be kept to 120 charaters at maximum, but sometimes it
  can be clearer to go just over the limit, so this may be changed with
  `/*jshint*/` if it makes sense.
* `indent`: Same rationale as `white`. An indent value of 4 is enforced because
  it is the most commonly used indent size. Since the toolkit uses hard tabs,
  you may set your editor to whatever indent size you prefer, but jshint will
  always assume that one tab equals four spaces for the purposes of code
  validation.
* `maxerr`: Provided as a consistent default in case JSHint ever changes its
  default. A high value is used to allow all errors to display for all but the
  most badly mangled files.
* `predef`: The only global variables that toolkit code should use are
  `require` and `define`.
* `quotmark`: Same rationale as `white`. A single quote is enforced because it
  requires one fewer keystroke on standard QWERTY keyboards.
* `maxcomplexity`: In order to avoid creating massive, unmaintainable
  functions, a default cyclomatic complexity limit of 10 is enforced on all
  toolkit code. If an individual function can justify an increased complexity
  limit, `/*jshint*/` may be used within the function to increase the limit as
  long as a comment justifying the increase is also provided. Refactoring code
  that violates the complexity limit is preferred.
