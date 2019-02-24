# Encoding Objects

Since we can decode objects we need to have a way to encode them into JavaScript objects as well. The `encode` expression is the way to do that:

```text
encode { name = "Bob" } /* Object */
encode variable /* Object */
```

The `encode` expression tries to encode a typed object into a JavaScript object \(`Object` type in Mint\), in case that it's impossible to do that you will get a nice error message. 

The general rule is that you can `encode` everything which can be `decode`ed.

Encoding data is useful when you want to convert it to Json:

```text
encode { name = "Bob" }
|> Json.stringify()
/* { "name": "Bob"} */
```

