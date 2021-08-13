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

