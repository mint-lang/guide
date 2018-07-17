# Connecting Stores

Components can be connected to [stores](../store.md) in order to **use functions and properties from them**.

Connecting a store is easy with the `connect` keyword:

```text
store Counter {
  property count : Number = 0

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

When connecting a store you must explicitly defined which functions or properties you wan to expose from the store, you can do that with the `exposing` keyword after the stores name.

