# FoilScript

FoilScript: a new ~~dialect~~ ~~accent~~ variant of JS that fixes the sucky parts but still looks and feels like JS.

## Why?
Some people will assume that I'm making FoilScript because I dislike JS. The truth is, I love JS. Seriously. I'm all in on JS. I just have things I don't like about it. In fact, there's a few things I hate about it.

The problem is, I've tried to get these things "fixed" in JS by making proposals, and I've been told several times, basically, "you're doing it wrong." Get shut down enough times, and you give up.

But I'm not giving up on JS. I'm just going to make the fixes myself. I'm not making a new language, I'm fixing what I hate about JS. The stuff that I love about JS is staying. FoilScript will look an awful lot like JS, on purpose. Because I love JS. And FoilScript will transpile to JS. In fact, most FoilScript will just be JS itself. Only the new stuff gets transpiled.

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

* `(a+b)*(c*d)` type expressions will automatically be [FOIL expanded](http://en.wikipedia.org/wiki/FOIL_method) to `a*c + a*d + b*c + b*d` (**note:** this part is kind of a joke but is the namesake feature for this language!)
* `NaN` will be renamed `InvalidNum`, in addition to `isNaN()` becoming `isInvalidNum()`
* `let (foo = 42) { .. }` styled let-block-statements (even though [ES6 abandoned](https://twitter.com/littlecalculist/status/318726015432159233) them) via something like [BlockScoper](https://github.com/getify/BlockScoper.js)'s technique
* `currentThis` [binding](https://gist.github.com/getify/5253319) for [determining where](https://gist.github.com/getify/5254459) in the `[[Prototype]]` chain the current executing function is found (basically `currentThis.__proto__` is equivalent to a `super`)
* `#` operator for [soft-binding of 'this'](https://gist.github.com/getify/4596011) (I hope, I dunno)
* `@` operator for [statement-localized continuations](https://gist.github.com/getify/727232) (I hope, I dunno)
* `a ? b` shortened "ternary" where the `:` clause is [optional and defaulted to](http://mozilla.6506.n7.nabble.com/Existential-operator-tp109073p109123.html) `undefined`
* regular expressions will have a ['/n' flag that lets you turn off defaulted capturing](https://mail.mozilla.org/pipermail/es-discuss/2012-March/021387.html) of `( )` groups
* a few new annotations (similar to asm.js) that let you control implicit coercions [more sanely](https://gist.github.com/getify/3057796)
* the compiler will include some "linting" like the rules proposed in ["use restrict";](http://restrictmode.org)
* ...more

## Strategy

FoilScript will be extremely similar to (and almost syntax-compatible with) JavaScript. That's a key differentiator to something like CoffeeScript. The parts that are different will be small (but useful) compared to what's still valid JS.

Think of it a little bit like LESS compared to real CSS. LESS looks like CSS and has a few differences. As opposed to something like SASS (**not SCSS** but indentation-sensitive SASS) which is more like CoffeeScript to JS.

FoilScript's compiler will use a JS parser (hopefully an ES6 one) that has some tweaks to it. It will not rewrite most of your code, but will pass it through un-touched (also so different from CoffeeScript).

When it does have to re-write your code, it will "annotate" your compiled JS code with comments that include signals which the compiler can use to reverse-transpile from JS back into your source FoilScript. This should make it easier to collaborate with others who only write JS if you use FS. There will be tools for the transpiling (compiling) and the reversing.
