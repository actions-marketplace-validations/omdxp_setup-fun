# Setup Fun Action

Downloads a Fun release bundle and adds the `fun` binary to `PATH`.

## Inputs

- `version`: Release tag (e.g. `v1.2.3`) or `latest` (default: `latest`).
- `repo`: GitHub repo in `owner/name` format (default: current repository).
- `token`: GitHub token for API requests (default: `github.token`).
- `install-dir`: Install directory (default: `${{ runner.temp }}/fun`).

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

## Fun CLI usage

```
fun -in <input_file> [-fmt | -fmt-all] [-out <output_file>] [-no-exec] [-outf] [-ast] [-help] [-- <program args...>]
fun -version
```

### Options

- `-help`: Show the help message.
- `-version`: Print version and exit.
- `-in <file>`: Input file to compile (required).
- `-fmt`: Format the input file in-place (optional).
- `-fmt-all`: Format the input file and all locally imported modules (optional).
- `-out <file>`: Output file (optional, defaults to input filename with `.c` extension).
- `-no-exec`: Disable automatic compilation and execution (optional, execution enabled by default).
- `-outf`: Generate .c output file (optional, disabled by default).
- `-ast`: Print AST nodes (optional, disabled by default).
- `--`: All following args are passed to the compiled program.
```

