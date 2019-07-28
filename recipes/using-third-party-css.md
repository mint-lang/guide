# Using third party CSS

There is this frequently asked question:

> How can I use it with a CSS library like bootstrap with Mint?

So in this page I will guide you through it.

### Adding the library

In this example we will be adding [Bootstrap](https://getbootstrap.com) to a Mint application.

First you need to create an HTML file which will be loaded in the `head` of the compiled HTML, for now it will only contain the link to the stylesheet from the CDN:

{% code-tabs %}
{% code-tabs-item title="assets/head.html" %}
```markup
<link rel="stylesheet" 
  href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" 
  integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" 
  crossorigin="anonymous">
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Next you will need to modify the `mint.json` file so the file we just created:

{% code-tabs %}
{% code-tabs-item title="mint.json" %}
```javascript
{
  "name": "mint-bootstrap-example",
  "source-directories": [
    "source"
  ],
  "application": {
    "head": "assets/head.html"
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If you start the development server and load the application the CSS for Bootstrap will be loaded.

### Using the library

Now you can use the library as you normally would, by adding the `class` attribute on HTML elements:

{% code-tabs %}
{% code-tabs-item title="source/Main.mint" %}
```text
component Main {
  style base {
    background: #f5f5f5;
    text-align: center;
    height: 100vh;

    justify-content: center;
    align-items: center;
    display: flex;
  }

  fun render : Html {
    <div::base>
      <form class="form-signin">
        <img
          src="https://getbootstrap.com/docs/4.3/assets/brand/bootstrap-solid.svg"
          class="mb-4"
          height="72"
          width="72"
          alt=""/>

        <h1 class="h3 mb-3 font-weight-normal">
          "Please sign in"
        </h1>

        <label
          for="inputEmail"
          class="sr-only">

          "Email address"

        </label>

        <input
          placeholder="Email address"
          class="form-control mb-3"
          id="inputEmail"
          type="email"
          autofocus=""
          required=""/>

        <label
          for="inputPassword"
          class="sr-only">

          "Password"

        </label>

        <input
          class="form-control mb-3"
          placeholder="Password"
          id="inputPassword"
          type="password"
          required=""/>

        <div class="checkbox mb-3">
          <label>
            <input
              value="remember-me"
              type="checkbox"/>

            " Remember me"
          </label>
        </div>

        <button
          class="btn btn-lg btn-primary btn-block"
          type="submit">

          "Sign in"

        </button>

        <p class="mt-5 mb-3 text-muted">
          "© 2017-2019"
        </p>
      </form>
    </div>
  }
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

