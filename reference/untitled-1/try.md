# try

`try` is a control expression for **handling synchronous computations that might fail**, for example when you are trying to convert an **untyped** **JavaScript object** into a **typed Record.**

A try expression is built up from 3 parts:

* statements that returns a `Result`
* catch expressions
* a return expression

Let's see an example where we are using this expression to decode an object:

```text
record User {
  email : String,
  name : String
}

module Example {
  fun decodeUser (object : JSObject) : Result(Json.Error, User) {
    try {
      # Try to decode the email from the object,
      # if succeeds the value is assigned to the 
      # "email" variable.
      email = 
        object
        |> Json.Decoder.field("email", Json.Decoder.string)

      # Same for the name.
      name = 
        object
        |> Json.Decoder.field("name", Json.Decoder.string)

      # At this point we have the fields so we can return 
      # a result with the user.  
      Result.ok({
        email = email
        name = name
      })

    # If any of the decoders fail we handle it here and
    # return an result with the error.
    } catch Json.Error => error {
      Result.error(error)
    }
  }
}
```

Keep in mind that **you need to handle all possible errors** that can be returned from a statement, although the compiler has your back here and will show an error if you forgot one.

In contrast to the **do expression** this expression **returns the return value of it's last statement**, this is why every catch expression must return the same type, also as above the compiler will tell you if any of the catch expressions does not match the return value.

