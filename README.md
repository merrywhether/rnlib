# Minimal build error repro

This demonstrates the build error that arises with the explicit
addition(/duplication) of `@babel/plugin-proposal-class-properties` in the
default babel config for
[`react-native-builder-bob`](https://github.com/callstack/react-native-builder-bob).
This package is a fresh invocation of `yarn create react-native-library`, and
the only changes are updating `src/index.tsx` and deleting the `example/`
directory.

The file `src/index.tsx` is a minimal clone of [`react-native-svg`'s `Symbol`
component](https://github.com/software-mansion/react-native-svg/blob/main/src/elements/Symbol.tsx).
It includes the bare minimum repro that requires all three of these features:

- `export default class`
- class name shadowing the `Symbol` global
- static class property

Removing the explicit plugin restores `@babel/preset-env`'s natural transform
ordering and allows this library to build without issue.

The easiest way to test this is to manually remove line 75 in
`node_modules/react-native-builder-bob/lib/utils/compile.js` in your local node
modules.

Created for
[react-native-builder-bob/pull/363](https://github.com/callstack/react-native-builder-bob/pull/363).
