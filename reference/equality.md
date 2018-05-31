# Equality

In Mint equality is handled in **logical way** meaning that what **seems to be equal should be equal.**

For example two records with the same type and values should be equal:

```text
{ name = "Jon Doe" } == { name = "Jon Doe" }
```

or two `Maybe` with same value should be equal:

```text
Maybe.just("A") == Maybe.just("A")
```

or just take an `Array` with the same items which should be equal:

```text
["A"] == ["A"]
```

In many languages \(for example JavaScript\) these type of comparisons would return false, which leads to bugs because it seems logical for these to be true.

In Mint there is a special algorithm for checking the quality of two entities. 

Alongside with **records**, and **enums**, the following types have this kind of equality implemented:

* `String`
* `Number`
* `Boolean`
* `Array`
* `FormData`
* `Date`
* `Maybe`
* `Result`

## Fallback

Since Mint is compiled to JavaScript any type that does not have  a custom comparison algorithm will fall back to use the **strict equality operator** `===`

