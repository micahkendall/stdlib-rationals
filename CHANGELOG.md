# Changelog

## v1.2.0 - 2023-06-17

### Added

- [`transaction/value.MintedValue`](https://aiken-lang.github.io/stdlib/aiken/transaction/value.html#MintedValue)
- [`transaction/value.from_minted_value`](https://aiken-lang.github.io/stdlib/aiken/transaction/value.html#from_minted_value): Convert from `MintedValue` to `Value`
- [`transaction/value.to_minted_value`](https://aiken-lang.github.io/stdlib/aiken/transaction/value.html#to_minted_value): Convert from `Value` to `MintedValue`
- [`transaction/bytearray.to_hex`](https://aiken-lang.github.io/stdlib/aiken/bytearray.html#to_hex): Convert a `ByteArray` to a hex encoded `String`
- [`math/rational`](https://aiken-lang.github.io/stdlib/aiken/math/rational.html): Working with rational numbers.
    - [x] `abs`
    - [x] `add`
    - [x] `ceil`
    - [x] `compare`
    - [x] `compare_with`
    - [x] `div`
    - [x] `floor`
    - [x] `from_int`
    - [x] `mul`
    - [x] `negate`
    - [x] `new`
    - [x] `proper_fraction`
    - [x] `reciprocal`
    - [x] `reduce`
    - [x] `round`
    - [x] `round_even`
    - [x] `sub`
    - [x] `truncate`
    - [x] `zero`

### Removed

- module `MintedValue` was merged with `Value`

## v1.1.0 - 2023-06-06

### Added

- [`list.count`](https://aiken-lang.github.io/stdlib/aiken/list.html#count): Count how many items in the list satisfy the given predicate.

- [`int.from_utf8`](https://aiken-lang.github.io/stdlib/aiken/int.html#from_utf8): Parse an integer from a utf-8 encoded `ByteArray`, when possible.

- [`dict.foldl`](https://aiken-lang.github.io/stdlib/aiken/dict.html#foldl) & [`dict.foldr`](https://aiken-lang.github.io/stdlib/aiken/dict.html#foldr): for left and right folds over dictionnary elements in ascending key order.

- [`dict.insert_with`](https://aiken-lang.github.io/stdlib/aiken/dict.html#insert_with): Insert a value in the dictionary at a given key. When the key already exist, the provided merge function is called.

- [`transaction/value.add`](https://aiken-lang.github.io/stdlib/aiken/transaction/value.html#add): Add a (positive or negative) quantity of a single token to a value. This is more efficient than `merge` for a single asset.

- [`transaction/value.to_dict`](https://aiken-lang.github.io/stdlib/aiken/transaction/value.html#to_dict): Convert a `Value` into a dictionnary of dictionnaries.

- A new module [`transaction/minted_value`](https://aiken-lang.github.io/stdlib/aiken/transaction/minted_value.html): This is used exclusively for representing values present in the `mint` field of transactions. This allows to simplify some of the implementation for `Value` which no longer needs to handle the special case where null-quantity tokens would be present. It isn't possible to construct `MintedValue` by hand, they come from the script context entirely and are 'read-only'.

- More documentation for `dict` and `interval` modules.

### Changed

> **Warning**
>
> Most of those changes are breaking-changes. Though, given we're still in an
> alpha state, only the `minor` component is bumped from the version number.
> Please forgive us.

- Rework `list.{foldl, foldr, reduce, indexed_foldr}`, `dict.{fold}`, `bytearray.{foldl, foldr, reduce}` to take the iterator as last argument. For example:

  ```
  fn foldl(self: List<a>, with: fn(a, b) -> b, zero: b) -> b

  ↓ becomes

  fn foldl(self: List<a>, zero: b, with: fn(a, b) -> b) -> b
  ```

- Fixed implementation of `bytearray.slice`; `slice` would otherwise behave as if the second argument were an offset.

- Rename `transaction/value.add` into `transaction/value.merge`.

- Swap arguments of the merge function in `dict.union_with`; the first value received now corresponds to the value already present in the dictionnary.

- Fixed various examples from the documentation

### Removed

- Removed `dict.fold`; replaced with `dict.foldl` and `dict.foldr` to remove ambiguity.

## v1.0.0 - 2023-04-13

### Added

N/A

### Changed

N/A

### Removed

N/A
