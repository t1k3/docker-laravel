# Laravel Docker

## Usage
* Copy `.env.example` to `.env` and update
* Remove `/src` from `.gitignore`
* Delete or update `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, `DB_PASSWORD` in `src/.env`

```bash
$ cp .env.example .env
$ docker-compose -p <projectname> up -d

$ docker-compose -p <projectname> run --rm composer create-project --prefer-dist laravel/laravel ./

$ docker-compose -p <projectname> run --rm composer install
$ docker-compose -p <projectname> run --rm npm install
$ docker-compose -p <projectname> exec -T php-fpm php artisan key:generate

$ docker-compose -p <projectname> exec php sh
```

# Check URL in browser
* [http://localhost:8001](http://localhost:8001)

### TODO
* [ ] Add [queues](https://laravel.com/docs/5.6/queues)
* [ ] Fix docker-host permission: [userns-remap](https://docs.docker.com/engine/security/userns-remap/)
* [ ] Update project with swarm: secrets, configs
