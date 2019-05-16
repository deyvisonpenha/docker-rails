# Docker-rails
This tutorial explain how to implement ruby on rails using docker
### I - Instalation 
First is necessary to install docker and docker-composer, to do that check the tutorial given by docker site:

https://docs.docker.com/install/linux/docker-ce/ubuntu/

*Manage Docker as a non-root user
1.Create the `docker` group.

    $ sudo groupadd docker

2.Add your `user` to the `docker` group.

    $ sudo usermod -aG docker $USER
    
3.Log out and log back in so that your group membership is re-evaluated.

4.Verify that you can run `docker` commands without `sudo`.

    $ docker run hello-world
    
*Install Compose on Linux systems

1.Run this command to download the current stable release of Docker Compose:

    $ sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

2.Apply executable permissions to the binary:

    $ sudo chmod +x /usr/local/bin/docker-compose

### II - Ruby on rails Project
In this step is necessary to create some files as Dockerfile that prepare the image of ruby ​​and other stuff necessary to implement ruby ​​on rails application. So when you clone this repository pay attention on version of ruby, in Docker file, and rails in Gemfile

### TIPS
To sincronize Redis with Sidekiq using a docker-compose is necessary to have a .env file, and put this code:
  REDIS_URL=redis://redis:6379/0
 
