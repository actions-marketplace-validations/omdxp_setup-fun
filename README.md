# Setup Fun Action

Downloads a Fun release bundle and adds the `fun` binary to `PATH`.

## Inputs

- `version`: Release tag (e.g. `v1.2.3`) or `latest` (default: `latest`).
- `repo`: GitHub repo in `owner/name` format (default: `omdxp/fun`; if blank, falls back to `$GITHUB_REPOSITORY`).
- `token`: GitHub token for API requests (default: empty; if blank, falls back to `$GITHUB_TOKEN`/`${{ github.token }}`).
- `install-dir`: Install prefix passed to `install.sh --prefix` on Linux/macOS, and MSI extraction root on Windows (default: empty; if blank, uses `${{ runner.temp }}/fun`).

## Outputs

- `fun-path`: Full path to the `fun` binary.
- `version`: Resolved release tag.
- `install-dir`: Installation root directory.
- `target`: Resolved release target.

## Example

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: omdxp/setup-fun@v1
        with:
          version: latest
      - run: fun -version
```

Pinning a specific release instead of tracking `latest`:

```yaml
      - uses: omdxp/setup-fun@v1
        with:
          version: v0.45.0
```

## CLI usage

Run `fun -help` for the flags and subcommands supported by the version you installed. Full documentation lives in the [compiler repository](https://github.com/omdxp/fun).

## Compiler overrides

The generated C is built with a host C compiler, which you can override on a runner:

- `FUN_CC`: Overrides the compiler executable.
- `FUN_CC_ARGS`: Extra arguments appended to the compiler command.

Defaults are `gcc` on Linux/macOS and MSVC `cl` on Windows.
