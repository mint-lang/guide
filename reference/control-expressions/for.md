# for

`for` is useful for iterating over either an `Array(a)` or a `Set(a)` or a `Map(a,b)`. The result if the iteration is always an array where the type of it's items is from the type of the expression.

In the next example we iterate over an array of Strings and making them uppercase:

```text
for (item of ["bob", "joe"]) {
  String.toUpperCase(item)
}
/* The result will be ["BOB", "JOE"]
```

The return type of this `for` expression is `Array(String)` 

#### Selecting items

You can limit the items for which the iteration should take place with an optional `when` block:

```text
for (item of ["bob", "joe"]) {
  String.toUpperCase(item)
} when {
  item == "bob"
}
/* The result will be ["BOB"]
```

In the example we specified that the expression should only run \(and return\) for items  which equals "bob".

