# Store

Stores are global containers of application specific data. They are defined with the `store` keyword:

```text
store Counter.Store {
  state counter : Number = 0

  fun increment : Promise(Never, Void) {
    next { counter = counter + 1 }
  }

  fun decrement : Promise(Never, Void) {
    next { counter = counter - 1 }
  }
}
```

In the example above, we defined a store for a global counter with a function to increment it and one to decrement it.

Stores are:

* **global** - which means they are accessible from anywhere \(for example: `Counter.Store.counter`\). This also means all accesses update the same, shared data.
* **mutable** - their data can be changed using a `next` call \(but only inside the store\)
* they can only contain **functions** and **properties**

## States

States on a store define keys which correspond to specific type of values. They can be accessed by their name.

## Connecting to components

Stores can be connected to components. To learn more, check out [ components](components/connecting-stores.md).

