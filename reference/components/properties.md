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

Properties are referenced by name within the component \(in **styles, functions, getters,** etc.\).

## Passing properties

Property values are passed to the component when it is rendered:

```text
component Main {
  fun render : Html {
    <Test color="blue" size="big"/>
  }
}
```

Things to remember:

* The name of the property must:
  * start with a lowercase letter
  * contain only letters and numbers
* All properties are type checked, attempting to set an incompatible value will show an error.

