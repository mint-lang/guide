# Routing

In Mint, routes of an application are defined at the top level with the **routes** block.

Here is an example of an application where you can list users on one route and show a single user on another route:

```text
routes {
  / {
    Application.setPage("index")
  }

  /users/:id (id: Number) {
    do {
      Application.setPage("show")
      Application.loadUser(id)
    }
  }
}
```

Keep in mind the following things:

* Routes are matched in the order they are defined from **top to bottom**
* Routes can only have one routes block per application
* Routes are used to set the state, not to render things

