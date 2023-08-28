# rover-actions

**The code in this repository is experimental and has been provided for reference purposes only. Community feedback is welcome but this project may not be supported in the same way that repositories in the official [Apollo GraphQL GitHub organization](https://github.com/apollographql) are. If you need help you can file an issue on this repository, [contact Apollo](https://www.apollographql.com/contact-sales) to talk to an expert, or create a ticket directly in Apollo Studio.**

## [install-rover-cli](./install-rover-cli/action.yml)

This is a GitHub Action to install the [Apollo Rover CLI](https://rover.apollo.dev/) on action runners. Once installed, `rover` is added to `PATH`, so it can be used in subsequent steps.

### Inputs

| Name | Description | Default |
| ---- | ----------- | ------- |
| `version` | The version of [`rover`](https://rover.apollo.dev/) to install | `latest` |

### Usage

Installing a specific version of `rover`:

```yaml
- uses: apollosolutions/rover-actions/install-rover-cli@v1
  with:
    version: 0.18.1
```

Install the latest version:

```yaml
- uses: apollosolutions/rover-actions/install-rover-cli@v1
```

Run a rover command after install:

```yaml
- uses: apollosolutions/rover-actions/install-rover-cli@v1
- name: Run schema check
  env:
    APOLLO_KEY: ${{ secrets.APOLLO_KEY }}
  run: rover subgraph check ${{ env.APOLLO_GRAPH_REF }} --name subgraph-name --schema ./path/to/schema.graphql
```
