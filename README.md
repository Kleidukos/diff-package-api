# diff-package-api

## Usage

Install the [print-api](https://github.com/Kleidukos/print-api) in your development environment and build your project with GHC environment files enabled:

```bash
$ cabal build --write-ghc-environment-files=always
```

Then produce the human-readable API summary with the command:

```bash
$ print-api -p <your-package>
```

And save the output to a file in the repository. You will track this file so that the workflow may compare
its results during CI with this canonical file.

In your Workflow file, add the `--write-ghc-environment-files=always` option to your `cabal build` line, and after build and tests have passed, add:

```yaml
- name: Diff the expected and actual package APIs
  uses: kleidukos/diff-package-api@v0.0.1.0
  with:
    package-name: <my-package>
    expected-interface: <the path where you track the canonical interface file>
    ghc: <The GHC version you use in CI>
    version: 0.0.1.0 # This is the version of the print-api tool
```

If you use a job matrix, the value of the `ghc:` parameter may be `${{ matrix.ghc }}`
