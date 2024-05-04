# GitHub Action: `setup-boundary`

The `hashicorp/setup-boundary` Action sets up the [Boundary](https://www.boundaryproject.io) CLI in your GitHub Actions workflow by adding the `boundary` binary to `PATH`.

<img alt="Boundary" src="images/Boundary.png" alt="Image" width="500px"/>

<!-- TOC -->
* [GitHub Action: `setup-boundary`](#github-action-setup-boundary)
  * [Usage](#usage)
    * [OS Support](#os-support)
  * [Inputs](#inputs)
  * [Outputs](#outputs)
  * [License](#license)
  * [Code of Conduct](#code-of-conduct)
<!-- TOC -->

## Usage

Create a GitHub Actions Workflow file (e.g.: `.github/workflows/boundary.yml`):

```yaml
name: boundary

on:
  push:

env:
  PRODUCT_VERSION: "0.16.0"

jobs:
  boundary:
    runs-on: ubuntu-latest
    name: Run Boundary
    steps:
      - name: Setup `boundary`
        uses: hashicorp/setup-boundary@main
        id: setup
        with:
          version: "latest"

      - name: Run `boundary connect`
        id: connect
        run: "boundary connect -target-id ttcp_1234567890"
```

In the above example, the following definitions have been set.

- The event trigger has been set to `push`. For a complete list, see [Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows).
- The origin of this GitHub Action has been set as `hashicorp/setup-boundary@main`. For newer versions, see the [Releases](https://github.com/hashicorp/setup-boundary/releases).
- The version of `boundary` to set up has been set as `0.16.0`. For a complete list, see [releases.hashicorp.com](https://releases.hashicorp.com/boundary/).
- The Boundary Target to interact with has been set as `ttcp_1234567890`.

> [!NOTE]
> To retrieve the `latest` version, this GitHub Action polls the HashiCorp [Releases API](https://api.releases.hashicorp.com/v1/releases/boundary) and finds the latest released version of Boundary that isn't marked as a pre-release (`is_prerelease`).

These definitions may require updating to suit your deployment, such as specifying [self-hosted](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#choosing-self-hosted-runners) runners.

Additionally, you may configure [outputs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#example-defining-outputs-for-a-job) to consume return values from the Action's operations.

### OS Support

The action can be run on `ubuntu-latest`, `windows-latest`, and `macos-latest` GitHub Actions runners.

> [!IMPORTANT]
> When running on `windows-latest` the shell must be set to `bash`.

## Inputs

This section contains a list of all inputs that may be set for this Action.

- `version` - The version of `boundary` to install. Defaults to `latest` if unset.

## Outputs

This section contains a list of all outputs that can be consumed from this Action.

- `version` -  The version of `boundary` that was installed.

## License

Licensed under the Mozilla Public License, Version 2.0 (the "License").

See the License for the specific language governing permissions and limitations under the License.

## Code of Conduct

[Code of Conduct](CODE_OF_CONDUCT.md)