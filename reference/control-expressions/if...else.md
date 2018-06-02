# if...else

The `if...else` conditional expression can return two different values based on a condition. 

An `if...else` expression looks like this:

```text
if (condition) {
  value1
} else {
  value2
}
```

There are some rules that will be enforced by either the parser or the compiler:

* The `else` branch must be present, if it's missing you will get a syntax error this is to make sure that all of the possibilities are covered
* The `condition` must evaluate to the type `Bool` this is checked by the compiler and will notify you if different
* The values of both branches **must evaluate to the same type**

{% hint style="info" %}
Currently there is no shorthand for a conditional expression.
{% endhint %}



