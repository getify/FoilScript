# FoilScript

FoilScript: a new dialect of JS that fixes the sucky parts but still looks and feels like JS.

## What's out
JS "stuff" that FoilScript will not have:

* `typeof null === "object"`
* `with`
* `eval()`
* ASI
* `class`
* `new`
* "inheritance"
* `document.write()`
* ...probably more

## What's in
FoilScript will have this "stuff" that JS doesn't:

* `#` operator for soft-binding of `this` (I hope, I dunno)
* `@` operator for statement-localized continuations (I hope, I dunno)
* `a ? b` shortened "ternary" where the `:` clause is optional and defaulted to `undefined`
* regular expressions will have a `/n` flag that lets you turn off defaulted capturing of `( )` groups
* a few new annotations (similar to asm.js) that let you control implicit coercions more sanely
* the compiler will include some "linting" like the rules proposed in ("use restrict";)[http://restrictmode.org]
* ...more

## Strategy

FoilScript will be extremely similar to (and almost syntax-compatible with) JavaScript. That's a key differentiator to something like CoffeeScript. The parts that are different will be small (but useful) compared to what's still valid JS.

Think of it a little bit like LESS compared to real CSS. LESS looks like CSS and has a few differences. As opposed to something like SASS (**not SCSS** but indentation-sensitive SASS) which is more like CoffeeScript to JS.

FoilScript's compiler will use a JS parser (hopefully an ES6 one) that has some tweaks to it. It will not rewrite most of your code, but will pass it through un-touched (also so different from CoffeeScript).

When it does have to re-write your code, it will "annotate" your compiled JS code with comments that include signals which the compiler can use to reverse-transpile from JS back into your source FoilScript. This should make it easier to collaborate with others who only write JS if you use FS. There will be tools for the transpiling (compiling) and the reversing.
