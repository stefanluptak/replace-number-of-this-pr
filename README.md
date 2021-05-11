# Replace <NUMBER_OF_THIS_PR> with an actual number

_GitHub Action to replace `<NUMBER_OF_THIS_PR>` in the PR title or text with an actual number of that PR_

## Motivation

I needed to generate URLs in our PR body that contained the actual PR number. The rest of the URL was static, co I just needed to put some `substring` in it and then replace it programmatically.

## Usage

```yaml
name: PR body substitutions

on:
  pull_request:
    types:
      - opened

jobs:
  fill-pr-body:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - uses: stefanluptak/replace-number-of-this-pr@v1
```

## Notes

It's needed to have the `actions/checkout@v2` step before this action, otherwise the `hub` command inside the action won't know on what git repository to operate.

If you're using Dependabot, you might want to consider putting `if: startsWith(github.head_ref, 'dependabot') != true` on top of your job definition to prevent this action running on PRs made by Dependabot.