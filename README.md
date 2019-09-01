# Rails 6 Docker Alpine
Docker image size

```sh
$ docker images
REPOSITORY                                 TAG                       SIZE
blitz_web                                  latest                    390MB

```

### Steps

1. Clone & Create

```sh
git clone git@github.com:zazk/Rails-6-Docker-Alpine.git
```

Create a new Rails application under the repository directory

```sh
cd Rails-6-Docker-Alpine
rails new . --webpack --database=postgresql
```

2. Configure:

Modify your database configuration to use the postgresql container configuration:

```yaml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  host: db
  username: postgres
```

Remove check Yarn

```yaml
# ./config/environments/development.rb
# Disable Yarn Check
config.webpacker.check_yarn_integrity = false
```

3. Build the project:

```sh
docker-compose build
```

4. Create the database and run the migrations:

```sh
docker-compose run --rm web bin/rails db:create
docker-compose run --rm web bin/rails db:migrate
```

5. Run the app:

```sh
docker-compose up
```

Visit your application

```
http://localhost:3000
```

### Troubleshooting

1. If you have probles with `pg` gem you should install Postgres before. On Mac `brew install postgres`
2. Ruby Version `2.5.3`
