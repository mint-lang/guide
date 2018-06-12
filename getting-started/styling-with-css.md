# Styling with CSS

After you have something on the screen then you probably want to add some styles to it, in Mint this is easy to do, and you can even do it with simple CSS!

In components styles can be defined with an identifier \(which you can think of as a CSS class\). These styles then can be applied to HTML inside the component, and can contain any number of CSS definitions.

{% hint style="info" %}
All styles are scoped to the component its defined in.
{% endhint %}

This is how it looks like when we style the component what we just created:

```text
component Main {
  style button {
    background: red;
    color: white;
  	border: 0;
  }
  
  fun render : Html {
    <button::button>
      <{ "Click ME!" }>
    </button>
  }
}
```

The button is now a red one with white text.

