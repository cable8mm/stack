# Knowledge Acquisition

## phpunit.xml 이 로컬과 ci 서버 설정이 달라요

`phpunit.xml`과 `phpunit.xml.dist`의 우선순위는 `phpunit.xml`이 더 높습니다. 따라서, 로컬에서 사용해야 하는 설정을 `phpunit.xml`로 하고, 서버에서의 설정을 `phpunit.xml`로 합니다.

ci 서버의 전처리기에서 phpunit.xml을 삭제하던지 아니면 `phpunit.xml.dist`를 `phpunit.xml`로 `cp` 하시면 됩니다.

## Git에서 원격에서만 파일을 없애고 싶어요

특정 파일을 제거할 경우,

```sh
git rm --cached <파일명>
```

특정 디렉토리를 제거할 경우,

```sh
git rm --cached -r <디렉토리명>
```

## phpunit에서 IDE의 자동완성기능이 작동하지 않아요

`phpunit`이 설치가 안되어 있다면:

```sh
composer require phpunit/phpunit --dev
```

`phpunit`이 설치가 되어 있다면:

```sh
composer remove phpunit/phpunit --dev
composer require phpunit/phpunit --dev
```

## iOS 13에서 iPad WKWebview의 유저에이젼트가 Mac으로 표기됩니다

`WKWebpagePreferences`의 [preferredContentMode](https://developer.apple.com/documentation/webkit/wkwebpagepreferences/3194426-preferredcontentmode?language=objc)를 `.mobile`로 설정.

## 맥 업데이트 후 "gpg: WARNING: no command supplied"

맥을 업데이트하고 `gpg: WARNING: no command supplied` 워닝이 나오고 푸쉬가 되지 않을 때에는 이렇게 해 본다.

```bash
git config --global gpg.program "/usr/local/bin/gpg"
```
