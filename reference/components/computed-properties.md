# Computed Properties

Computed properties are like functions that work like properties, they can be defined with the `get`keyword. 

```text
component Greeter {
  property name : String = ""
  
  get text : Html {
    "Hello " + name + "!"
  }
  
  fun render : Html {
    <div>
      <{ text }>
    </div>
  }
}
```



