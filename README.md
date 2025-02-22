# Hash Files in CI

A very simple action to calculate the SHA256 (only, for now) hash of a given file and expose it as output.

Primary usecase: sharing artifacts between jobs and needing to verify integrity between them.

This only exists because I need to do it over and over again.

## Usage

### Inputs

* `path`
  * Path to the file to hash.

### Outputs

* `sha256`
  * The hexadecimal representation of the SHA256 hash of the content of `path`.

### Example

```yaml
- name: Calculate hash
  id: hash
  uses: fionn/action-hash@master
  with:
    path: path/to/file

- name: Check SHA256
  run: echo "$HASH  path/to/file" | sha256sum -c -
  shell: bash
  env:
    HASH: ${{ steps.hash.outputs.sha256 }}
```
