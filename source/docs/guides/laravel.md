---
title: Laravel Guide
description: The Laravel Guide
extends: _layouts.documentation
section: content
---

# Laravel Guide

Pest was built with Laravel in mind. In this guide, we are going
to see how can you create tests with the elegance you expect, and
with the convenience you love.

Once you [install Pest](/docs/installation) in your Laravel application, and because Pest is a **progressive testing framework**,
your current test suite will still work, even if you run it with the `./vendor/bin/pest` console command.

Now, let's get started by taking a look at the default test suite in Laravel:

```bash
- tests
    - Feature
        - ExampleTest.php
    - Unit
        - ExampleTest.php
    - CreatesApplication.php
    - TestCase.php
- phpunit.xml
```

First, let's run the `pest:install` artisan command:
```bash
php artisan pest:install
```

This command will create the `Pest.php` file with the contents:
```php
<?php

uses(Tests\TestCase::class)->in('Feature');
```

Next, let's migrate the `tests/Unit/ExampleTest.php`:
```php
<?php

test('basic')->assertTrue(true);
```

and the `tests/Feature/ExampleTest.php`:
```php
<?php

it('has welcome page')
    ->get('/')
    ->assertStatus(200);
```

And that's it! You should now have a fresh Laravel installation with
a test suite in Pest.

---

## Artisan commands

### `pest:install`

The `pest:install` Artisan command creates the `test/Pest.php` file in your tests folder.

```
php artisan pest:install
```

As described on the [Underlying Test Case](/docs/underling-test-case) section,
the `Pest.php` is the place where all your `uses` should live.

### `pest:test`

The `pest:test <name>` Artisan command creates a new test in the `tests/Feature` folder.

```
php artisan pest:test UsersTest
```

Optionally, you can provide the option `--unit` to create the
given test under the `tests/Unit` folder.

```
php artisan pest:test UsersTest --unit
```

### `pest:dataset`

The `pest:dataset` Artisan command creates a new dataset in the `tests/Datasets` folder.

```
php artisan pest:dataset Emails
```

As detailed on the [Datasets](/docs/datasets) section, datasets allows you to
run the same test multiple times with different data.

---

## Traits

As explained in the [Underlying Test Case](/docs/underlying-test-case) section, the usage
of traits in Pest is possible with the `uses` function.

```
<?php

use App\User;
use Illuminate\Foundation\Testing\RefreshDatabase;

uses(RefreshDatabase::class);

beforeEach(fn () => factory(User::class)->create());

it('has users')->assertDatabaseHas('users', [
    'id' => 1,
]);
```

Keep in mind that you can avoid the `uses(RefreshDatabase::class)`
line, adding that same line to your `Pest.php` file.

Next section: [PHPUnit →](/docs/guides/phpunit)
