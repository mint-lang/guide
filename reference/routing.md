# Routing

In Mint routes of an application are defined at the top level with the **routes** block.

An example of an application where use can list users on one and show a single user on an other route:

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

* Routes are matched in order they are defined from **top to bottom**
* Can only have one routes block per application
* Routes are used to set the state, not to render things

