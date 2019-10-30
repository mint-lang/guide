# Referencing elements and components

Sometimes it's necessary to access elements or components in a component for a number of reasons. To do that you can use the `as name` notation.

The usual example is to focus an element after an event happens:

```text
component Main {
  fun handleClick : Promise(Never, Void) {
    case (input) {
      Maybe::Just element => Dom.focusWhenVisible(element)
      Maybe::Nothing => next {}
    }
  }
  
  fun render : Html {
    <div>
      <input as input/>

      <button onClick={handleClick}>
        "Focus the input!"
      </button>
    </div>
  }
}
```

As you can see the `input` variable will be a `Maybe(Dom.Element)` and this is because there is no guarantee that the element will be in the DOM at the time the function runs. 

This works with components as well:

```text
component Item {
  state text : String = "Hello"

  fun update(text : String) : Promise(Never, Void) {
    next { text = text }
  }

  fun render : Html {
    <div>
      <{ text }>
    </div>
  }  
}

component Main {
  fun handleClick : Promise(Never, Void) {
    case (item) {
      Maybe::Just component => component.update("Bello")
      Maybe::Nothing => next {}
    }
  }
  
  fun render : Html {
    <div>
      <Item as item/>

      <button onClick={handleClick}>
        "Click me!"
      </button>
    </div>
  }
}
```

