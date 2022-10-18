# Primer API

Tagging a release on this repository will generate and release new SDKs. Currently included SDKs:

- JavaScript/TypeScript SDK: https://github.com/fern-api/primer-node

## [tl;dr] How does it work?

1. When you tag a release, Fern generates SDKs based on the Fern API Definition in this repo.
1. Each generated SDK is pushed to its own GitHub repo.
1. Each SDK's repo has GitHub actions that compile the code and publish the package to its respective registry.

## What is in this repository?

This repository contains

- Primer's [Fern API Definition](./fern/primer/definition/)
- Enabled generators ([generators.yml](./fern/primer/generators.yml))

## What is in the API Definition?

The API Definition contains information about what endpoints, types, and errors are used in the API. The definition is broken into smaller files such as [client-session.yml](fern/primer/definition/client-session.yml) and [payments.yml](fern/primer/definition/payments.yml).

In order to make sure that the definition is valid, you can use the Fern CLI.

```bash
npm install -g fern-api
fern check
```

## What are Generators?

A generator reads in your API Definition and outputs files. The generated files are then pushed to a GitHub repo.

The list of enabled generators is in [generators.yml](./fern/primer/generators.yml).

For example, the TypeScript generator creates the TypeScript SDK. Fern pushes the generated files to [primer-node](https://github.com/fern-api/primer-node) and tags a release on that repo. This triggers a GitHub action on the [primer-node](https://github.com/fern-api/primer-node) repo, which compiles and publishes the package to npm.

The generators are invoked by running `fern release`. When you tag a release on this repo, there's a [GitHub action](.github/workflows/ci.yml#L31) that runs `fern release`.

## How do I make changes to the API?

1. Clone this repo
1. Install fern: `npm install -g fern-api`
1. Edit the [API Definition](fern/primer/definition) 
1. You can run `fern check` to check for issues
1. Make a PR to this repo
1. If checks pass, merge the PR in
1. When you're ready to release new versions of your SDKs, just tag a release on this repo
