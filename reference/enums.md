# Enums

In Mint **enums** represents [Algebraic Data Types](https://en.wikipedia.org/wiki/Algebraic_data_type). 

With **enums** it's possible to describe data which contains **different type of values** \(called variants\). For example a type for a logged in state can be written as two variants:

```text
enum UserState {
  LoggedIn(User)
  Visitor
}
```

since this is a type it can be used in type signatures:

```text
fun isLoggedIn (userState : UserState) : Bool {
  case (userState) {
    UserState::LoggedIn user => true
    UserState::Visitor => false
  }
}

isLoggedIn(UserState::LoggedIn(user)) /* true */
isLoggedIn(UserState::Visitor) /* false */
```

as you can see from the code above you can create instances of the type by using it's name then a double colon then it's variant and then any arguments it takes `UserState::LoggedIn(user)` also you can match the variants in a [case expression](control-expressions/case.md).

## Type variables

You can define **type variables** for an **enum** so it can become generic meaning that a type of a value of a variant can be any other type.

The best example for this is the `Result(error, value)` type:

```text
enum Result(error, value) {
  Err(error)
  Ok(value)
}
```

which can be used with any types for error and value:

```text
/* A result where the error and value is both string */
Result(String, String) 

/* An example result type for HTTP requests. */
Result(Http.ErrorResponse, Response)
```

