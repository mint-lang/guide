# do

`do` expressions are for two things:

* **handling asynchronous computations that might fail**, for example when loading something with a request,
* **executing asynchronous expressions sequentially**

A do expression is built up from 3 parts:

* expressions or statements that returns a `Promise` or a `Result`
* catch expressions
* an optional finally expression

An example of handling loading something with a request:

```text
store Users {
  property users : Array(User) = []
  property loading : Bool = true
  property error : String = ""

  fun loadUsers : Array(User) {
    do {
      # Started to load the users
      next { state | loading = true }

      # Make the request and wait for it to complete 
      # and store in the "response" variable
      response = 
        Http.get('/users.json')

      # Try to decode the list of users and convert the
      # Result into a Promise so we can handle it here then
      # store it in the "users" variable
      users = 
        response.body
        |> Json.decode()
        |> Json.Decoder.decodeArray(decodeUser)

      # If everything went well store the users
      next { state | users = users }

    # If the request fails handle it here
    } catch Http.Error => error {
      next { state | error = error.message }

    # If the decoding fails handle it here
    } catch Json.Error => error {
      next { state | error = error.message }

    # After everything is handled or finished
    # it's not loading anymore
    } finally {
      next { state | loading = false }
    }
  }
}
```

Keep in mind that **you need to handle all possible errors** that can be returned from a statement, although the compiler has your back here and will show an error if you forgot one.

In contrast to the **try expression** a do expression **always returns Void.**

