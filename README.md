# Git Hooks
Repository for various git hooks that I use.

The `multihook` delegator script is based on [Konfekt's script](https://gist.github.com/Konfekt/d9e86763b0f3febd7b2f7ca589f6c482).

## Installation
Using at least git version 2.9. Clone the repo to whereever you want it and set the `core.hooksPath`:
```
git clone https://github.com/0siriz/githooks githooks
git config --global core.hooksPath $(pwd)/githooks
```

And it should work automagically from there

Else copy all the files into the `.git/hooks` directory in your repo
```
git clone https://github.com/0siriz/githooks /tmp/githooks
cp -r /tmp/githooks/* .git/hooks/
```

## Dependencies
- `pre-commit.d/00-gitleaks` requires the [gitleaks](https://github.com/gitleaks/gitleaks) utility

## Conditional hooks

To only run a hook when certain conditions are met, create an executable sidecar file named `<hookname>.condition` next to the hook script. If the condition file exits non-zero, the hook is silently skipped (no terminal output).

Example — only run Go linting in Go projects (`pre-commit.d/00-golint.condition`):

```sh
#!/usr/bin/env bash
test -f go.mod && command -v golangci-lint >/dev/null 2>&1
```

This pairs naturally with project-specific hooks: place a language/tool check in the `.condition` file and the hook script itself stays focused on the actual linting logic.

Several bundled hooks include `.condition` files to only run when relevant:
- `pre-commit.d/00-gitleaks` won't run until the gitleaks utility is installed separately (it fails if absent)
- `pre-commit.d/01-nonascii-filenames.condition` checks `hooks.allownonascii` — set it to `true` to disable

## Notes
I like having my commits signed, and so `post-commit.d/99-warn-unsigned` and `post-rewrite.d/99-warn-unsigned` will warn of missing commit signature, if you dont want this then you are welcome to delete them

To use `commit-msg.d/00-commitlint` to lint commit messages against [conventional commits](https://conventionalcommits.org), with configured types (and optionally scopes), create a `.commitlintrc` file at the root of your git repo:
```sh
TYPES=(
  "feat"
  "fix"
  "build"
  "ci"
  "docs"
  "perf"
  "refactor"
  "style"
  "test"
)
SCOPES=()
SUBJECT_MAX=50
```
