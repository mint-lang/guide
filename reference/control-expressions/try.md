# try

`try` is a control expression for **handling synchronous computations that might fail**.

A try expression has 3 parts:

- statements that returns a `Result`
- catch expressions
- a return expression

Let's see an example where we are using this expression to decode an object:

```text
record User {
  email : String,
  name : String
}

module Example {
  fun decodeUser (object : Object) : Result(Object.Error, User) {
    try {
      /*
      Try to decode the email from the object,
      if succeeds the value is assigned to the
      "email" variable.
      */
      email =
        object
        |> Object.Decode.field("email", Object.Decode.string)

      /*
      Same for the name.
      */
      name =
        object
        |> Object.Decode.field("name", Object.Decode.string)

      /*
      At this point we have the fields so we can return
      a result with the user.  
      */
      Result.ok({
        email = email
        name = name
      })

    /*
    If any of the decoders fail we handle it here and
    return an result with the error.
    */
    } catch Object.Error => error {
      Result.error(error)
    }
  }
}
```

Keep in mind that **you need to handle all possible errors** that can be returned from a statement, although the compiler has your back here and will show an error if you forgot one.

In contrast to the `do` expressions, the value of a `try` expression is the value of **its last expression**. So every `catch` expression must also return the same type.
