# do

`do` expressions are for:

- **handling asynchronous computations that might fail**, for example when loading something with a request,
- **executing asynchronous expressions sequentially**

A do expression is built up from 3 parts:

- expressions or statements that return a `Promise` or a `Result`
- `catch` expressions
- an optional `finally` expression

An example of handling loading something with a request:

```text
store Users {
  property users : Array(User) = []
  property loading : Bool = true
  property error : String = ""

  fun loadUsers : Array(User) {
    do {
      /* Started to load the users */
      next { state | loading = true }

      /*
      Make the request and wait for it to complete
      and store in the "response" variable
      */
      response = Http.get('/users.json')

      /* Parse the body of the response as JSON */
      body = Json.parse(repsonse.body)

      /*
      Try to decode the list of users and convert the
      Result into a Promise so we can handle it here then
      store it in the "users" variable
      */
      users =
        decode response.body as Array(User)

      /* If everything went well store the users */
      next { state | users = users }

    /* If the request fails handle it here */
    } catch Http.Error => error {
      next { state | error = "Something went wrong loading the request" }

    /* If the decoding fails handle it here */
    } catch Object.Error => error {
      next { state | error = Object.Error.toString(error) }

    /*
    After everything is handled or finished
    it's not loading anymore
    */
    } finally {
      next { state | loading = false }
    }
  }
}
```

Keep in mind that **you need to handle all possible errors** that can be returned from a statement, although the compiler has your back here and will show an error if you forget one.

In contrast to the `try` expression, the value of a `do` expression is **Void.**
