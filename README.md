# update-version

GitHub action to verify the version tag and release have the same name, and
update the major version tag, when there's a new latest release.

Whenever you're publishing a release with a semantic version, you should
manually create a new tag with the semantic version. You then should make sure
the tag matches the release name exactly, so that there's no confusion about the
distinction between a tag (a Git feature) and a release (a GitHub feature). If
this release isn't a pre-release (so it shouldn't be labeled a prelease and
shouldn't have a suffix, like -alpha), and it's the latest version, you then
should update the major version tag to point to this commit.

> Example: if you publish a latest release v1.2.3, you should create a new tag
> v1.2.3 when creating the release, and update the tag v1 to point to the same
> commit as v1.2.3.

It's a hassle to remember to manually check that the tag and release are the
same, delete the old major version tag, and create a new major version tag
referencing the current commit. So this action does all that automatically every
time there's a new stable latest release.

## Usage

See [action.yml](action.yml).

## Example Workflow

```yaml
name: Update my version

on:
  release:
    types: [released]

jobs:
  publish:
    runs-on: ubuntu-latest

    # You have to grant content:write permissions to this job in order to update
    # the major version tag.
    permissions:
      contents: write

    steps:
      - name: Update version
        uses: colinparsonsme/update-version@v1
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
