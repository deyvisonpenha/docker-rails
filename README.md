# Docker-rails
This tutorial explain how to implement ruby on rails using docker
### I - Instalation and Configuration of your development environment 
First is necessary to install docker and docker-composer, to do that check the tutorial given by docker site:

https://docs.docker.com/install/linux/docker-ce/ubuntu/

*Manage Docker as a non-root user
1.Create the `docker` group.

    $ sudo groupadd docker

2.Add your `user` to the `docker` group.

    $ sudo usermod -aG docker $USER
    
3.Log out and log back in so that your group membership is re-evaluated.

4.(optional) Verify that you can run `docker` commands without `sudo`.

    $ docker run hello-world
    
*Install Compose on Linux systems

1.Run this command to download the current stable release of Docker Compose:

    $ sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

2.Apply executable permissions to the binary:

    $ sudo chmod +x /usr/local/bin/docker-compose

### II - Ruby on rails Project
In this step is necessary to create some files as Dockerfile that prepare the image of ruby ​​and other stuff necessary to implement ruby ​​on rails application. So when you clone this repository pay attention on version of ruby, in Docker file, and rails in Gemfile. Don't forget to create the `.env` file that have something like that

    REDIS_URL=redis://redis:6379/0
    COMPOSE_PROJECT_NAME=my_dockerized_app

Because we're using docker image for Redis is necessary to code in this way but if you have already installed in your computer change it to `'redis://localhost:6379/0'`. COMPOSE_PROJECT_NAME is for personalise the name of images and containers that will be created.

After this steps we can running the script bellow that will create yours rails project. Let's explain what is happen here. `myapp` is the name of Service that have in `docker-compose`, after that is pure Rails code to create projects. 

    $ docker-compose run myapp rails new . --force --no-deps --database=postgresql

When the project is created by Docker the owner of all files is `root` so is necessary to change for yours user, to do that write in terminal console. If you get message error as `Permission Denied` try this comand

    $ sudo chown -R $USER:$USER .

Modify the `database.yml` in `/config/database.yml` to some like that

    default: &default
    adapter: postgresql
    encoding: unicode
    host: db
    username: postgres
    password:
    pool: 5

    development:
     <<: *default
    database: myapp_development


    test:
    <<: *default
    database: myapp_test

And add two gems in yours `Gemfile`

    gem 'redis'
    gem 'sidekiq'
    

And install `gem` in the new `Gemfile` which was create with `rails new`

    docker-compose run myapp bundle

quase finalizando, vamos agora rodar o codigo para levantar os serviços 

    docker-compose up

In a new terminal 
    
    docker-compose run myapp rails db:create


### TIPS
To sincronize Redis with Sidekiq using a docker-compose is necessary to have a .env file, and put this code:
  REDIS_URL=redis://redis:6379/0
 
 
 https://docs.docker.com/install/linux/docker-ce/ubuntu/
 
 https://docs.docker.com/compose/rails/
 
 https://onebitcode.com/dominando-o-uso-de-jobs-no-rails/
