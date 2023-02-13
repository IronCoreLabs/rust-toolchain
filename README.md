# Install Rust Toolchain

This GitHub Action installs a Rust toolchain using rustup. It is designed for
one-line concise usage and good defaults.

## Example workflow

```yaml
name: test suite
on: [push, pull_request]

jobs:
  test:
    name: cargo test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: IronCoreLabs/rust-toolchain@v1
      - run: cargo test --all-features
```

## Toolchain File

The [Rust toolchain file](https://rust-lang.github.io/rustup/overrides.html#the-toolchain-file) is supported.
If present it will be used to populate `toolchain`, `components` and `targets` parameters. If those parameters are explicitly set as inputs to the action, they will take precedence over the values in the toolchain file. To use only the toolchain file for parameters, pass no inputs and set the `@rev` to `@v1`.

## Inputs

All inputs are optional.

<table>
<tr>
  <th>Name</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>toolchain</code></td>
  <td>
    Rustup toolchain specifier e.g. <code>stable</code>, <code>nightly</code>, <code>1.42.0</code>, <code>nightly-2022-01-01</code>. Defaults to <code>stable</code> if not passed or in the <code>rust-toolchain.toml</code>.
  </td>
</tr>
<tr>
  <td><code>targets</code></td>
  <td>Comma-separated string of additional targets to install e.g. <code>wasm32-unknown-unknown</code></td>
</tr>
<tr>
  <td><code>components</code></td>
  <td>Comma-separated string of additional components to install e.g. <code>clippy, rustfmt</code></td>
</tr>
</table>

## Outputs

<table>
<tr>
  <th>Name</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>toolchain</code></td>
  <td>
    Rustup's name for the selected version of the toolchain. "1.62.0"
  </td>
</tr>
<tr>
  <td><code>cachekey</code></td>
  <td>A short hash of the rustc version, appropriate for use as a cache key. ex "20220627a831"</td>
</tr>
</table>

## Outputs

<table>
<tr>
  <th>Name</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>cachekey</code></td>
  <td>A short hash of the installed rustc version, appropriate for use as a cache key. <code>"20220627a831"</code></td>
</tr>
<tr>
  <td><code>name</code></td>
  <td>Rustup's name for the selected version of the toolchain, like <code>"1.62.0"</code>. Suitable for use with <code>cargo +${{steps.toolchain.outputs.name}}</code>.</td>
</tr>
</table>

<br>

## Toolchain expressions

The following forms are available for projects that use a sliding window of
compiler support.

```yaml
     # Installs the most recent stable toolchain as of the specified time
     # offset, which may be written in years, months, weeks, or days.
  - uses: IronCoreLabs/rust-toolchain@v1
    with:
      toolchain: stable 18 months ago
```

```yaml
     # Installs the stable toolchain which preceded the most recent one by
     # the specified number of minor versions.
  - uses: IronCoreLabs/rust-toolchain@v1
    with:
      toolchain: stable minus 8 releases
```

## License

The scripts and documentation in this project are released under the [MIT
License].

[MIT License]: LICENSE
