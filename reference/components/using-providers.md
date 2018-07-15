# Using Providers

A Provider represents a source of asynchronous events. To subscribe to a Provider, you `use` it and pass it a block that will be called whenever there is an event to process.

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

In the above example we will update `counter` every second using the [Tick Provider](https://github.com/mint-lang/mint-core/blob/master/source/Provider/Tick.mint).

Other available Providers: [AnimationFrame](https://github.com/mint-lang/mint-core/blob/master/source/Provider/AnimationFrame.mint), [Mouse](https://github.com/mint-lang/mint-core/blob/master/source/Provider/Mouse.mint) and [Scroll](https://github.com/mint-lang/mint-core/blob/master/source/Provider/Scroll.mint)
