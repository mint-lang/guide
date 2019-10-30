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

The name of the property must start with a lowercase letter and can only contain letters and numbers.

Properties are referenced by **name** within the component \(in **styles, functions, computed properties,** etc.\).

{% hint style="warning" %}
Properties must be fully defined meaning types in it cannot have any type variables.
{% endhint %}

## Passing properties

Property values are passed to the component when it is rendered:

```text
component Main {
  fun render : Html {
    <Test color="blue" size="big"/>
  }
}
```

All properties are type checked, attempting to set an incompatible value will show an error.

There are some examples of passing different things:

```text
component Main {
  fun render : Html {
    <Test 
      color={variable}
      items=[item1, item2]/>
  }
}
```

