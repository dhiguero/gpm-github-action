# GPM GitHub Action

This action leverages [GPM](https://github.com/dhiguero/grpc-proto-manager) to compile and generate protobuf stubs from a given protorepo. GitHub Actions is a convenient way to integrate CI/CD operations into the development process. With this action attached to a protorepo, a pull request can be checked by compiling the resulting protobuf code, and generated protobuf code in different languages can be generated and pushed on the merge event.

## Inputs

### `debug`

**Required** Whether debug information must be shown. Default `"false"`.

### `skipPublish`

**Required** This flags controls whether the process pushes the generated code to the repositories that have been modified. Set this to false for use on pull requests, and set this flag to true for pushing new code on merge events. Default `"false"`.

### `accessToken`

**Optional** This flags allows specifying a [GitHub Personal Access Tokens](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/creating-a-personal-access-token) that is required to pull and push code to private repositories.

## Outputs

### `time`

The time the action was executed.

## Example usage

Pushing new code on merge working with private repositories. A [secret](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets) with the personal access token has been defined as `GPM_PAT`.

```
on: [push]

jobs:
  generate_protos:
    runs-on: ubuntu-latest
    name: Compile and push new protos
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: GPM
        uses:  dhiguero/gpm-github-action@v0.0.3
        id: gpm
        with:
          debug: 'false'
          skipPublish: 'false'
          accessToken: ${{ secrets.GPM_PAT }}
```

## References
- https://github.com/dhiguero/grpc-proto-manager
- https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/creating-a-personal-access-token
- https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets

