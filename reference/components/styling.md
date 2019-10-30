# Styling

Mint includes CSS support for styling HTML elements.

Within a component, you define styles with a **style block** named with an identifier:

```text
component Test {
  style base {
    font-family: sans;
    font-weight: bold;
    color: red;
  }

  fun render : Html {
    <div::base>
      Hello
    </div>
  }
}
```

Then you apply the styles to an HTML element by specifying it after the tag of the element `<div::style/>` .

You can have CSS definitions, sub rules, media queries, `if` and `case` expressions inside a `style` block.

You can even apply multiple styles to an HTML element:

```text
component Main {
  style a {
    color: red;
  }

  style b {
    background: blue;
  }

  fun render : Html {
    <div::a::b/> 
  }
}
```

## Interpolation

Expressions can be interpolated in the value of a property using the interpolation syntax `#{...}`:

```text
component Test {
  style base {
    color: #{color};
  }

  get color : String {
    "red"
  }

  fun render : Html {
    <div::base>
      Hello
    </div>
  }
}
```

Here the color of the text evaluates to `"red"`.

## Arguments

A style block can take many arguments just like a function:

```text
component Main {
  style base(color : String) {
    color: #{color};
  }

  fun render : Html {
    <div> 
      <div::base("red")>
        "I am red!"
      </div>

      <div::base("blue")>
        "I am blue!"
      </div>
    </div>
  }
}
```

## Sub rules

Additional rules that match the element can be defined in the same block:

```text
component Test {
  style base {
    color: cyan;
    
    /* The ampersand character references the rule it resids in. */
    &:focus {
      color: red;
    }

    /* This is a sub rule which uses the descendant selector. */
    a {
      color: blue;
    }
  }

  fun render : Html {
    <div::base tabindex="0">
      <{ "Hello " }>
      <a>
        <{ "world" }>
      </a>
    </div>
  }
}
```

This is useful for styling **pseudo elements and states** or style child elements.

## Media queries

[Media queries](https://www.w3.org/TR/css3-mediaqueries/) can be defined for a style or sub rule. When matched, their contents apply to all elements that match them.

```text
component Test {
  style base {
    color: red;

    @media (min-width: 600px) {
      color: blue;
    }
  }
  fun render : Html {
    <div::base>
      <{ "Hello " }>  
    </div>
  }
}
```

## Nesting 

Sub rules and media queries can be nested in each other infinitely:

```text
style base {
  color: red;
  
  div {
    color: blue;
    
    span {
      color: yellow;
      
      @media (max-width: 500px) {
        font-weight: bold;
      }
    }
  }
}
```

## If and Case

A special version of `if` and `case` expressions can be used inside `style` blocks:

```text
style base {
  if (loading) {
    pointer-events: none;
    opacity: 0.5;
  } 

  case (status) {
    Status::Ok => color: blue;
    Status::Err => 
      border: 1px solid red;
      color: red;
  }
}
```

In this case the some different rules: 

* one expression rule does not apply
* you can have one or more CSS definitions in each branch
* the `else` and empty case branch can be omitted

## Inline Styles

You can use inline styles just like in HTML in two different ways:

```text
component Main {
  fun render : Html {
    <div>
      /* As a String */
      <div style="color: red;">
        "I am red!"
      </div>

      /* As a Map(String, String) */
      try {
        style = 
          Map.empty()
          |> Map.set("color", "red")

        <div style={style}>
          "I am red!"
        </div>
      }
    </div> 
  }
}
```

## Behind the scenes

The compiler separates properties that have interpolations from the ones that don't. The properties with interpolations are converted to use CSS variables \(`--test-base-color` \).

During compiling the dynamic properties are converted to use a `style` object that contains the appropriate variables with their expressions.

The defined styles are static and added to the `head` of the document at runtime.

