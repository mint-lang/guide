# if...else

The `if...else` conditional expression returns one of two values based on a condition. It looks like this:

```text
if (condition) {
  value1
} else {
  value2
}
```

There are some rules that will be enforced:

- The `else` branch must be present, if it's missing you will get a syntax error. This ensures you handle all possibilities.
- The `condition` must evaluate to type `Bool`.
- The values of both branches **must evaluate to the same type**

{% hint style="info" %}
Currently there is no shorthand for a conditional expression.
{% endhint %}
