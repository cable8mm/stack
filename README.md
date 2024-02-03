# Introduction

[![Markdown Validate](https://github.com/cable8mm/stack/actions/workflows/markdown-validate.yml/badge.svg)](https://github.com/cable8mm/stack/actions/workflows/markdown-validate.yml)
[![Check Markdown links](https://github.com/cable8mm/stack/actions/workflows/markdown-link-check.yml/badge.svg)](https://github.com/cable8mm/stack/actions/workflows/markdown-link-check.yml)
![GitHub Release](https://img.shields.io/github/v/release/cable8mm/stack)
![GitHub commits since latest release](https://img.shields.io/github/commits-since/cable8mm/stack/latest)
![GitHub contributors](https://img.shields.io/github/contributors/cable8mm/stack)
[![CC BY 4.0][cc-by-shield]][cc-by]

[cc-by]: https://creativecommons.org/licenses/by/2.0/kr/deed.ko
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

편하게 글을 읽으시려면 깃북으로 오세요 : [Gitbook](https://stack.palgle.com)

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

## 기여하기

기여하는 방법은 두가지가 있습니다. 본 레포지토리에 멤버로 참여하거나 본 레포지토리를 fork 한 후 PR로 글을 기여 할 수 있습니다.

멤버라면,

```sh
git clone https://github.com/cable8mm/stack.git

cd stack

git checkout -b <new-branch>
```

후에 branch를 만들어서 레포지토리에 푸쉬 합니다.

```sh
git push
```

머지를 통해서 본 레포지토리에 적용되면 자동으로 깃북은 업데이트 됩니다.

## 마크다운 문법 지키기와 링크 검사

본 레포지토리에 PR을 만들어서 푸쉬를 할 경우 마크다운 문법과 링크 검사가 자동으로 이루어 집니다. 효율을 위해서 아래의 방법으로 로컬 컴퓨터에서도 이 둘을 진행할 수 있습니다.

```sh
brew install markdownlint-cli

markdownlint-cli2 --config .markdownlint.json --fix "docs/**/*.md"
```

```sh
npm install -g markdown-link-check

find . -name \*.md -print0 | xargs -0 -n1 markdown-link-check -c mlc_config.json
```

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]
