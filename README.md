# Introduction

[![Markdown Validate](https://github.com/cable8mm/stack/actions/workflows/markdown-validate.yml/badge.svg)](https://github.com/cable8mm/stack/actions/workflows/markdown-validate.yml)
[![Check Markdown links](https://github.com/cable8mm/stack/actions/workflows/markdown-link-check.yml/badge.svg)](https://github.com/cable8mm/stack/actions/workflows/markdown-link-check.yml)
[![CC BY 4.0][cc-by-shield]][cc-by]

[cc-by]: https://creativecommons.org/licenses/by/2.0/kr/deed.ko
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

For read in convenient : [Gitbook](https://stack.palgle.com)

```php
<?php

Route::redirect('/')->away('https://stack.palgle.com');
```

For issue : [Github](https://github.com/cable8mm/stack/issues)

```php
<?php

Route::middleware('auth:love-developer')->group(function () {
    Route::redirect('/question', '/cable8mm/stack/issues');
    Route::redirect('/edit-or-write', '/cable8mm/stack/pulls');
});
```

## How to contribute

```sh
git clone https://github.com/cable8mm/stack.git

cd stack
```

Before writing, you should make new branch.

```sh
git checkout -b <new-branch>
```

You have written for a while, then you can push your contents.

```sh
git push
```

Finally you should make PR.

After we have reviewed your contents, it would be merged and published.

## How to lint markdown style

```sh
brew install markdownlint-cli

find . -name \*.md -print0 | xargs -0 -n1 markdownlint
```

```sh
npm install -g markdown-link-check

find . -name \*.md -print0 | xargs -0 -n1 markdown-link-check
```

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]
