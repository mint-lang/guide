# Connecting Stores

Components refer to [stores](../store.md) in order to **use functions and properties from the store**.

The component references a store with the `connect` keyword:

```text
store Counter {
  property count : Number

  fun setCount (count : Number) : Void {
    next { state | count = count }
  }
}

component Main {
  connect Counter exposing { count, setCount }

  fun render : Html {
    <div
      onClick={\event : Html.Event => setCount(count + 1)}
      onContextMenu={\event : Html.Event => setCount(0) }>

      <{ "Count: " + Number.toString(count) }>

    </div>
  }
}
```

When connecting a store, the component must use the `exposing` keyword to list the particular functions or properties it will use.
