# Introduction

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
