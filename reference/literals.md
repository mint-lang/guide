# Literals

## Boolean

Represents the [Boolean type](https://en.wikipedia.org/wiki/Boolean_data_type). It has two possible values `true` and `false`.

```text
true
false
```

## Number

Represents the [Number type](https://developer.mozilla.org/en-US/docs/Glossary/Number) from JavaScript.

```text
3.14
42
-10
```

{% hint style="warning" %}
Currently there are no support for other representations such as hex or binary.
{% endhint %}

## String

Represents the [String type](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) from JavaScript.

```text
"hello world"
```

Escaping works as in JavaScript:

```text
"hello \"world\""
```

Strings can span multiple lines

```text
"hello
world"
```

or can be split into smaller consecutive parts

```text
"hello " \
"world" == "hello world"
```

## Array

An Array is a generic type containing elements of any other type.

It is typically created with an array literal:

```text
[1, 2, 3]
```

