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

You can decode JavaScript values into Mint **primitive values** \(`String`, `Bool`, `Number`, `Time`\) **simple structures** \(`Maybe(a)`,`Set(a)`,`Map(a,b)`, `Array(a)`\) and **records** which only have **decodable values**.

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

In this case, `user` is a `Result(Object.Error, User)`.

## Decoding not supported names

There are times when we want to decode a key from an object into a record whats name is not supported as a record key for example `tag_list`. In this case we can use the `using` keyword to specify the mapping between the object and the record.

Here is an example:

```text
record Post {
  tagList: Array(String) using "tag_list"
}
```

When decoding an object as a `Post` it will look for the `tag_list` field instead of the `tagList` field in the object, so this JavaScript Object:

```javascript
{
  tag_list: ["a", "b"]
}
```

will decode into this record: 

```text
{
  tagList = ["a", "b"]
}
```

...it will use this key for the encoding as well.

