# Laravel Docker

## Usage
* Remove `/project` from `.gitignore`
* Setup `DB_HOST=mysql` in `.env`
 
```bash
$ docker-compose -p <projectname> up -d

$ docker-compose run --rm composer create-project --prefer-dist laravel/laravel ./

$ docker-compose run --rm composer install
$ docker-compose run --rm artisan migrate
$ docker-compose run --rm npm install

$ docker-compose exec php-72-fpm sh
```

# Check URL in browser
* [http://localhost:8080](http://localhost:8080)

### TODO
* [ ] Fix `chmod`

### How to set PhpStorm
* Open settings: `File\Settings` <OR> `Ctrl` + `Alt` + `S`
* Set PHP interpreter 
    * `Languages and Frameworks\PHP`
    *  CLI Interpreter: `[...]`
    * `[+]`, `From Docker...`, `Docker` or `Docker compose`
    * Path mappings: `<Project root>→/opt/project`
* Set PHPUnit 
    * `Languages and Frameworks\PHP\Test Frameworks`
    * `[+]`, `PHPUnit by Remote...`
    * Path to script: `/opt/project/project/vendor/autoload.php`
    * Default configuration file: `/opt/project/project/phpunit.xml`
