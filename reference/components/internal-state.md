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

The `state :` keyword is used to attach **private** state to a Component. It cannot be passed in from another Component, but is updated with the `next` keyword, just like we would for a property.
