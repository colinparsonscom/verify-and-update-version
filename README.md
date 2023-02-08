# verify-and-update-version

GitHub action to verify the version tag and release have the same name, and
update the major version tag, when there's a new latest release.

When you're releasing a semantic version, you should:

1. Manually create a new tag with the semantic version.
2. Make sure the tag matches the release name exactly, so there's no confusion
   about the distinction between a tag (a Git feature) and a release (a GitHub
   feature).
3. If the release is the latest version, update the major version tag to point
   to the current commit.

> Example: if you publish a latest release v1.2.3, you should create a new tag
> v1.2.3 when creating the release, and update the tag v1 to point to the same
> commit as v1.2.3.

It's a hassle to manually check that the tag and release are the same, delete
the old major version tag, and create a new major version tag referencing the
current commit. So this action does all that automatically every time there's a
new latest release.

Note: [GitHub generally wants version tags prefixed with v](https://docs.github.com/en/actions/creating-actions/about-custom-actions#using-tags-for-release-management)
(ex. v1.2.3 instead of 1.2.3), and this action enforces that convention
strictly. In other words, this action will intentionally fail if you don't
prefix a version tag with v.

## Usage

See [action.yml](action.yml).

## Example Workflow

```yaml
name: Verify and update my version

on:
  release:
    types: [released]

jobs:
  verify-and-update-version:
    runs-on: ubuntu-latest

    # You have to grant content:write permissions to this job in order to update
    # the major version tag.
    permissions:
      contents: write

    steps:
      - name: Verify and update version
        uses: colinparsonsme/verify-and-update-version@v1
```

## License

See the [License](LICENSE).

## Contributing

See the [Contributing Guidelines](CONTRIBUTING.md).

### Contributor Code of Conduct

See the [Code of Conduct](CODE-OF-CONDUCT.md).

## Contact

If you're interested in getting in touch outside of this project, check out
[colinparsons.com](https://colinparsons.com).
