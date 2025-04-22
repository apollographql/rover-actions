# rover-actions

This repository contains a set of GitHub Actions to use [Rover](https://rover.apollo.dev) in your GitHub Actions workflows.  

## [install-rover-cli](./install-rover-cli/action.yml)

This is a GitHub Action to install the [Apollo Rover CLI](https://rover.apollo.dev/) on action runners. Once installed, `rover` is added to `PATH`, so it can be used in subsequent steps.

### Inputs

| Name | Description | Default |
| ---- | ----------- | ------- |
| `version` | The version of [`rover`](https://rover.apollo.dev/) to install | `latest` |

### Usage

Installing a specific version of `rover`:

```yaml
- uses: apollographql/rover-actions/install-rover-cli@v1
  with:
    version: 0.26.3
```

Install the latest version:

```yaml
- uses: apollographql/rover-actions/install-rover-cli@v1
```

Run a manual rover command after install:

```yaml
- uses: apollographql/rover-actions/install-rover-cli@v1
- name: Run manual schema check (instead of included commands)
  env:
    APOLLO_KEY: ${{ secrets.APOLLO_KEY }}
  run: rover subgraph check ${{ vars.APOLLO_GRAPH_REF }} --name subgraph-name --schema ./path/to/schema.graphql
```

## [subgraph-check](./subgraph-check/action.yml)

This is a GitHub Action to perform the [`rover subgraph check`](https://www.apollographql.com/docs/rover/commands/subgraphs#subgraph-check) command.

### Inputs

| Name | Description | Required | Default |
| ---- | ----------- | :------: | :-----: |
| `apollo-key` | Your Apollo Studio API key | * | |
| `graph-ref` | `<NAME>@<VARIANT>` of graph in Apollo Studio | * | |
| `name` | The name of the subgraph | * | |
| `schema` | The schema file to check | * | |
| `background` | Set to `true` if the check should run asynchronously | | `false` |
| `query-count-threshold` | The minimum number of times a query or mutation must have been executed in order to be considered in the check operation | | |
| `query-percentage-threshold` | The minimum percentage of times a query or mutation must have been executed, relative to the request count, for it to be considered in the check (0 <= x <= 100) | | |
| `validation-period` | Size of the time window with which to validate schema against (i.e. `24h` or `1w 2d 5h`) | | |
| `log` | Specify Rover's log level | | `info` |
| `format` | Specify Rover's log format type [`plain`, `json`] | | `plain` |
| `client-timeout` | Configure the timeout length (in seconds) when performing HTTP(S) requests | | `30` |

### Usage

_**Note**: You must first install the Rover CLI_

```yaml
- uses: apollographql/rover-actions/install-rover-cli@v1
- uses: apollographql/rover-actions/subgraph-check@v1
  with:
    apollo-key: ${{ secrets.APOLLO_KEY }}
    graph-ref: ${{ vars.APOLLO_GRAPH_REF }}
    name: subgraph-name
    schema: ./path/to/schema.graphql
```

## [subgraph-lint](./subgraph-lint/action.yml)

This is a GitHub Action to perform the [`rover subgraph lint`](https://www.apollographql.com/docs/rover/commands/subgraphs#subgraph-lint) command.

### Inputs

| Name | Description                                                                                                                                                      | Required | Default |
| ---- |------------------------------------------------------------------------------------------------------------------------------------------------------------------| :------: | :-----: |
| `apollo-key` | Your Apollo Studio API key                                                                                                                                       | * | |
| `graph-ref` | `<NAME>@<VARIANT>` of graph in Apollo Studio                                                                                                                     | * | |
| `name` | The name of the subgraph                                                                                                                                         | * | |
| `schema` | The schema file to check                                                                                                                                         | * | |
| `ignore-existing-lint-violations` | Set to `true` if the check should ignore existing violations                                                                                                     | | `false` |
| `log` | Specify Rover's log level                                                                                                                                        | | `info` |
| `format` | Specify Rover's log format type [`plain`, `json`]                                                                                                                | | `plain` |
| `client-timeout` | Configure the timeout length (in seconds) when performing HTTP(S) requests                                                                                       | | `30` |

### Usage

_**Note**: You must first install the Rover CLI_

```yaml
- uses: apollographql/rover-actions/install-rover-cli@v1
- uses: apollographql/rover-actions/subgraph-lint@v1
  with:
    apollo-key: ${{ secrets.APOLLO_KEY }}
    graph-ref: ${{ vars.APOLLO_GRAPH_REF }}
    name: subgraph-name
    schema: ./path/to/schema.graphql
```

## [subgraph-publish](./subgraph-publish/action.yml)

This is a GitHub Action to perform the [`rover subgraph publish`](https://www.apollographql.com/docs/rover/commands/subgraphs#subgraph-publish) command.

### Inputs

| Name | Description | Required | Default |
| ---- | ----------- | :------: | :-----: |
| `apollo-key` | Your Apollo Studio API key | * | |
| `graph-ref` | `<NAME>@<VARIANT>` of graph in Apollo Studio | * | |
| `name` | The name of the subgraph | * | |
| `schema` | The schema file to check | * | |
| `routing-url` | Url of the running subgraph where a supergraph can route operations | [On first publish](https://www.apollographql.com/docs/rover/commands/subgraphs#subgraph-publish) | `<empty>` |
| `allow-invalid-routing-url` | Bypasses warnings and the prompt to confirm publish when the routing url is invalid in TTY environment | |  `false`  |
| `no-url`                    | Shorthand for setting an invalid `routing-url` and using `allow-invalid-routing-url`; this is predominantly used for Connectors-based subgraphs. |                                                                                                  |  `false`  |
| `log` | Specify Rover's log level | | `info` |
| `format` | Specify Rover's log format type [`plain`, `json`] | | `plain` |
| `client-timeout` | Configure the timeout length (in seconds) when performing HTTP(S) requests | | `30` |

### Usage

_**Note**: You must first install the Rover CLI_

```yaml
- uses: apollographql/rover-actions/install-rover-cli@v1
- uses: apollographql/rover-actions/subgraph-publish@v1
  with:
    apollo-key: ${{ secrets.APOLLO_KEY }}
    graph-ref: ${{ vars.APOLLO_GRAPH_REF }}
    name: subgraph-name
    schema: ./path/to/schema.graphql
    routing-url: https://sample.apollo.dev/graphql
```
