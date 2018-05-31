# Built in Types

There are some built in types of the language which are used in control expressions: `Promise`, `Result`, `Void` and `Never`, also there is `Maybe`

## Promise

The promise type represents a [JavaScript promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) \(an asynchronous computational task that might fail\).

In Mint promises have two parameters `Promise(error, result)` :

* **error** - the type of the error
* **result** - the type of the result

A good example is a HTTP request which in Mint looks like this:

`Promise(Http.ErrorResponse, Http.Response)`

where the `Http.ErrorResponse` is a record containing information about the error that happened while `Http.Response` is a record containing the response of the request.

Promises are used in a [**do expressions.**](untitled-1/do.md)

## Result

The result type \(similarly to the promise type\) represents a **synchronous** task that might fail.

In Mint results have two parameters `Result(error, value)`:

* **error** - the type of the error
* **value** - the type of the result

A good example is converting a `String` to a `Number`:

* If the conversion fails we get an error:

  ```text
  "blah"
  |> Number.fromString() 
  |> Result.isError() # true
  ```

* If the conversion succeeds we get a value

  ```text
  "10"
  |> Number.fromString()
  |> Result.isOk() # true
  ```

Results are used in [**do**](untitled-1/do.md) **and** [**try expressions**](untitled-1/try.md)**.**

## Void

The void type represents a side-effect: an expression which cannot have a value, either because it's not synchronous or because it causes a state change.

* `Void` is used to handle events coming from the DOM or any outside source.
* `Void` can be explicitly returned with the `void` keyword.

## Never

The never type is used to describe tasks \(promises or results\) that can never fail. For example here is the type of task that can never fail: `SomeTask(Never, Value)`

These tasks don't need to be caught in do and try expressions.

## Maybe

The maybe type represents a value which may or may not exists. 

For example there is a user which may or may not have a car:

```text
record Car {
  type : String,
  engine : String
}

record User {
  name : String,
  card : Maybe(Car)
}
```

