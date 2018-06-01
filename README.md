# Laravel Docker

## Usage
* Remove `/project` from `.gitignore`
* Setup `DB_HOST=mysql` in `.env`
* Setup (or delete) `DB_PASSWORD=<password>` in `.env` from `docker-compose.yml #mysql:MYSQL_PASSWORD`
 
```bash
$ docker-compose -p <projectname> up -d

$ docker-compose -p <projectname> run --rm composer create-project --prefer-dist laravel/laravel ./

$ docker-compose -p <projectname> run --rm composer install
$ docker-compose -p <projectname> run --rm npm install
$ docker-compose -p <projectname> exec -T php-72-fpm php artisan key:generate

$ docker-compose -p <projectname> exec php-72-fpm sh
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
