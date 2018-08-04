# Computed Properties

Computed properties are functions that work like properties, they are defined with the `get`keyword and no arguments.

```text
component Greeter {
  property name : String = ""

  get text : String {
    "Hello " + name + "!"
  }

  fun render : Html {
    <div>
      <{ text }>
    </div>
  }
}
```

