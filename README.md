<!--
SPDX-License-Identifier: Apache-2.0
SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 🏷️ Check Semantic Versioning String/Tag

Validates a given string for conformity to Semantic Versioning.

Refer to the site/documentation: [Semantic Versioning](https://semver.org/)

## tag-validate-semantic-action

## Usage Example

Pass the string to check as input to the action:

```yaml
steps:
  - name: "Check string for: SemVer"
    if: startsWith(github.ref, 'refs/tags/')
    uses: lfreleng-actions/tag-validate-semantic-action@main
    with:
      string: ${{ github.ref_name }}
```

## Inputs

<!-- markdownlint-disable MD013 -->

| Name          | Required | Default   | Description                                     |
| ------------- | -------- | --------- | ----------------------------------------------- |
| string        | True     | N/A       | Tag/version string to check for conformity      |
| exit_on_fail  | False    | false     | Exits/aborts with error if check fails          |

<!-- markdownlint-enable MD013 -->

## Outputs

<!-- markdownlint-disable MD013 -->

| Name        | Description                                                |
| ----------- | ---------------------------------------------------------- |
| valid       | Set true when tag/string conforms to Semantic Versioning   |
| dev_version | Set true when tag contains pre-release/development strings |

<!-- markdownlint-enable MD013 -->

## Implementation Details

For further details: <https://regex101.com/r/vkijKf/1/>

The RegEx used for semantic compliance is:

`pattern="^(0|[1-9]\d*)\.(0|[1-9]\d*)\.(0|[1-9]\d*)(?:-((?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*)(?:\.(?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*))*))?(?:\+([0-9a-zA-Z-]+(?:\.[0-9a-zA-Z-]+)*))?$"`

The RegEx used for development compliance is:

`pattern="(dev|pre|alpha|beta|rc|snapshot|nightly|canary|preview)"`

For further details: <https://regex101.com/r/yHAIUN/1>

The second RegEx uses the grep flags `"-Eqi"` which makes the match
case-insensitive and allows for partial matches.
