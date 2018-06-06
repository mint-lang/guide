# Inlining JavaScript

{% hint style="danger" %}
Inlining JavaScript code can be dangerous, in essence you are circumventing the type system, also it can introduce runtime errors! Use it with care!
{% endhint %}

Since Mint compiles to [JavaScript](https://en.wikipedia.org/wiki/JavaScript) using it inside the language is pretty straightforward.

## Usage

By wrapping JavaScript code in **back-ticks** ```alert('Hello')``` will inline it into the compiled JavaScript output. This kind of inlining can be done any place you would write an **expression.**

Here is an example of calling [Window.alert](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert) when a button is clicked:

```text
component Main {
  fun handleClick (event : Html.Event) : Void {
    `alert("Hello")`
  }
  
  fun render : Html {
    <div onClick={handleClick}>
      <{ "Click to alert!" }>
    </div>
  }
}
```

## Expressions

Since Mint is an expression based language the inlined code must always return a value. If you need to use multiple statements, wrapping the code in a [self executing anonymous function](http://markdalgleish.com/2011/03/self-executing-anonymous-functions/) will enable you to do that:

```text
module Greeter {
  fun greet (name : String) : String {
    `
    (()=> 
      let returnValue = "Hello " + name + "!"
      return returnValue
    )()
    `
  }
}
```

{% hint style="warning" %}
You can always expect the code you write will be use in a `return` statement.
{% endhint %}

## Type Checking

Since we cannot type check the result of the inlined JavaScript code,  the type of the inlined code is always matches the which is matched against.

