# Properties

Properties can be defined for components with the **property** keyword:

```text
component Test {
  property size : String = "small"
  property color : String = "red"

  fun render : Html {
    <div>
      <{ color }>
      <{ size }>
    </div>
  }
}
```

Properties can be accessed by their name inside the component \(in **styles, functions, getters,** etc.\).

## Passing properties

Properties are passed to the components when they are rendered:

```text
component Main {
  fun render : Html {
    <Test color="blue" size="big"/>
  }
}
```

Things to remember:

* the name of the property must:
  * start with a lowercase letter
  * only contain letters and numbers
* all properties are type checked, giving not matching values will show an error

