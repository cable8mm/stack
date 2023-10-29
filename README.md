# Introduction

![Markdown Validate](https://github.com/cable8mm/stack/workflows/Markdown%20Validate/badge.svg)
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

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]
