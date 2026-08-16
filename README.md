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

Some of the later ones (json, enet, SDL3, cimgui, clay) bind external C libraries through modules that ship with the GX release. When a file starts with an `import`, build it with the modules folder on the include path:

```
gx 45_json.gx -I path/to/gx/modules -o json
```

## Demos

The `demos` folder holds small complete programs, games and graphics, built on sokol and raylib. Same rule as above, point `-I` at the modules folder:

```
gx demos/sokol/snake.gx -I path/to/gx/modules -o snake
```

The `*_web.gx` files are browser builds of the same demos. GX has a JS backend, so the playground on gxlang.org runs these without installing anything.
