# GX Examples

Example programs for the GX programming language, kept small and readable on purpose. If you are new to GX, read the numbered files in order. Each one covers one part of the language, and the comment at the top explains why the feature works the way it does, not just how to call it.

GX is a statically typed, procedural language for people who like knowing what their code turns into. It compiles natively through LLVM, or through C when you want to read and keep the generated source. There is no garbage collector and there are no hidden allocations. Structs have C layout, so C libraries bind directly, without a wrapper layer in between.

The numbering has some gaps and a few doubled numbers. Examples get added and reworked as the language moves, and I would rather keep stable names than renumber everything on each release.

## Running the examples

Get GX from [gxlang.org](https://gxlang.org), unpack it, and put the `gx` binary on your PATH. Then:

```
gx 02_variables.gx -o variables
./variables
```

That is the whole workflow. Most numbered examples are self contained and print to the console.

Some of the later ones (json, enet, SDL3, cimgui, clay) bind external C libraries through modules that ship with the GX release. The compiler finds them on its own, next to the `gx` binary, so these build the same way:

```
gx 45_json.gx -o json
```

If you keep modules somewhere unusual, point at them with `-I path/to/modules`.

## Coming from Python or JavaScript

More of GX will feel familiar than you might expect. String interpolation is an f-string with the letter dropped: `"hello {name}"`. A `map<str, i32>` is your dict or object. `for (var x in items)` reads the way you already write loops, and a `where` filter on it does what the condition in a comprehension does. Semicolons are optional. You can go a long way before the systems side of the language asks anything of you.

The real differences are three, and all of them are deliberate. First, GX compiles to a native executable: there is a build step, and types are checked before anything runs, so a whole class of errors you would meet at runtime in Python shows up while compiling instead. Second, there is no garbage collector. Most code never notices, but when something allocates, like `collect`, freeing it is your job, and the examples show where. Third, there are no exceptions. A function that can fail returns a value that says so, and you check it at the call site; `43_errors.gx` shows the patterns that replace try/except.

The early examples assume nothing. Read 01 through 13 in order and you will have the whole core of the language; the compile-time system (29 to 35) is where GX becomes something Python and JavaScript have no equivalent for.

## Demos

The `demos` folder holds small complete programs, games and graphics, built on sokol and raylib:

```
gx demos/sokol/snake.gx -o snake
```

The `*_web.gx` files are browser builds of the same demos. GX has a JS backend, so the playground on gxlang.org runs these without installing anything.
