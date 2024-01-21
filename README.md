# semver-pre-release
 
Enforce the ref for a pre-release.  The git ref:

- MUST be a SemVer version
- MUST have a pre-release version

## Using

``` yaml
name: Pre-Release

on:
  release:
    types: [prereleased]

jobs:
  publish_pre_release:
    runs-on: ubuntu-latest
    name: NAME
    steps:
      - name: Enforce SemVer for pre-release
        id: enforce_semver
        uses: NetChris/semver-pre-release@v0
      - name: Use the SemVer version
        run: echo Do something with semver_version: ${{ steps.enforce_semver.outputs.semver_version }}
```

## Notes

Although not a concern of this action, it's important to point out an issue with the `prereleased` release type.  From [the GitHub documentation](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#release), there is an issue releasing a _draft_ pre-release:

> Note: The prereleased type will not trigger for pre-releases published from draft releases, but the published type will trigger. If you want a workflow to run when stable and pre-releases publish, subscribe to published instead of released and prereleased.
