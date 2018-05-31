# Records

Records are object like data structures, that have a fix set of keys and values.

You can define a **record type** with the `record` keyword:

```text
record User {
  email : String,
  name : String,
  id : Number
}
```

{% hint style="warning" %}
Record definitions are unique, so defining a record with a same structure will raise an error.
{% endhint %}

## Nested records

Records can be nested in each other, although **record types can only be one level deep.**

```text
record Position {
  x : Number,
  y : Number
}

record Entity {
  position : Position,
  id : String
}
```

Creating a nested record is straightforward:

```text
entity = 
  {
    position = {
      x = 0,
      y = 0
    },
    id = "0"
  }
```

## Working with records

Records can be created like this:

```text
{ 
  email = "john.doe@gmail.com",
  name = "John Doe", 
  id = 0
}
```

You can create a new record from an existing one by copying all none specified fields like this:

```text
user = 
  { 
    email = "john.doe@gmail.com",
    name = "John Doe", 
    id = 0
  }

updatedUser =   
  { user | name = "Stuart" }

{ 
  email = "john.doe@gmail.com",
  name = "Stuart", 
  id = 0
}
```

{% hint style="warning" %}
Trying to add fields to a record which doesn't have it in it's definition will raise an error.
{% endhint %}

{% hint style="info" %}
**\[PLANNED\]** You can update a nested record with a dot notation.
{% endhint %}

```text
user = 
  {
    name = "Stuart",
    address = {
      location = "Freedonia"
    }
  }
  
{ user | 
  name = "Bob",  
  address.location = "Super Silly Fun Land" 
}
```

[  
](https://gdotdesign.gitbooks.io/mint-old/content/literals.html)

