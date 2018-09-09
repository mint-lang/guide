# Decoding Objects

In order to process data from JavaScript in Mint, you must convert it from JavaScript:

* object `{ name: "Joe" }`
* array `[1, 2, 3]`
* number `0`
* string `"Joe"`
* `null`
* `undefined`

...to a Mint typed value.

The `decode` expression:

```text
decode object as String
```

...will try to convert the untyped value to a typed value. it returns a `Result(Object.Error, ...)`, which can be used in a [try expression](../control-expressions/try.md).

You can decode JavaScript values into Mint **primitive values** \(`String`, `Bool`, `Number`, `Time`\) **simple structures** \(`Maybe(a)`, `Array(a)`\) and **records** which only have **decodable values**.

{% hint style="info" %}
If you try to decode a Type which is not supported or try to decode something that is not an `Object`, you will get a nice error message.
{% endhint %}

An example of decoding a simple record:

```text
record User {
  name : String,
  age : Number
}

component Main {
  fun render : Html {
    try {
      object =
        Json.parse("{\"name\": \"John\", \"age\": 30 }")
        |> Maybe.toResult("Decode Error")

      user =
        decode object as User

      (<div>
        <{ user.name }>
      </div>)
    } catch Object.Error => error {
      <div><{ "Could not decode!" }></div>
    } catch String => error {
      <div><{ "Invalid JSON!" }></div>
    }
  }
}
```

In this case, `user` is a `Result(Object.Error, String)`.

## Manual decoding

TODO

