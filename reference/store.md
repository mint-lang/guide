# Store

Stores are global containers of application specific data. They are defined with the `store` keyword:

```text
store Counter.Store {
  property counter : Number = 0

  fun increment : Void {
    next { state | counter = counter + 1 }
  }

  fun decrement : Void {
    next { state | counter = counter - 1 }
  }
}
```

In the example above, we defined a store for a global counter with a function to increment it and one to decrement it.

Stores are:

- **global** - which means they are accessible from anywhere \(for example: `Counter.Store.counter`\). This also means all accesses update the same, shared data.
- **mutable** - their data can be changed using a `next`` call \(but only inside the store\)
- they can only contain **functions** and **properties**

## State

Stores have a **state** record containing all of their defined properties. The type of this record is the name of the store and its fields are the properties. In the example above, this looks like:

```text
Counter.Store(counter: Number)
```

## Properties

Properties on a store define keys which correspond to specific type of values. They can be accessed by their name or through the **state** record.

## Connecting to components

Stores can be connected to components. To learn more, check out [ components](components/connecting-stores.md).
