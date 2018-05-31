# Functions

Functions are callable pieces of code which:

* can be defined for **components, modules, stores,** and **providers**
* must have only one expression as the body
* can take 0 or more parameters

A function is defined by the `fun` keyword followed by it's **name, arguments** and **type:**

```text
module Greeter {
  fun greet (name : String) : Html {
    <div>
      <{ "Hello " + name + "!" }>
    </div>
  }
}
```

Things to keep in mind:

* the name of the function must:
  * start with a lowercase letter
  * only contain letters and numbers
* **the body of the function is always a single expression**
* type annotations are mandatory
* the parentheses for the arguments can be left out if the function does not take any

## Type of a function

Functions have a specific type signature, for the example above it looks like this:

```text
Function(String, Html)
```

The `Function` type represents a function, the type parameters \(in the parenthesis\) are the types of the functions arguments, in this case the `String` is the type of the `name` parameter, while the `Html` is the type of the return value.

This type can be read as: 

> A function which takes a `String` and returns `Html`

## Calling a function

You can call a function \(which is in scope\) with it's name, followed by the parenthesized arguments separated by commas.

```text
module Greeter {
  fun greet (name : String) : Html {
    <div>
      <{ "Hello " + name + "!" }>
    </div>
  }

  fun main : Html {
    greet("Bob") 
  }
}
```

If the function belongs to a **store** or a **module** you can call it like this:

```text
module Greeter {
  fun greet (name : String) : Html {
    <div>
      <{ "Hello " + name + "!" }>
    </div>
  }
}

component Main {
  fun render : Html {
    Greeter.greet("Bob") 
  }
}
```

## Passing a function

There are functions that take other functions as **arguments**, for which we can either pass **anonymous functions** or we can pass **already defined functions:**

```text
module Greeter {
  fun greet (name : String) : Html {
    <div>
      <{ "Hello " + name + "!" }>
    </div>
  }
}

component Main {
  fun renderGreeting (name : String, greeter : Function(String, Html)) : Html {
    greeter(name)
  }

  fun render : Html {
    renderGreeting("Bob", Greeter.greet) 
  }
}
```

Here we passed the `Greeter.greet` function as an argument.

## Where block

You can assign variables for use in the function body in a where block:

```text
fun greet (id : String, users : Array(User)) : String {
  "Hello " + user.name + "!"
} where {
  user = 
    getUserFromId(id, users)
}
```

## Anonymous functions

Anonymous functions look like this:

```text
\event : Number => handleClick(event)
```

They can be used as an expression anywhere you would use a value otherwise:

```text
component Greeter {
  fun render : Html {
    <div onClick={\event : Html.Event => do { Debug.log("Hello") }}>
      <{ "Click Me!" }>
    </div>
  }
}
```



