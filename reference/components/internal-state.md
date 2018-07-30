# Internal State

```text
component Main {
  state greeting : String = "Welcome"

  fun greet : Void {
    next { greeting = newGreeting }
  } where {
    newGreeting =
      if (greeting == "hello") {
        "bye"
      } else {
        "hello"
      }
  }

  fun render : Html {
    <div>
      <{ greeting }>
      <br/>

      <button onClick={(event : Html.Event) : Void => { greet() }}>
        <{ "Switch" }>
      </button>
    </div>
  }
}
```

The `state` keyword is used to attach **private** state variable to a Component. It cannot be passed in from another Component, but is updated with the `next` keyword.

