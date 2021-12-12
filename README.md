# commitlint-config-git-commit-emoji

[![npm latest][version-img]][pkg-url]
[![download][download-img]][pkg-url]
[![MIT][license-img]](LICENSE)

Shareable `commitlint` config for the VS Code extension [git-commit-plugin](https://github.com/RedJue/git-commit-plugin) with emoji enabled.
Use with [commitlint](https://github.com/conventional-changelog/commitlint).

## Getting started

```sh
npm install --save-dev @commitlint/cli commitlint-config-git-commit-emoji

echo "module.exports = {extends: ['git-commit-emoji']};" > .commitlintrc.js
```

## Format

```text
<emoji> <type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

### Example

```text
✨ feat(blog): add comment section
```

## Rules

### Problems

The following rules are considered problems for `commitlint-config-git-commit-emoji` and will yield a non-zero exit code when not met.
Consult [docs/rules](https://conventional-changelog.github.io/commitlint/#/reference-rules) for a list of available rules.

#### type-enum

- **condition**: `type` is found in value
- **rule**: `always`
- **value**

```text
[
  '🎉 init',
  '✨ feat',
  '🐞 fix',
  '📃 docs',
  '🌈 style',
  '🦄 refactor',
  '🎈 perf',
  '🧪 test',
  '🔧 build',
  '🐎 ci',
  '🐳 chore',
  '↩ revert',
]
```

```sh
echo "foo: some message" # fails
echo "🐞 fix: some message" # passes
```

#### type-case

- **description**: `type` is in case `value`
- **rule**: `always`
- **value**

```text
'lowerCase'
```

```sh
echo "FIX: some message" # fails
echo "🐞 fix: some message" # passes
```

#### type-empty

- **condition**: `type` is empty
- **rule**: `never`

```sh
echo ": some message" # fails
echo "🐞 fix: some message" # passes
```

#### scope-case

- **condition**: `scope` is in case `value`
- **rule**: `always`

```text
'lowerCase'
```

```sh
echo "🐞 fix(SCOPE): some message" # fails
echo "🐞 fix(scope): some message" # passes
```

#### subject-case

- **condition**: `subject` is in one of the cases `['sentence-case', 'start-case', 'pascal-case', 'upper-case']`
- **rule**: `never`

```sh
echo "🐞 fix(SCOPE): Some message" # fails
echo "🐞 fix(SCOPE): Some Message" # fails
echo "🐞 fix(SCOPE): SomeMessage" # fails
echo "🐞 fix(SCOPE): SOMEMESSAGE" # fails
echo "🐞 fix(scope): some message" # passes
echo "🐞 fix(scope): some Message" # passes
```

#### subject-empty

- **condition**: `subject` is empty
- **rule**: `never`

```sh
echo "🐞 fix:" # fails
echo "🐞 fix: some message" # passes
```

#### subject-full-stop

- **condition**: `subject` ends with `value`
- **rule**: `never`
- **value**

```text
'.'
```

```sh
echo "🐞 fix: some message." # fails
echo "🐞 fix: some message" # passes
```

#### subject-exclamation-mark

- **condition**: `subject` must not have a `!` before the `:` marker
- **rule**: `never`

The [angular commit
convention](hhttps://github.com/angular/angular/blob/master/CONTRIBUTING.md#commit)
dose not use a `!` to define a breaking change in the commit subject. If you
want to use this feature please consider using the [conventional commit
config](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional#commitlintconfig-conventional).

#### header-max-length

- **condition**: `header` has `value` or less characters
- **rule**: `always`
- **value**

```text
72
```

```sh
echo "🐞 fix: some message that is way too long and breaks the line max-length by several characters" # fails
echo "🐞 fix: some message" # passes
```

#### body-leading-blank

- **condition**: Body should have a leading blank line
- **rule**: `always`

```sh
echo "🐞 fix: some message
body" # fails

echo "🐞 fix: some message

body" # passes
```

#### footer-leading-blank

- **condition**: Footer should have a leading blank line
- **rule**: `always`

```sh
echo "🐞 fix: some message
BREAKING CHANGE: It will be significant" # fails

echo "🐞 fix: some message

BREAKING CHANGE: It will be significant" # passes
```

## Thanks

- Header regex pattern modified from [@gitmoji/parser-opts](https://github.com/arvinxx/gitmoji-commit-workflow/blob/master/packages/parser-opts/README.md)
- Most of the rules come from [@commitlint/config-angular](https://github.com/conventional-changelog/commitlint/blob/master/%40commitlint/config-angular/README.md)

## License

[MIT](LICENSE) © Nor Cod

<!-- badge url -->

[pkg-url]: https://www.npmjs.com/package/commitlint-config-git-commit-emoji
[version-img]: https://img.shields.io/npm/v/commitlint-config-git-commit-emoji?color=deepgreen&style=flat-square
[download-img]: https://img.shields.io/npm/dm/commitlint-config-git-commit-emoji?style=flat-square
[license-img]: https://img.shields.io/badge/license-MIT-blue?style=flat-square
