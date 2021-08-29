# jupyterlab development environment with docker
## Install Docker
1. Follow the instructions in this link: [https://docs.docker.com/engine/install/ubuntu/]

2. Do the post install options:
Link for more information: [https://docs.docker.com/engine/install/linux-postinstall/]
Add group with the name docker to the system.
```sh
sudo groupadd docker
```

add your user to the docker group
```sh
sudo usermod -aG docker $USER
```

reboot the machine
```sh
reboot
```

Try out if it works, command should work without sudo
```sh
docker run hello-world
```

3. Configure docker to start on boot.
```sh
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

## Install Docker-compose
1. Follow the instructions in this link: [https://docs.docker.com/compose/install/]

See if it is correctly installed
```sh
docker-compose --version
```

## Create docker-compose file for jupyter-lab
change out mimslade to your user.
First path in volumes is the path on your host computer you want to stor notebooks.
second path in volumes is the path on the docker container.
1. Create file named: docker-compose.yml
```yml
version: "3"
services:
    datascience-notebook:
        restart: 'always'
        image: 'jupyter/datascience-notebook'
        volumes:
            - '/home/mimslade/dev:/home/mimslade/dev'
        ports:
            - '8888:8888'
        command: "start-notebook.sh"
        container_name: 'dnc'
        user: 'root'
        environment:
            NB_USER: 'mimslade'
            NB_UID: 1000
            NB_GID: 1000
            CHOWN_HOME: 'yes'
            CHOWN_HOME_OPTS: '-R'
            GRANT_SUDO: 'yes'
            JUPYTER_ENABLE_LAB: 'yes'


```

2. suggested path to store yml file
```sh
/home/mimslade/dev/docker/docker-compose/jupyter-lab/docker-compose.yml
```

3. Try out if the docker-compose file is working
```sh
cd /home/mimslade/dev/docker/docker-compose/jupyter-lab
```
```sh
docker-compose up
```

4. run it in detached mode
```sh
docker-compose up -d
```

