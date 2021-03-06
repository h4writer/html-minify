# Laravel 5 HTML Minify
This package is originally from https://github.com/fitztrev/laravel-html-minify i just updated the package and made it compatible with laravel 5.

## About

This package compresses the HTML output from your Laravel 5 application, seamlessly reducing the overall response size of your pages.

Other scripts that I've seen will compress the HTML output on-the-fly for each request. Instead, this package extends the Blade compiler to save the compiled template files to disk in their compressed state, reducing the overhead for each request.

## Why?

Even with gzip enabled, there is still an improvement in the response size for HTML content-type documents.

Test Page | w/o Gzip | w/ Gzip | w/ Gzip + Laravel HTML Minify
--- | ---: | ---: | :---:
**#1** | 8,039 bytes | 1,944 bytes | **1,836 bytes** (5.6% improvement)
**#2** | 377,867 bytes | 5,247 bytes | **4,314 bytes** (17.8% improvement)

## Installation

1. Add `"yocmen/html-minify": "2.*"` to **composer.json**.
2. Run `composer update`
3. Add `Yocmen\HtmlMinify\HtmlMinifyServiceProvider` to the list of providers in **config/app.php**.
4. Publish your config with `php artisan vendor:publish` command
5. **Important:** You won't see any changes until you edit your `*.blade.php` template files. Once Laravel detects a change, it will recompile them, which is when this package will go to work. To force all views to be recompiled, just run this command: `find . -name "*.blade.php" -exec touch {} \;`


### Options

- **`enabled`** - *boolean*, default **true**

If you are using a javascript framework that conflicts with Blade's tags, you can change them.

- **`blade.rawTags`** - *array*, default `{!!` and `!!}`
- **`blade.contentTags`** - *array*, default `{{` and `}}`
- **`blade.escapedContentTags`** - *array*, default `{{{` and `}}}`

#### Skipping minification

To prevent the minification of a view file, add `skipmin` somewhere in the view.

```
{{-- skipmin --}}
<!-- skipmin -->
```