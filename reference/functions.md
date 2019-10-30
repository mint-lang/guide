# Functions

Functions are callable pieces of code which:

* can take 0 or more parameters
* must have only one expression as the body
* can be defined in **components, modules, stores,** and **providers**

A function is defined by the `fun` keyword followed by its **name, arguments** and **return type:**

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
  * contain only letters and numbers
* **the body of the function is always a single expression**
* type annotations are mandatory
* the parentheses for the arguments can be left off if the function does not take any arguments.

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

## Calling a function

You call a function with its name, providing zero or more arguments separated by commas in parentheses.

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

## Functions as arguments

You can define a function which takes a function as an argument. The type of this argument must be defined \(see [below](functions.md#type-of-a-function)\) and must match the type of the actual function passed at runtime. The function can be an **anonymous** or **named** function.

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

## Type of a function

Functions have a specific type signature, like everything else in Mint. The type for the function includes the types of its arguments \(in parenthesis\) and the return value \(last in list\).

For a function like:

```text
  fun greet (name : String) : Html {
    <div>
      <{ "Hello " + name + "!" }>
    </div>
  }
```

the type is:

```text
Function(String, Html)
```

This can be read as:

> A function which takes a `String` and returns `Html`

## Anonymous functions

Anonymous functions look like this:

```text
(event : Number) : Void { handleClick(event) }

(suffix : String, match : Regex.Match) : String { match.match + suffix }

() : Void { 42 }
```

The anonymous function starts with one or more argument definitions enclosed by parentheses followed by the type definition after a colon `:` , then a single expression that determines the return value enclosed by brackets.

This can be used as an expression anywhere you would use a value:

```text
component Greeter {
  fun render : Html {
    <div onClick={(event : Html.Event) : Void { Debug.log("Hello") }}>
      "Click Me!" 
    </div>
  }
}
```

## Partial Application

Functions can be[ partially applied](https://en.wikipedia.org/wiki/Partial_application) which means that if you call a function with less arguments than the number of arguments defined, it will not call the function but return an other function with takes the arguments that were left out:

```text
fun concat(head : String, tail : String) : String {
  head + " " + tail
}

try {
  partialFunction = 
    concat("Head") /* Function(String) */

  partialFunction("Tail") /* Head Tail */
}
```

## Recursive Functions

All functions can be called recursively:

```text
component Main {
  fun fibonacci(num : Number) : Number {
    if (num <= 1) {
      1
    } else {
      fibonacci(num - 1) + fibonacci(num - 2)
    }
  }

  fun render : Html {
    <div>
      <{ fibonacci(10) }>
    </div>
  }
}
```

{% hint style="danger" %}
Be careful when using recursive functions, the type-checker does not check if there is an exit condition, if there is not it will cause an infinite loop.
{% endhint %}

