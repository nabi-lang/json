# Changelog

All notable changes to this package. Versions follow semver, independent of the Nabi toolchain.

## 0.1.0 (unreleased)

First release.

- `Value` tree and a strict RFC 8259 parser (`parse`) with `line:col` errors.
- Compact and indented writers.
- `Tokenizer`: a streaming reader of events for large inputs.
- Typed conversion with `#[derive(Json)]` and the `ToJson` / `FromJson`
  traits: `from_str`, `to_str`, `to_value`, `from_value`, as in std's
  `nabion` module.
- JSON Pointer.
- Tested against JSONTestSuite. Needs Nabi 0.1 or later.
