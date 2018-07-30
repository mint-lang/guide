# Inlining JavaScript

Since Mint itself compiles to [JavaScript](https://en.wikipedia.org/wiki/JavaScript), including additional JavaScript is pretty straightforward. Simply wrap the JavaScript in **back-ticks** anywhere you would write an expression. Mint assumes that the type of the value returned by this expressions matches whatever is needed by the surrounding Mint code \(but see [decoding](decoding-objects.md) for a way to safely convert it\).

{% hint style="danger" %}
Inlining allows you to invoke arbitrary JavaScript code. This can cause unexpected runtime errors. You can bypass the Mint type system, storing invalid data in Mint variables and cause Mint itself to be the source of the runtime error. Use it with care!
{% endhint %}

Here is an example inlining a call to the JavaScript function [Window.alert](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert):

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

## Inlined JavaScript Statements

Since Mint is an expression based language, the inlined JavaScript code must also be an expression. If you need to execute multiple JavaScript statements, wrap the code in a [self executing anonymous function](http://markdalgleish.com/2011/03/self-executing-anonymous-functions/):

```text
module Greeter {
  fun greet (name : String) : String {
    `
    (() => {
      Math.SquareCircle( 1.0);
      Math.TrisectAngle( Math.Pi / 4)
      return "Hello " + name + "!"
    })()
    `
  }
}
```

Your code need not return a value if you know that Mint does not expect one in that context \(such as at the end of a `do` expression or a function of type `Void`\).

{% hint style="warning" %}
You should expect your code to be used in a `return` statement.
{% endhint %}

