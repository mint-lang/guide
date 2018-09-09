# Equality

In Mint, 2 objects are considered equal if they have the same type and all values are equal. The equality operator is `==`.

These examples all evaluate to true:

```text
{ name = "Jon Doe", age=27 } == { age=27, name = "Jon Doe" }
Maybe.just("A") == Maybe.just("A")
["A"] == ["A"]
```

In JavaScript, the same `==` comparison would return false. We say Mint uses "logical" equality.

In addition to **records** and **enums**, the following types use logical equality:

* `String`
* `Number`
* `Boolean`
* `Array`
* `FormData`
* `Date`
* `Maybe`
* `Result`
* `Map`
* `Set`
* `SearchParams`

Types that have not implemented the logical equality operation fall back to using the JavaScript **strict equality operator** `===`

