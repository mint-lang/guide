# case

A `case` expression is useful for matching enums or exact values, while also supporting a default value.

A case expression looks like this:

```text
case (condition) {
  match1 => value1
  match2 => value2
  match3 => value3
  => defaultValue 
}
```

It returns the value of the branch that matches the condition.

There are some rules that will be enforced by either the parser or the compiler:

* the `condition` can be any type
* the matches of branches must be the same type as the condition
* the values of the branches must be the same type as the value of the first branch

{% hint style="info" %}
`case` expressions are compile to `if...else` statements.
{% endhint %}

