# vyos-github-actions

<!-- start title -->

This keeps all the reusable github action workflows for vyos

## codeql-analysis ##

This reusable workflow performs codeql analysis on the invoking repo using given inputs.

This performs below:

- Checkout the code.
- Initialize codeql. This uses the input languages. Initializes for each language given in input.
- Build the code. Either using autobuild or manual build as per input.
- Analyze with codeql.

_Usage_:

```yaml
name: "Perform CodeQL Analysis"

on:
  push:
    branches: [ "current", "sagitta", "equuleus" ]
  pull_request:
    # The branches below must be a subset of the branches above
    branches: [ "current" ]
  schedule:
    - cron: '22 10 * * 0'

permissions:
  actions: read
  contents: read
  security-events: write

jobs:
  codeql-analysis-call:
    uses: vyos/vyos-github-actions/.github/workflows/codeql-analysis.yml@main
    secrets: inherit
    with:
      languages: "['python']"
```

<!-- end usage -->
<!-- start inputs -->

| **Input**              | **Description**                                                                                | **Default**    | **Required**  |
| ---------------------- | ---------------------------------------------------------------------------------------------- | ---------------| ------------- |
| **`languages`**        | Languages for CodeQL check. Supported values are: 'cpp', 'csharp', 'go', 'java', 'javascript'  | **['python']** | **false**     |
| **`codeql-cfg-path`**  | Path to a CodeQL config file                                                                   |                | **false**     |
| **`build-command`**    | Manual build command.  The multiline syntax is supported                                       |                | **false**     |

<!-- end inputs -->
Referenece:
[Codeql Action](https://github.com/github/codeql-action)


Also see the [GitHub reusable workflows documentation](https://docs.github.com/en/actions/creating-actions/sharing-actions-and-workflows-from-your-private-repository)
