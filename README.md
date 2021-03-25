# Laravel Docker

## Usage
* Copy `.env.example` to `.env` and update
* Remove `/src` from `.gitignore`
* Delete or update `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, `DB_PASSWORD` in `src/.env`

```bash
$ cp .env.example .env
$ docker-compose up -d

$ docker-compose run --rm composer create-project --prefer-dist laravel/laravel ./

$ docker-compose run --rm composer install
$ docker-compose run --rm npm install
$ docker-compose exec -T php-fpm php artisan key:generate

$ docker-compose exec php-fpm sh
```

# Check URL in browser
* [http://localhost:8001](http://localhost:8001)

### TODO
* [ ] Add swarm configuration: docker-stack.yml
* [ ] Remove supervisor: [The Twelve Factors](https://12factor.net/)
  * [ ] Cron Service
  * [ ] Migration Service
  * [ ] [Queue worker](https://laravel.com/docs/8.x/queues)
* [ ] Separate (named) volumes
* [ ] Separate .env files
* [ ] Add [Traefik](https://doc.traefik.io/traefik/) labels
* [ ] Add [multistage dockerfile](https://docs.docker.com/develop/develop-images/multistage-build/)
* [ ] Makefile / Ansible
