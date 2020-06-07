# Introduction

![Markdown Validate](https://github.com/esc-company/helloworld/workflows/Markdown%20Validate/badge.svg)
[![CC BY 4.0][cc-by-shield]][cc-by]

[cc-by]: https://creativecommons.org/licenses/by/2.0/kr/deed.ko
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

For read in convenient : [Gitbook](https://helloworld.holapet.com)

```php
<?php

Route::redirect('/')->away('https://helloworld.holapet.com');
```

For issue : [Github](https://github.com/esc-company/helloworld/issues)

```php
<?php

Route::middleware('auth:love-holapet')->group(function () {
    Route::redirect('/question', '/esc-company/helloworld/issues');
    Route::redirect('/edit-or-write', '/esc-company/helloworld/pulls');
});
```

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]