# Setup OPA GitHub Action

GitHub action to configure the [Open Policy Agent CLI](https://www.openpolicyagent.org/docs/latest/cli/) in your GitHub Actions workflow.

[Open Policy Agent (OPA)](https://github.com/open-policy-agent/opa) is an open source, general-purpose policy engine. 

## Running tests

This GitHub Action works great to run any [tests](https://www.openpolicyagent.org/docs/latest/policy-testing/) you have included with your Rego files.

## Basic Usage

Here we see a simple template that checks out the repository code, installs the latest OPA, and then runs all of the Rego files in the `tests` directory. 

```yml
name: Run OPA Tests  
on: [push]
jobs:
  Run-OPA-Tests:
    runs-on: ubuntu-latest
    steps:
    - name: Check out repository code
      uses: actions/checkout@v2

    - name: Setup OPA
      uses: open-policy-agent/setup-opa@v1
      with:
        version: latest

    - name: Run OPA Tests 
      run: opa test tests/*.rego -v
```

## Choose OPA Version

When OPA is installed on the GitHub runner, you can select a the specific version of OPA you wish to run.

```yml
steps:
  - name: Setup OPA
    uses: open-policy-agent/setup-opa@v1
    with:
      version: 0.34.1
```

Or, OPA can be locked to a [SemVer range](https://www.npmjs.com/package/semver#ranges).

```yml
steps:
  - name: Setup OPA
    uses: open-policy-agent/setup-opa@v1
    with:
      version: 0.34.x
```

```yml
steps:
  - name: Setup OPA
    uses: open-policy-agent/setup-opa@v1
    with:
      version: 0.34
```

```yml
steps:
  - name: Setup OPA
    uses: open-policy-agent/setup-opa@v1
    with:
      version: <0.34
```

You may also use the `latest` or `edge` version.

```yml
steps:
  - name: Setup OPA
    uses: open-policy-agent/setup-opa@v1
    with:
      version: latest
```

```yml
steps:
  - name: Setup OPA
    uses: open-policy-agent/setup-opa@v1
    with:
      version: edge
```

You can also choose to run your tests against multiple versions of OPA.

```yml
strategy:
  matrix:
    version: [latest, 0.38.x, 0.37.x]
steps:
  - name: Setup OPA
    uses: open-policy-agent/setup-opa@v1
    with:
      version: ${{ matrix.version }}
```

## Inputs

The action supports the following inputs:

- `version`: Optional, defaults to `latest`.  `latest`, `edge`, and [SemVer ranges](https://www.npmjs.com/package/semver#ranges) are supported, so instead of a [full version](https://github.com/open-policy-agent/opa/releases) string, you can use `0.35`. This enables you to automatically get the latest backward compatible changes in the v0.35 release.

## Outputs

This action does not set any direct outputs.

## Credits

Thanks to the folks over at [Infracost](https://github.com/infracost/infracost) who created the initial version of this repository. 

## Contributions
Contributions are welcome! See [Contributor's Guide](https://www.openpolicyagent.org/docs/latest/contributing/)

## Code of Conduct
👋 Be nice. See our [code of conduct](https://github.com/open-policy-agent/opa/blob/main/CODE_OF_CONDUCT.md)