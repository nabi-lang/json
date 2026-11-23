# json

[![CI](https://github.com/nabi-lang/json/actions/workflows/ci.yml/badge.svg)](https://github.com/nabi-lang/json/actions/workflows/ci.yml) [![packages.nabi-lang.org](https://img.shields.io/github/v/tag/nabi-lang/json?label=packages.nabi-lang.org&sort=semver)](https://packages.nabi-lang.org/packages/json) [![License: MIT OR Apache-2.0](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue)](#license)

JSON ([RFC 8259](https://www.rfc-editor.org/rfc/rfc8259)) for Nabi: a `Value`
tree, a strict parser with `line:col` errors, compact and indented writers, a
streaming tokenizer for large inputs, typed conversion with
`#[derive(Json)]`, and JSON Pointer. The API follows std's `nabion` module:
`parse` / `to_str` / `from_str` / `to_value` / `from_value`, with `ToJson` /
`FromJson` traits.

## Add it

```sh
nabi add json
```

Needs Nabi 0.1 or later.

## Usage

```nabi
let v = try json::parse("{\"name\": \"geom\", \"sizes\": [1, 2.5, 12345678901234567890]}");
println(v.get("name")?.as_str() ?? "");          // geom
let big = v.pointer("/sizes/2")?.as_int() ?? 0;  // 12345678901234567890 (exact)
println(v.to_pretty(2));
```

Derive `Json` on your own types for typed `from_str` / `to_str`, and read
large inputs event by event with `Tokenizer`.

`parse` reads text straight into a `Value`: strings are found with
vectorized scans and, when they hold no escapes, share the input's
bytes instead of copying them; floats are read by the Eisel-Lemire
method (correctly rounded, the exact fallback only for the rare cases it
cannot decide). An invalid document is read again by the tokenizer for
the `line:col` error, so errors cost nothing on the happy path.

## Docs

https://docs.nabi-lang.org/packages/json/latest

## License

Licensed under either of [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE), at
your option. `tests/jsontestsuite.txt` is from JSONTestSuite, MIT License,
Copyright (c) 2016 Nicolas Seriot.
