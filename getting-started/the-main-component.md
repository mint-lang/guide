# The Main Component

To display anything on the screen you need to define the `Main` component. Anything it returns from its `render` function will be shown.

Here we render a button on the screen:

```text
component Main {
  fun render : Html {
    <button>
      "Click ME!"
    </button>
  }
}
```

