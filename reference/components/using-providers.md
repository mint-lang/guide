# Using Providers

```text
record Ticks {
  counter : Number
}

component Main {
  state : Ticks { counter = 0 }

  use Provider.Tick { ticks = \ => next { state | counter = state.counter + 1 } }

  fun render : Html {
    <div>
      <{ Number.toString(state.counter) }>
    </div>
  }
}
```

To subscribe to a Provider, you  `use` it and pass a block that will be called whenever there is an update from the [Tick Provider](https://github.com/mint-lang/mint-core/blob/master/source/Provider/Tick.mint). In the above example we will receive a call every second without argument.

