# ts-protoc-gen - Map issue

## Replication Steps

- `npm i` this repo
- `npm run gen` to generate the pb JS + TS files
- `npm run compile` to see the TypeScript compiler error/faillure

You can also `./gen.sh` to see the issue occur when calling `protoc` directly.

## Issue

`proto/test.proto` includes a message named `Map` and a message that implements a map internally:

```
message Map {
    string key = 1;
    string value = 2;
}

message Foo {
    map<string, string> fields = 1;
}
```

Generating the pb code with `npm run gen` leads to TypeScript compiler errors in `src/proto/test.ts`. The compiler can't tell the difference between the custom `Map` type and the `Map` built into TS.