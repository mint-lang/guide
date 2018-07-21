# Built in Types

Mint comes with several built in types. These are used in control expressions: `Promise`, `Result`, `Void`, `Never`. The `Maybe` type represents a [nillable](https://stackoverflow.com/questions/5913200/why-is-it-called-nillable) value.

## Promise

The promise type represents a [JavaScript promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), an asynchronous computational task that might fail.

In Mint promises have two parameters `Promise(error, result)` :

- **error** - the value if the task failed
- **result** - the value if the task succeeded

A good example is a HTTP request which in Mint looks like this:

`Promise(Http.ErrorResponse, Http.Response)`

where the `Http.ErrorResponse` is a record containing information about the error that happened while `Http.Response` is a record containing the response of the request.

Promises are used in a [do expression](control-expressions/do.md)

## Result

The result type, represents a **synchronous** task that might fail.

In Mint, results have two parameters `Result(error, value)`:

- **error** - the type of the error
- **value** - the type of the result

For example, converting a `String` to a `Number`:

- If the conversion fails we get an error:

  ```text
  "blah"
  |> Number.fromString()
  |> Result.isError() # true
  ```

- If the conversion succeeds we get a value

  ```text
  "10"
  |> Number.fromString()
  |> Result.isOk() # true
  ```

Results are used in [do](control-expressions/do.md) **and** [try](control-expressions/try.md) expressions.

## Void

The void type represents a side-effect: an expression which cannot have a value, either because it's not synchronous or because it causes a state change.

- `Void` is used to handle events coming from the DOM or any outside source.
- `Void` can be explicitly returned with the `void` keyword.

## Never

The never type is used to describe tasks \(promises or results\) that can never fail. For example, here is the type of task that can never fail: `SomeTask(Never, Value)`

These tasks don't need to be caught in `do` and `try` expressions.

## Maybe

The maybe type represents a value which may or may not exist.

For example here is a user who may or may not have a car:

```text
record Car {
  type : String,
  engine : String
}

record User {
  name : String,
  car : Maybe(Car)
}
```
