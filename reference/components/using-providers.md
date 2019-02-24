# Using Providers

A Provider represents a source of asynchronous events. To subscribe to a Provider, you `use` it and pass it a block that will be called whenever there is an event to process.

```text
component Main {
  state counter : Number = 0

  use Provider.Tick { 
    ticks = () : Promise(Never, Void) {
      next { counter = counter + 1 } 
    }
  }

  fun render : Html {
    <div>
      <{ Number.toString(counter) }>
    </div>
  }
}
```

In the above example we will update `counter` every second using the [Tick Provider](https://github.com/mint-lang/mint/blob/master/core/source/Provider/Tick.mint).

Other available Providers: [AnimationFrame](https://github.com/mint-lang/mint-core/blob/master/source/Provider/AnimationFrame.mint), [Mouse](https://github.com/mint-lang/mint/blob/master/core/source/Provider/Mouse.mint) and [Scroll](https://github.com/mint-lang/mint-core/blob/master/source/Provider/Scroll.mint)

