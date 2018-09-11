# sequence

`sequence` expressions allows you to do things in sequence.

A `sequence` expression is built up from multiple parts:

* expressions or statements that return a `Promise` or a `Result`
* `catch` branches
* an optional `finally` branch

An example of handling loading something with a request:

```text
sequence {
  /* Started to load the users */
  next { loading = true }

  /*
  Make the request and wait for it to complete
  and store in the "response" variable
  */
  response = 
    Http.get('/users.json')
    |> Http.send()

  /* Parse the body of the response as JSON */
  body = 
    Json.parse(response.body)
    |> Maybe.toResult("Json Parse Error")

  /*
  Try to decode the list of users and convert the
  result into a Promise so we can handle it here then
  store it in the "users" variable
  */
  users =
    decode response.body as Array(User)

  /* If everything went well store the users */
  next { users = users }

/* If the request fails handle it here */
} catch Http.Error => error {
  next { error = "Something went wrong loading the request." }

/* If the decoding fails handle it here */
} catch Object.Error => error {
  next { error = Object.Error.toString(error) }

/* Catch everything else */
} catch {
  next { error = "Could not decode the response." }

/*
After everything is handled or finished
it's not loading anymore
*/
} finally {
  next { loading = false }
}
```

Keep in mind that **you need to handle all possible errors** that can be returned from a statement, although the compiler has your back here and will show an error if you forget one.

The return value of a `sequence` expression is always a `Promise(error, result)` :

* If the last statement is a `Promise` then it will be returned as is
* If the last statement is not a Promise then it will return a promise which never fails `Promise(Never, result)` where the `result` is the value of the last statement

A few notable things to keep in mind:

* All of the catches must match the return value of the last statement
* Results and unwrapped into variables
* Promises are `await` -ed and unwrapped into variables



