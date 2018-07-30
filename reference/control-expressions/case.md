# case

A case expression looks like this:

```text
case (condition) {
  match1 => value1
  match2 => value2
  match3 => value3
  => defaultValue
}
```

It returns the value of the first branch that matches the condition, or the default if none matched.

There are some rules that will be enforced by either the parser or the compiler:

* the `condition` can be any type
* the matches of branches must be the same type as the condition.
* the values of the branches must be the same type

{% hint style="info" %}
`case` expressions are compiled to `if...else` statements.
{% endhint %}

