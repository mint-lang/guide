# Internal State

```text
record Greetings {
  greeting : String
}

component Main {
  state : Greetings { greeting = "Welcome" }

  fun greet : Void {
    next { greeting = newGreeting }
  } where {
    newGreeting =
      if (state.greeting == "hello") {
        "bye"
      } else {
        "hello"
      }
  }

  fun render : Html {
    <div>
      <{ state.greeting }>
      <br/>

      <button onClick={\e : Html.Event => greet()}>
        <{ "Switch" }>
      </button>
    </div>
  }
}
```

The `state` keyword can be used to attach private state to a Component. This means unlike a property, it can't be passed in from another Component. We're using the `next` keyword to set a new state, just like we would for a property.

