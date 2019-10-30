# Styling with CSS

After you have something on the screen you probably want to add some styles to it. This is easy to do in Mint, you can even do it with simple CSS!

In components, styles can be defined with an identifier, then applied to HTML using the identifier as a CSS class. A style can contain any number of CSS definitions, sub rules, media queries, `if` and `case` statements.

{% hint style="info" %}
A style is scoped to the component it's defined in.
{% endhint %}

This is how it looks when we style the component what we just created:

```text
component Main {
  style button {
    background: red;
    color: white;
    border: 0;
  }

  fun render : Html {
    <button::button>
      "Click ME!"
    </button>
  }
}
```

The button is now red with white text.

