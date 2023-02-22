# Minimal build error repro

This demonstrates the build error that arises with the explicit
addition(/duplication) of `@babel/plugin-proposal-class-properties` in the
default babel config for `react-native-builder-bob`.

It is a pocket-case that requires all three of these features:

- `export default class`
- class name shadowing the `Symbol` global
- static class property

Removing the explicit plugin restores `@babel/preset-env`'s natural transform
ordering and allows this library to build without issue.

The easiest way to test this is to manually remove line 75 in
`node_modules/react-native-builder-bob/lib/utils/compile.js` in your local node
modules.
