# Connecting Stores

Components refer to [stores](../store.md) in order to **use functions and properties from the store**.

The component references a store with the `connect` keyword:

```text
store Counter {
  state count : Number = 0

  fun setCount (count : Number) : Promise(Never, Void) {
    next { count = count }
  }
}

component Main {
  connect Counter exposing { count, setCount }

  fun render : Html {
    <div
      onClick={(event : Html.Event) : Void { setCount(count + 1) }}
      onContextMenu={(event : Html.Event) : Void { setCount(0) }}>

      <{ "Count: " + Number.toString(count) }>

    </div>
  }
}
```

When connecting a store, the component must use the `exposing` keyword to list the particular functions or properties it will use.

#### Exposing with a different name

You can expose a connected function or property by a different name using the `as` notation:

```text
connect Counter exposing { count as myCount }
```

