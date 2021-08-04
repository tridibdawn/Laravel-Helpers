# Laravel Helpers
How to create global helpers in Laravel

<p>To start off I created a folder in my <code>app</code> directory called <code>Helpers</code>. Then within the <code>Helpers</code> folder I added files for functions I wanted to add. Having a folder with multiple files allows us to avoid one big file that gets too long and unmanageable.</p>

```
php artisan make:provider HelperServiceProvider
```

Within the `register` method I added this snippet

```php
public function register()
{
    foreach (glob(app_path().'/Helpers/*.php') as $filename){
        require_once($filename);
    }
}
```

lastly `register` the service provider in your `config/app.php` in the providers array

```php
'providers' => [
    'App\Providers\HelperServiceProvider',
]
```

now any file in your `Helpers` directory is loaded, and ready for use.

```
- __Helper (GlobalHelper.php)__

`Helper` completely justifies its name. Any additional operation other than `CRUD` operation can be written in `helper`. Just create a directory as __`App\Helpers\Helper.php`__ and write your code inside it. For example as the code given below,

```php
<?php
use Illuminate\Support\Facades\DB;

if (!function_exists('user_counts'))
{
    function user_counts()
    {
        return DB::table('users')->count();
    }
}
```
