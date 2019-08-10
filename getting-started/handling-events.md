# Handling Events

In web applications there are a lot of interactive parts, and all of these parts are handling some input from the users. Inputs can come from a variety of sources such as keyboard, and mouse. An instance of these inputs is called an **event**.

You can handle events coming from the DOM using **event attributes**. An event attribute is always starts with `on` followed by the name of the event \(capitalized\), for example: `onClick` or `onInput`.

In this example we are listening on a click event:

```text
component Main {
  fun render : Html {
    <button onClick={(event : Html.Event) : String { Debug.log("Hello") } }>
      "Click Me!"
    </button>
  }
}
```

Every time the users clicks on this button the `"Hello"` string is printed in the console.

Event attributes should match a specific type signature `Function(Html.Event, a)` which means that only functions which take an `Html.Event` and return something can be passed to these attributes. Alternatively you can just pass a `Function(a)` if you don't care about the event.

### Html.Event

An Html.Event is a [record](../reference/records.md) with the following fields:

| Name | Type |
| :--- | :--- |
| **bubbles** | Bool |
| **cancelable** | Bool |
| **currentTarget** | Dom.Element |
| **defaultPrevented** | Bool |
| **eventPhase** | Number |
| **isTrusted** | Bool |
| **target** | Dom.Element |
| **timeStamp** | Number |
| **type** | String |
| **data** | String |
| **altKey** | Bool |
| **charCode** | Number |
| **ctrlKey** | Bool |
| **key** | String |
| **keyCode** | Number |
| **locale** | String |
| **location** | Number |
| **metaKey** | Bool |
| **repeat** | Bool |
| **shiftKey** | Bool |
| **which** | Number |
| **button** | Number |
| **buttons** | Number |
| **clientX** | Number |
| **clientY** | Number |
| **pageX** | Number |
| **pageY** | Number |
| **screenX** | Number |
| **screenY** | Number |
| **detail** | Number |
| **deltaMode** | Number |
| **deltaX** | Number |
| **deltaY** | Number |
| **deltaZ** | Number |
| **animationFrame** | String |
| **pseudoElement** | String |
| **propertyName** | String |
| **elapsedTime** | Number |

