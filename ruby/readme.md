# README

Revive Solidus app

## Provisioning

You need `docker` and `docker-compose` installed (for MacOS just use [official app](https://docs.docker.com/engine/installation/mac/)).

### Dip
Using [dip–CLI](https://github.com/bibendi/dip) utility for straightforward provisioning and interacting with an applications configured by docker-compose.

To install dip copy and run the command below:

```
$ gem install dip
```

more installation options are found here: https://github.com/bibendi/dip#installation

Then use the following commands:

```
# provision application (this will take a while)
dip provision

# run web app with all debuging capabilities (i.e. `binding.pry`)
dip rails s

# run rails console
dip rails c

# run webpacker dev server
dip up -d webpacker
# `-d` - mean that service will run in detached (background) mode
```

### Docker

Run the following commands to prepare your Docker dev env:

```sh
$ docker-compose build
$ docker-compose run runner yarn install
$ docker-compose run runner ./bin/setup
```

It builds the Docker image, installs Ruby and NodeJS dependencies, creates database, run migrations and seeds.

You're all set! Now you're ready to code!

#### Commands

- Running the app:

You can run the Rails up using the following command:

```sh
$ docker-compose up rails
```

If you want to run Webpack Dev server as well:

```sh
$ docker-compose up rails webpacker
```
