# Configuration

Your application / package is configured with the `mint.json` file \(which is a [JSON](https://en.wikipedia.org/wiki/JSON) file\).

The initial `mint.json` file of an application looks like this:

```text
{
  "name": "my-app",
  "source-directories": [
    "source"
  ],
  "dependencies": {
    "mint-core": {
      "repository": "https://github.com/mint-lang/mint-core",
      "constraint": "0.0.0 <= v < 1.0.0"
    }
  }
}
```

{% hint style="info" %}
All the fields are validated so if something is not right you will get a nice error message!
{% endhint %}

Here are all the possible fields \(dot notation denotes a nested object\):

| Path               | Purpose                                                                                                               |
| ------------------ | --------------------------------------------------------------------------------------------------------------------- |
|                    |                                                                                                                       |  |  |  |  |  |  |
| name               | The name of your application or package.                                                                              |
| source-directories | The directories which contains source files of your application.                                                      |
| test-directories   | The directories which contains tests for your application.                                                            |
| dependencies       | Contains the dependencies.                                                                                            |
| application        | Contains application specific information \(can be omitted in packages\)                                              |
| application.head   | A path to an HTML file which can contain links to external resources.                                                 |
| application.title  | The initial title of the application.                                                                                 |
| application.meta   | An object which contains informations which is converted to META tags.                                                |
| application.icon   | A path to an image file which is converted to different icons like [favicons](https://en.wikipedia.org/wiki/Favicon). |

## Dependencies

The dependencies object contains all the packages that your application needs. Each key is the name of a package and the value is an object that has a `repository` field pointing to Git repository and `constraint` field that is the version information in one of two formats:

* `0.0.0 <= v < 1.0.0` where the `v` is the resolvable version
* `master:1.0.0` where the first part is the Git reference \(of a branch, commit hash or tag\) followed by a colon and the version the package should resolve as this is necessary because the version is only specified by tags.
