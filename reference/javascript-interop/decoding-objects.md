# Decoding Objects

There are times when you have a JavaScript object from somewhere, for example:

* from an HTTP request
* from a websocket message
* from event
* etc...

In order to use them in Mint you have to convert them to a typed object, and it's done through decoders.

A JavaScript object have the type `Object` which can be any JavaScript value including:

* object `{ name: "Joe" }`
* array `[1, 2, 3]`
* number `0`
* string `"Joe"`
* `null`
* `undefined`

A decode will try to convert the untyped value to a typed value.

## Automatic decoding

In mint there is a syntax feature which allows you decode **primitive values** \(`String`, `Bool`, `Number`, `Time`\) **simple structures** \(`Maybe(a)`, `Array(a)`\) and **records** which only have **decodable values**.

To decode an object use the `decode` keyword:

```text
decode object as String
```

The **decode expression** will return a `Result(Object.Error, a)` in the case of the example it will be `Result(Object.Error, String)` this allows you use it in a [try expression](../control-expressions/try.md).

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

## Manual decoding

TODO

