# PHP 코딩 가이드라인

ESC Company에서 개발할 때 지켜야 하는 가이드라인을 설명합니다.

- [일반적인 PHP 룰](#일반적인-php-룰)
  - [컨벤션](#컨벤션)
  - [폴더 규칙](#폴더-규칙)
  - [이미 예약된 파일 이름](#이미-예약된-파일-이름)
  - [Composer 네임스페이스](#composer-네임스페이스)
  - [타입과 주석](#타입과-주석)
  - [삼항 연산자\(Ternary operators\)와 복수 파라미터](#삼항-연산자ternary-operators와-복수-파라미터)
- [에디터 설정](#에디터-설정)
  - [스타일 픽서](#스타일-픽서)
  - [VSCode Setting Example](#vscode-setting-example)

## 일반적인 PHP 룰

ESC Company에서는 PHP 7.3 이상을 기반으로 합니다.

PHP의 코딩에 있어서 [PSR-1](https://psr.kkame.net/accepted/psr-1-basic-coding-standard), PSR-2, [PSR-12](https://psr.kkame.net/accepted/psr-12-extended-coding-style-guide)는 반드시 지켜져야 합니다.

### 컨벤션

|            | Case Type                | Example           |
| :--------- | :----------------------- | :---------------- |
| Classes    | PascalCase               | HolapetClass      |
| Methods    | camelCase                | holapetMethod     |
| Properties | camelCase                | holapetProperty   |
| Constant   | UPPER\_CASE\_SNAKE\_CASE | HOLAPET\_CONSTANT |

### 폴더 규칙

폴더 규칙은 [pds/skeleton](https://github.com/php-pds/skeleton)를 지켜야 합니다.

|                | Folder Name | Example                        |
| :------------- | :---------- | :----------------------------- |
| Sources        | src/        | src/HelapetClass.php           |
| Test Sources   | tests/      | tests/holapetClassTest.php     |
| Configure      | config/     | config/config.php              |
| Resource Files | resources/  | resources/app.css              |
| Execute Files  | bin/        | bin/process\_join\_user\_count |
| Documents      | docs/       | docs/how-to-build.md           |

### 이미 예약된 파일 이름

|             | Folder Name |
| :---------- | :---------- |
| Information | README.md   |

### Composer 네임스페이스

모든 라이브러리는 `Composer` 규격에 맞는 네임스페이스를 지켜야 합니다.

### 타입과 주석

PHP 7부터는 리턴타입을 지원하기 때문에 메쏘드나 함수의 리턴타입을 주석으로 표기하지 않습니다.

```php
<?php

function sum($a, $b): float {
    return $a + $b;
}
?>
```

```php
<?php

class C {}

function getC(): C {
    return new C;
}
?>
```

모든 주석은 [phpdoc.org의 최신판](https://docs.phpdoc.org/latest/)에서 제공하는 규격을 정확히 따라야 합니다.

특히 인라인 태그 레퍼런스와 태그 레퍼런스의 의미에 맞는 태그를 사용하세요.

인라인 태그 레퍼런스 :

|             | Example                                                                                                                                                      |
| :---------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| @example    | @example example1.php Counting in action.                                                                                                                    |
| @internal   | @internal                                                                                                                                                    |
| @inheritdoc | @inheritdoc                                                                                                                                                  |
| @link       | @link [http://example.com/my/bar](http://example.com/my/bar) Documentation of Foo.                                                                           |
| @see        | @see [http://example.com/my/bar](http://example.com/my/bar) Documentation of Foo. / @see MyClass::$items           For the property whose items are counted. |

태그 레퍼런스 :

```text
@api
@author
@category
@copyright
@deprecated
@example
@filesource
@global
@ignore
@internal
@license
@link
@method
@package
@param
@property
@property-read
@property-write
@return
@see
@since
@source
@subpackage
@throws
@todo
@uses & @used-by
@var
@version
```

주석의 타입에서 [mixed는 2019년 2월 7일 PHP RFC를 통해서 명확히 정의](https://wiki.php.net/rfc/mixed-typehint)가 되었으므로, 다른 의미로 절대 사용하지 않습니다.

```text
// Good
mixed = string | bool | int | float | resource | array | object | callable | null

// Bad
mixed = string | null
```

mixed 타입에 void는 포함되지 않음을 유의하세요.

### 삼항 연산자\(Ternary operators\)와 복수 파라미터

삼항 연산자와 복수 파라미터의 표기는 다음에 나오는 것이 필수인지 아닌지로 구분합니다.

예를 들어서 삼항 연산자나 `compact` 함수와 같이 필수일 경우 컴마를 앞에 붙입니다.

```php
$result = $object instanceof Model
    ? $object->name
    : 'A default value';

compact(
    'seoul'
    , 'inchon'
    , 'jeju'
);
```

반면 배열과 같이 필수가 아닐 경우 뒤에 붙입니다.

```php
[
    'seoul',
    'inchon',
    'jeju',
]
```

이 경우에는 마지막 컴마를 삭제하지 않음을 유의하세요.

## 에디터 설정

### 스타일 픽서

VSCode에서는 [php\_cs\_fixer를 설치](https://github.com/junstyle/vscode-php-cs-fixer)하며, 아래와 같은 설정을 이용합니다.

```php
<?php

return PhpCsFixer\Config::create()
->setRules([
    '@PSR2' => true,
    'blank_line_after_opening_tag' => true,
    'braces' => [
        'allow_single_line_closure' => true,
    ],
    'compact_nullable_typehint' => true,
    'concat_space' => ['spacing' => 'one'],
    'declare_equal_normalize' => ['space' => 'none'],
    'function_typehint_space' => true,
    'new_with_braces' => true,
    'method_argument_space' => ['on_multiline' => 'ensure_fully_multiline'],
    'no_empty_statement' => true,
    'no_leading_import_slash' => true,
    'no_leading_namespace_whitespace' => true,
    'no_whitespace_in_blank_line' => true,
    'return_type_declaration' => ['space_before' => 'none'],
    'single_trait_insert_per_statement' => true,

    'array_indentation' => true,
    'array_syntax' => ['syntax' => 'short'],
    'combine_consecutive_unsets' => true,
    'method_separation' => true,
    'no_multiline_whitespace_before_semicolons' => true,
    'single_quote' => true,

    'binary_operator_spaces' => [
        'align_double_arrow' => false,
        'align_equals' => false,
    ],
    'hash_to_slash_comment' => true,
    'include' => true,
    'lowercase_cast' => true,
    'no_extra_consecutive_blank_lines' => [
        'curly_brace_block',
        'extra',
        'parenthesis_brace_block',
        'square_brace_block',
        'throw',
        'use',
    ],
    'no_multiline_whitespace_around_double_arrow' => true,
    'no_spaces_around_offset' => true,
    'no_unused_imports' => true,
    'no_whitespace_before_comma_in_array' => true,
    'object_operator_without_whitespace' => true,
    'single_blank_line_before_namespace' => true,
    'ternary_operator_spaces' => true,
    'trim_array_spaces' => true,
    'unary_operator_spaces' => true,
    'whitespace_after_comma_in_array' => true,
])
->setLineEnding("\n");
```

### VSCode Setting Example

```json
{
    "git.autofetch": true,
    "php.validate.executablePath": "/usr/local/bin/php",
    "git.confirmSync": false,
    "php-cs-fixer.rules": "@PhpCsFixer",
    "php-cs-fixer.executablePath": "php-cs-fixer",
    "[php]": {
        "editor.defaultFormatter": "junstyle.php-cs-fixer",
        "editor.formatOnSave": true
    },
    "markdown.preview.scrollEditorWithPreview": false,
    "editor.minimap.enabled": false,
    "explorer.openEditors.visible": 0,
    "editor.fontSize": 14,
    "workbench.startupEditor": "newUntitledFile",
    "files.associations": {        
        "*.ctp": "php",
        "*.json": "jsonc",
        "*.min.js": "plaintext",
        "*.min.css": "plaintext",
        "*.php_cs": "php"
    },
    "explorer.confirmDelete": false,
    "workbench.activityBar.visible": true,
    "emmet.showExpandedAbbreviation": "inMarkupAndStylesheetFilesOnly",
    "emmet.triggerExpansionOnTab": true,
    "blade.format.enable": true,
    "beautify.language": {
        "js": {
            "type": [
                "javascript",
                "json",
                "jsonc"
            ],
            "filename": [
                ".jshintrc",
                ".jsbeautifyrc"
            ]
        },
        "css": [
            "css",
            "less",
            "scss"
        ],
        "html": [
            "htm",
            "html",
            "blade"
        ]
    },
    "typescript.tsserver.log": "terse",
    "npm.packageManager": "yarn",
    "prettier.packageManager": "yarn",
    "eslint.packageManager": "yarn",
    "eslint.run": "onSave",
    "[jsonc]": {
        "editor.defaultFormatter": "vscode.json-language-features"
    },
    "window.zoomLevel": 0,
    "intelephense.format.enable": false,
    "php-cs-fixer.documentFormattingProvider": true,
    "php-cs-fixer.formatHtml": true,
    "php-cs-fixer.config": "/Users/cable8mm/.vscode/.php_cs",
    "intelephense.environment.documentRoot": "public",
    "intelephense.trace.server": "messages",
    "editor.suggestSelection": "first",
    "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
    "files.exclude": {
        "**/node_modules": true,
        "vendor": true
    },
    "intelephense.environment.phpVersion": "7.3.14",
    "editor.rulers": [],
    "editor.fontFamily": "'IBM Plex Mono', Menlo, Monaco, 'Courier New', monospace",
    "workbench.iconTheme": "material-icon-theme",
    "diffEditor.ignoreTrimWhitespace": false,
    "editor.formatOnSave": true,
    "typescript.format.enable": false,
    "[blade]": {
        "editor.defaultFormatter": "onecentlin.laravel-blade",
        "editor.formatOnSave": false
    },
    "php-docblocker.qualifyClassNames": true,
    "[json]": {
        "editor.defaultFormatter": "vscode.json-language-features"
    },
    "git.enableCommitSigning": true,
    "workbench.colorTheme": "Laravel Extra - Github",
    "markdown.extension.toc.levels": "2..6"
}
```