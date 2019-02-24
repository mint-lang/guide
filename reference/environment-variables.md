# Environment Variables

When building web applications usually the same application needs to working in different environments \(development, staging, production\). There are some [variables](https://en.wikipedia.org/wiki/Environment_variable) like API endpoints that are different between these environments.

Mint offers a simple feature for managing these variables. You can create different files `.env` `.env.production` which have contents like this:

```text
ENDPOINT=http://localhost:3001
WSENDPOINT=ws://localhost:3001
```

Then in Mint code you can inline them:

```text
component Main {
  fun render : Html {
    <div>  
      <{ @ENDPOINT }>
    </div>
  }
}
```

### Specifying .env file

[The Mint CLI](../getting-started/using-the-cli.md) has a global flab `-e` or `--env` which takes the path to the `.env` file:

```text
mint start --env .env.production
```

