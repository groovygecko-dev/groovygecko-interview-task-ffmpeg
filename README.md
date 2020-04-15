# Groovy Gecko Developer role interview task

## PHP with FFMPEG

### Installation steps

#### Docker

Install Docker https://docs.docker.com/get-docker/

note: if you are using Linux, you need to additionally install docker-compose


Run the following in a command shell (make sure you have navigated to the project directory)

1. Run `docker-compose build` to create the docker images for NGINX and PHP (7.4 fpm)
2. Run `docker-compose up -d` to run docker in detached mode

Once this is complete, you will be able to open http://localhost:8081 in your browser and see the output of `./public/index.php`

note: If you are using port 8081 for another project, you can change this by editing line 12 `docker-compose.yml` and then executing `docker-compose up -d` to load the changes.

To stop the project, run `docker-compose down`

#### Composer

To install PHP dependencies using composer, you need to have `docker-compose up -d` running.

`composer` is run inside the PHP docker container. `composer install` and can be run with `docker-compose exec phpfpm composer install`.
