# parallel

`parallel` expressions allows you to do things in parallel, and then do things with their results.

A `parallel` expression is built up from multiple parts:

* expressions or statements that return a `Promise` or a `Result`
* an optional `then` branch
* `catch` branches
* an optional `finally` branch

An example:

```text
parallel {
  articles = 
    loadImages()
  
  users =
    loadUsers() 
} then {
  next { 
    articles = articles,
    users = users,
  }
} catch {
 /* errors are catached here. */
} finally {
  /* Clean things up here. */
}
```

Keep in mind that **you need to handle all possible errors** that can be returned from a statement, although the compiler has your back here and will show an error if you forget one.

The return value of a `parallel` expression is always a `Promise(error, result)` :

* If the value of the `then` branch is a `Promise` then it will be returned as is
* If the value of the `then` branch is not a Promise then it will return a promise which never fails `Promise(Never, result)` where the `result` is the value of the `then` branch
* If there is no `then` branch then the return value is `Promise(Never, Void)`

A few notable things to keep in mind:

* All of the catches must match the return value of the last statement
* Results and unwrapped into variables
* Promises are `await` -ed and unwrapped into variables

