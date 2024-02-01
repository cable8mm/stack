---
description: Share your stacks and stories
---

# Introduce

For read in convenient : [Gitbook](https://stack.palgle.com)

```php
Route::redirect('/')->away('https://stack.palgle.com');
```

For issue : [Github](https://github.com/cable8mm/stack/issues)

```php
Route::middleware('auth:love-developer')->group(function () {
    Route::redirect('/question', '/cable8mm/stack/issues');
    Route::redirect('/edit-or-write', '/cable8mm/stack/pulls');
});
```

Share your stacks and stories!
