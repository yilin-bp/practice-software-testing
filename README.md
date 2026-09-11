[![Run Playwright Tests 🎭](https://github.com/testsmith-io/practice-software-testing/actions/workflows/run-tests.yml/badge.svg)](https://github.com/testsmith-io/practice-software-testing/actions/workflows/run-tests.yml) [![StackShare](http://img.shields.io/badge/tech-stack-0690fa.svg?style=flat)](https://stackshare.io/testsmith-io/practice-software-testing)


# Default accounts

| First name | Last name | Role   | E-mail                                | Password   |
|------------|-----------|--------|---------------------------------------|------------|
| John       | Doe       | admin  | admin@practicesoftwaretesting.com     | welcome01  |
| Jane       | Doe       | user   | customer@practicesoftwaretesting.com  | welcome01  |
| Jack       | Howe      | user   | customer2@practicesoftwaretesting.com | welcome01  |
| Bob        | Smith     | user   | customer3@practicesoftwaretesting.com | pass123    |

# URLs (hosted versions)

| Description           | Application                                                                                     | API                                                                                                            | Swagger                                                                                                                   |
|-----------------------|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Sprint 1              | [https://v1.practicesoftwaretesting.com](https://v1.practicesoftwaretesting.com)                | [https://api-v1.practicesoftwaretesting.com](https://api-v1.practicesoftwaretesting.com/status)                | [https://api-v1.practicesoftwaretesting.com](https://api-v1.practicesoftwaretesting.com/api/documentation)                |
| Sprint 2              | [https://v2.practicesoftwaretesting.com](https://v2.practicesoftwaretesting.com)                | [https://api-v2.practicesoftwaretesting.com](https://api-v2.practicesoftwaretesting.com/status)                | [https://api-v2.practicesoftwaretesting.com](https://api-v2.practicesoftwaretesting.com/api/documentation)                |
| Sprint 3              | [https://v3.practicesoftwaretesting.com](https://v3.practicesoftwaretesting.com)                | [https://api-v3.practicesoftwaretesting.com](https://api-v3.practicesoftwaretesting.com/status)                | [https://api-v3.practicesoftwaretesting.com](https://api-v3.practicesoftwaretesting.com/api/documentation)                |
| Sprint 4              | [https://v4.practicesoftwaretesting.com](https://v4.practicesoftwaretesting.com)                | [https://api-v4.practicesoftwaretesting.com](https://api-v4.practicesoftwaretesting.com/status)                | [https://api-v4.practicesoftwaretesting.com](https://api-v4.practicesoftwaretesting.com/api/documentation)                |
| Sprint 5              | [https://practicesoftwaretesting.com](https://practicesoftwaretesting.com)                      | [https://api.practicesoftwaretesting.com](https://api.practicesoftwaretesting.com/status)                      | [https://api.practicesoftwaretesting.com](https://api.practicesoftwaretesting.com/api/documentation)                      |
| Sprint 5 (with bugs)  | [https://with-bugs.practicesoftwaretesting.com](https://with-bugs.practicesoftwaretesting.com)  | [https://api-with-bugs.practicesoftwaretesting.com](https://api-with-bugs.practicesoftwaretesting.com/status)  | [https://api-with-bugs.practicesoftwaretesting.com](https://api-with-bugs.practicesoftwaretesting.com/api/documentation)  |
| Sprint 5 (holtesting) | [https://holtesting.practicesoftwaretesting.com](https://with-bugs.practicesoftwaretesting.com) | [https://api-holtesting.practicesoftwaretesting.com](https://api-with-bugs.practicesoftwaretesting.com/status) | [https://api-holtesting.practicesoftwaretesting.com](https://api-with-bugs.practicesoftwaretesting.com/api/documentation) |

## Mobile App

The mobile app is fully integrated with version 4 of Practice Software Testing, which means both share the same environment. Any changes you make through the mobile app (like creating or editing data) will appear on the website, and updates on the website will also show up in the app.

[Android Mobile APK](https://testsmith.ams3.cdn.digitaloceanspaces.com/artifacts/practice-software-testing.apk)

[iOS Simulator App](https://testsmith.ams3.cdn.digitaloceanspaces.com/artifacts/practice-software-testing.zip)

# Using the docker containers

I will take up to 5 minutes (depending on your internet connection speed), if you run `docker compose up -d` for the first
time. Any subsequent `docker compose up -d` will take seconds. You may need to add sudo before the docker command `sudo docker compose up -d`

All images together are less than 1,5 GB.

## 🐳 Docker Compose Setup

This project includes multiple Docker Compose configurations to support development, testing, and production usage.

### 🔧 Local Development (with live-reloading, source-mounted volumes)

Use this when actively working on the application:

```bash
docker compose up -d
```

This will:

* Build the containers from local source (`docker-compose.yml`)
* Mount the source code for live changes
* Automatically include `docker-compose.override.yml` (mailcatcher, cron, phpmyadmin)

### 🧪 Development + Excluding Optional Services

To start the bare minimum:

```bash
docker compose -f docker-compose.yml up -d
```
This will:

* Use only what's defined in docker-compose.yml
* Ignore docker-compose.override.yml completely
* Skip optional services like cron, phpmyadmin, mailcatcher


### 🚀 Production Setup (with prebuilt Docker images)

```bash
docker compose -f docker-compose.prod.yml up --pull missing -d
```

## URL's (local version)

| URL                                                                                | Description           |
|------------------------------------------------------------------------------------|-----------------------|
| [http://localhost:8091](http://localhost:8091)                                     | (REST) API            |
| [http://localhost:8091/api/documentation](http://localhost:8091/api/documentation) | Swagger               |
| [http://localhost:1080](http://localhost:1080)                                     | MailCatcher           |
| [http://localhost:4200](http://localhost:4200)                                     | (Angular) Application |
| [http://localhost:8000](http://localhost:8000) (`root`/`root`)                     | PHPMyAdmin            |

## Switch sprint

Update the `SPRINT` in [.env](.env) to use the proper version that belongs to the sprint.

## Sprint 5 quick restart (dev stack)

Use this if you want to close everything and start again quickly.

### Fast start

1. Ensure sprint5 is selected in `.env`:

```bash
SPRINT=sprint5
```

2. Start the local development stack:

```bash
docker compose up -d
```

3. Verify the main services:

```bash
curl -i http://localhost:8091/status
curl -i "http://localhost:8091/products?page=1"
```

4. Open the app:

```text
http://localhost:4200
```

Expected:

* Product cards are visible on the home page.
* API status returns JSON with version/environment.

### Is this live-reload dev mode?

Yes.

* UI code is source-mounted from `./${SPRINT}/UI` and served with `ng serve`.
* API code is source-mounted from `./${SPRINT}/API`.
* Frontend changes should appear automatically in the browser.

### Troubleshooting (problems we hit and fixes)

#### Problem: UI starts but product cards do not load

Symptoms:

* Empty/skeleton cards.
* Browser console shows failed requests.

Fix sequence:

1. Check API health:

```bash
curl -i http://localhost:8091/status
curl -i "http://localhost:8091/products?page=1"
```

2. If responses contain a PHP fatal error about `vendor/autoload.php` missing, install API dependencies:

```bash
docker compose run --rm --entrypoint sh composer -lc "composer config --global process-timeout 1800; composer install --no-dev --optimize-autoloader --ignore-platform-req=ext-ffi --no-interaction"
```

3. If `/products` returns an error because tables are missing, apply schema and seed data:

```bash
docker compose exec laravel-api php artisan migrate --force
docker compose exec laravel-api php artisan db:seed --force
```

4. Reload `http://localhost:4200`.

#### Problem: CORS errors in browser console

Checks:

```bash
curl -i -X OPTIONS -H "Origin: http://localhost:4200" -H "Access-Control-Request-Method: GET" http://localhost:8091/products
```

Expected headers include `Access-Control-Allow-Origin`.

Note:

* We observed CORS-like browser failures while the API was fatally broken.
* Once Composer dependencies and DB were fixed, the endpoints returned correct CORS headers.

#### Problem: startup is slow

Notes:

* First startup can still take a while due to image pulls and the initial `npm install` in the UI container.
* Subsequent UI starts are faster because `node_modules` is cached in a named Docker volume and `npm install` is only rerun when needed.

Avoid this if you want faster restarts:

```bash
docker compose down -v
```

This removes volumes and may force expensive reinstall/reseed work next time.

### Copilot prompt for quick setup/recovery

Use this prompt in GitHub Copilot Chat:

```text
In this repository, bring up sprint5 local development quickly.
1) Verify .env uses SPRINT=sprint5.
2) Run docker compose up -d.
3) Verify http://localhost:4200 and http://localhost:8091/status.
4) If API shows vendor/autoload.php missing, run:
	docker compose run --rm --entrypoint sh composer -lc "composer config --global process-timeout 1800; composer install --no-dev --optimize-autoloader --ignore-platform-req=ext-ffi --no-interaction"
5) If products fail due to missing tables/data, run:
	docker compose exec laravel-api php artisan migrate --force
	docker compose exec laravel-api php artisan db:seed --force
6) Re-verify products endpoint and confirm the home page product cards are visible.
7) Report final status and any remaining blockers.
```

## Roll Back - Run Migrations - Seed Database

`docker exec -it pst-laravel-api-1 php artisan migrate:fresh --seed`

## Migrate database schema

`docker exec -it pst-laravel-api-1 php artisan migrate`

## Seed database

`docker exec -it pst-laravel-api-1 php artisan db:seed`

## Access to the Laravel Logs

`docker exec -it pst-laravel-api-1 tail -f storage/logs/laravel.log`

## Generate Swagger documentation

`docker exec -it pst-laravel-api-1 php artisan l5-swagger:generate`

## Update order status

`docker exec -it pst-laravel-api-1 php artisan order:update`

## Remove PDF documents

`docker exec -it pst-laravel-api-1 php artisan invoice:remove`

## Generate PDF documents

`docker exec -it pst-laravel-api-1 php artisan invoice:generate`

## Execute unit tests (sprint 1 to sprint 4)

`./vendor/bin/phpunit`

## Execute unit tests (sprint 5)

`./vendor/bin/pest`

## Execute unit tests with coverage

`XDEBUG_MODE=coverage ./vendor/bin/phpunit --coverage-html tests/coverage`

## Start pact-mock-service

`pact-mock-service start --host localhost --port 7203 --consumer AnyConsumer --provider ProductAPI --pact-dir ./pacts --log ./storage/logs/pact.log`

## Stop pact-mock-service

`pact-mock-service stop --port 7203`

# Sprints

## Sprint 0

During this initial sprint, we made some architectural decisions. We decided to implement a
super-fast [Laravel](https://laravel.com/) API, as well as an [Angular](https://angular.io/) frontend.

Every developer or tester can spin up the environment on its own machine. This makes testing easier, and it
allows you to manipulate data.

The deliverable of Sprint0 is a Dockerized environment, just like database seeding scripts. Basically, the result is
an empty environment.

# Support This Project

If you find this project useful and want to support its ongoing development, please consider [supporting](https://testwithroy.com/b/support) it!

I appreciate your support!

# License

This repository is publicly viewable for reference purposes only.

Commercial use, public hosting, redistribution, and use for third-party services are not allowed without prior written permission. See [LICENSE](LICENSE) for details.
