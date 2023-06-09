![tests](https://img.shields.io/github/workflow/status/gruppe-adler/action-release-with-hemtt/test?label=tests)
[![codecov](https://codecov.io/gh/gruppe-adler/action-release-with-hemtt/branch/master/graph/badge.svg)](https://codecov.io/gh/gruppe-adler/action-release-with-hemtt)

# action-release-with-hemtt

This action builds your [HEMTT](https://github.com/synixebrett/HEMTT) mod and then zips it. You could then use that zip and attach it as an artifact or to a release.

## Inputs

### `zip_build`
This input is optional (Default: `true`)
Whether the build should be zipped.

### `cwd`
This input is optional (Default: `.`)
Working directory of *hemtt*.

## Outputs

### `release_path`
Relative path of released addon before it is zipped. (is equal to `./releases/<version>`)

### `mod_name`
Name of mod. (is equal to `modname` inside hemtt.toml)

### `zip_path`
Relative path of zipped mod. Will be not set if input `zip_build` is `false`

### `zip_name`
Name of packed mod (without file extension). Will be not set if input `zip_build` is `false`.

## Example usage

```yaml
steps:
- uses: actions/checkout@master

- uses: gruppe-adler/action-release-with-hemtt@v3
  id: build

- run: echo 'Release ${{ steps.build.outputs.zip_name }} is ready.'

- uses: actions/upload-artifact@v3
  with:
    name: 'packed-mod'
    path: ${{ steps.build.outputs.zip_path }}
```

## License
The scripts and documentation in this project are released under the [MIT License](LICENSE)
