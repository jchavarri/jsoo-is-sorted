# jsoo-is-sorted

[js_of_ocaml](http://ocsigen.org/js_of_ocaml/) bindings for [is-sorted](https://www.npmjs.com/package/is-sorted).

Just for personal learning and educational purposes. In real life, just use `List.sort compare` :)

### Building vs bundling

For js_of_ocaml case, we use one tool for building and another for bundling:

- esy is used to gather the OCaml / ReasonML sources and all build tooling (OCaml compiler, Dune, etc).
- yarn (or npm) is used to gather the JavaScript dependencies from the bindings and also the bundling of resulting JS files.

### Installation

As mentioned above, this is not intended to be used. But if it was to be added to an existing project,
it would need both `esy.json` and `package.json`.

1. Run `yarn add jsoo-is-sorted`.
2. Run `esy add jsoo-is-sorted-esy`.
3. Add the library to your dune file:

```dune
(executable
  (name App)
  (libraries jsoo-is-sorted)
)
```

### Using it

```ocaml
let foo = IsSorted.isSorted [|20; 3; 124|]
```

Or with Reason syntax:

```reason
let foo = IsSorted.isSorted([|20, 3, 124|]);
```

### Publishing

Due to esy [not being able to read](https://esy.sh/docs/en/concepts.html#support-for-esyjson) `esy.json` files
from published npm packages (this is to prevent downloading and unpacking all tarballs to do version resolution),
the bindings are distributed in two packages.

To publish:
- Make sure both `esy.json` and `package.json` have the same version
- Run `npm publish` normally
- Delete `package.json`
- Rename `esy.json` to `package.json`
- Run `npm publish` again to publish `jsoo-is-sorted-esy`
