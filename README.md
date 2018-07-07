# Laravel Deployment Shared Hosting
Laravel Deployment Shared Hosting with or without SSH

## Without SSH
### Laravel 5.5

1. Compress your Laravel Project and upload it to Root of your Shared Hosting
2. Extract your project to root of your Shared Hosting
3. Move all files in your `public` to `public_html` folder
4. open `server.php` in root of your server (Included in Laravel Project)
5. rename `public` folder to `public_html`

before
```
if ($uri !== '/' && file_exists(__DIR__.'/public'.$uri)) {
    return false;
}

require_once __DIR__.'/public/index.php';
```
after 
```
if ($uri !== '/' && file_exists(__DIR__.'/public_html'.$uri)) {
    return false;
}

require_once __DIR__.'/public_html/index.php';
```

6. Open `app\Providers\AppServiceProvider.php` and add this following code into `public function register()`

```
// override path.public
$this->app->bind('path.public',function(){
    return base_path('public_html');
});
```

## SSH Supported
### Laravel 5.5

1. Do the following instruction on 'Without SSH'
2. Make sure your `.env` was configured
3. Force `composer` to update
```
composer install
```
3. Generate new key , then execute 
```
php artisan key:generate
```
4. You Supposed to have no problem use your `artisan` and `composer` command

#### if you had git supported project 
You could init your git in root of Shared Hosting and add this following `.gitignore` to prevent unnecessary file push to your git repository

[grab your .gitignore here](https://github.com/wendyliga/laravel-deployment-shared-hosting/blob/master/gitignore_ssh.md)

# Next Steps
Happy Code Guys

# Feedback
Please don't hesitate for [issuing](https://github.com/wendyliga/laravel-deployment-shared-hosting/issues) something that doesn't work for you, I will really happy to help you
