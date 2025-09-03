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
- `pre-commit.d/00-gitleaks` requires the [gitleaks](https://github.com/gitleaks/gitleaks) utility is installed

## Notes
I like having my commits signed, and so `post-commit.d/99-warn-unsigned` and `post-rewrite.d/99-warn-unsigned` will warn of missing commit signature, if you dont want this then you are welcome to delete them
