# Using Providers

```text
record Ticks {
  counter : Number
}

component TickCounter {
  state : Ticks { counter = 0 }

  use Provider.Tick { ticks = \ => next { state | counter = state.counter + 1 } }

  fun render : Html {
    <div>
      <{ Number.toString(state.counter) }>
    </div>
  }
}
```

