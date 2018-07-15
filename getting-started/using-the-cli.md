# Using the CLI

Once you install Mint you will have a `mint` binary at your disposal.

This is the help section \(you can print this using the `--help` flag\):

```text
mint --help
Mint - Help
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Usage:
  mint [flags...] <COMMAND> [arg...]

Mint

Flags:
  --help   # Displays help for the current command.

Arguments:
  COMMAND  # The sub command to run.

Subcommands:
  build    # Builds the project for production
  init     # Initializes a new project
  install  # Installs dependencies
  loc      # Counts Lines of Code
  start    # Starts the development server.
  test     # Runs the tests.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
All done in 197μs!
```

## Initializing a new application

To initialize a new application, you invoke the binary with the `init` command:

```text
mint init my-app
```

This will scaffold a new application in the `my-app` directory:

```text
my-app
├── source
│   └── Main.mint
└── mint.json
```

## Installing dependencies

You install dependencies by invoking the binary with the `install` command:

```text
mint install
```

This builds a dependency tree of the packages and installs them by cloning their repositories from Git sources into the `.mint` directory.

## Starting a development server

To start a development server for an application, just invoke the binary with the `start` command:

```text
mint start
```

## Running tests

To run the test written for an application, just invoke the binary with the `test` command:

```text
mint test
```

This will:

- compile the application including the tests
- open a browser in headless mode
- run the tests in the browser printing the results along the way

## Building for production

To build the application for production deployment, invoke the binary with the `build` command:

```text
mint build
```

This will:

- generate the `index.html` file
- compile the application in production mode
- if a base icon is provided, generate favicons in different sizes
- copy all static files from the `public` directory
