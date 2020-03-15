# Ruby version

* `2.7.0`

# System dependencies

* docker

# Configuration

* See `docker-compose.yml`

# Database creation

* command

    ``` shell
    $ docker-compose exec app rails db:create
    ```

# Database initialization

* command

    ``` shell
    $ docker-compose exec app rails db:migrate
    ```

# How to run the test suite

* [WIP]command

    ``` shell
    $ docker-compose exec app rspec spec/
    ```

# Services (job queues, cache servers, search engines, etc.)

* redis
* MySQL

# Deployment instructions

* [WIP]command

    ``` shell
    $ export RAILS_MASTER_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    $ 
    $ docker build \
        --build-arg RAILS_MASTER_KEY="${RAILS_MASTER_KEY}" \
        --no-cache \
        --tag ${any_tag} \
        --target prod_mode \
        --file containers/app/Dockerfile \
        .
    $ 
    $ # docker push .......
    ```
