Installation
============

## Via Composer (create-project)

You can use the `create-project` command from [Composer](http://getcomposer.org/)
to create the project in one go:

```console
$ composer create-project laminas-api-tools/api-tools-skeleton path/to/install
```

## Via Git (clone)

First, clone the repository:

```console
$ git clone https://github.com/laminas-api-tools/api-tools-skeleton.git # optionally, specify the directory in which to clone
$ cd path/to/install
```

At this point, you need to use [Composer](https://getcomposer.org/) to install
dependencies. Assuming you already have Composer:

```console
$ composer install
```

## All methods

> ### PHP 7.1+ users
>
> If you are on PHP 7.1 or greater, you will want to prepare your skeleton to
> use the latest versions of dependencies, as several dependencies have new
> major releases that can make use of the newer PHP versions. To do this,
> execute the following within your project root:
>
> ```console
> $ rm composer.lock && rm -rf vendor
> $ composer install
> ```
>
> and answer any prompts as they occur.

Once you have the basic installation, you need to put it in development mode:

```console
$ cd path/to/install
$ composer development-enable # put the skeleton in development mode
```

Now, fire it up! Do one of the following:

- Create a vhost in your web server that points the DocumentRoot to the
  `public/` directory of the project (hardest!).
- Use the built-in vagrant configuration: `vagrant up`.
- Use the built-in docker-compose configuration: `docker-compose up`.
- Fire up the built-in web server in PHP (**note**: do not use this for
  production!)

In the latter case, do the following:

```console
cd path/to/install
php -S 0.0.0.0:8080 -ddisplay_errors=0 -t public public/index.php
```

You can then visit the site at http://localhost:8080/ - which will bring up a
welcome page and the ability to visit the dashboard in order to create and
inspect your APIs.

> ### NOTE ABOUT OPCACHE
> 
> **Disable all opcode caches when running the admin!**
> 
> The admin cannot and will not run correctly when an opcode cache, such as APC or
> OpCache, is enabled. API Tools does not use a database to store configuration;
> instead, it uses PHP configuration files. Opcode caches will cache these files
> on first load, leading to inconsistencies as you write to them, and will
> typically lead to a state where the admin API and code become unusable.
> 
> The admin is a **development** tool, and intended for use a development
> environment. As such, you should likely disable opcode caching, regardless.
> 
> When you are ready to deploy your API to **production**, however, you can
> disable development mode, thus disabling the admin interface, and safely run an
> opcode cache again. Doing so is recommended for production due to the tremendous
> performance benefits opcode caches provide.

> ### NOTE ABOUT DISPLAY_ERRORS
> 
> The `display_errors` `php.ini` setting is useful in development to understand what warnings,
> notices, and error conditions are affecting your application. However, they cause problems for APIs:
> APIs are typically a specific serialization format, and error reporting is usually in either plain
> text, or, with extensions like XDebug, in HTML. This breaks the response payload, making it unusable
> by clients.
> 
> For this reason, we recommend disabling `display_errors` when using the API Tools admin interface.
> This can be done using the `-ddisplay_errors=0` flag when using the built-in PHP web server, or you
> can set it in your virtual host or server definition. If you disable it, make sure you have
> reasonable error log settings in place. For the built-in PHP web server, errors will be reported in
> the console itself; otherwise, ensure you have an error log file specified in your configuration.
> 
> `display_errors` should *never* be enabled in production, regardless.
