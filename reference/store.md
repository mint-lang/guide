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

In the example above we defined a simple store to store the value of a counter globally. It has two functions one to increment the counter and one to decrement it.

Stores are:

* **global** - which means they are accessible from anywhere \(for example: `Counter.Store.counter`\)
* **mutable** - their data can be changed using a next call \(inside the store\)
* they can only contain **functions** and **properties**

## State

Stores have a **state** record containing all of their defined properties. The type of this record is the name of the store and its fields are the properties. In the type of the store for the example above looks like this:

```text
Counter.Store(counter: Number)
```

## Properties

Properties on a store define keys which correspond to specific type of values. They can be accessed by their name or through the **state** record.

## Connecting to components

Stores can be connected to components, to learn more check out the article about it in the[ components section.](components/connecting-stores.md)

