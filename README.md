### Prerequisite

1. `sudo apt-get update`

2. `sudo apt-get install ca-certificates curl gnupg lsb-release`

### Install using the convenience script (For Raspi this is the way) 

In future, maybe there will be more better approach.

1. `curl -fsSL https://get.docker.com -o get-docker.sh`

2. You can run the script with the DRY_RUN=1 option to learn what steps the script will execute during installation: `DRY_RUN=1 sh ./get-docker.sh`

3. If step 3 went good, run `sudo sh get-docker.sh`. This will downloads the script from [docker](get.docker.com) and runs it to install the latest stable release of Docker on Linux.

4. for using Docker as a non-privileged user `sudo usermod -a -G docker <raspberry_pi_username>`

5. Check docker version `docker --version`

6. Check if docker is running `sudo systemctl status docker.service`

7. For installing docker compose `sudo apt-get install docker-compose-plugin`

8 If some erro with dpkg try `sudo apt-get install -f` and `sudo reboot`

### Configure Docker to start in boot

1. To enable `sudo systemctl enable docker.service` and `sudo systemctl enable containerd.service`

2. To disable `sudo systemctl disable docker.service` and `sudo systemctl disable containerd.service`


### Portainer Installation

POrtainer provides gui presentation for containers running in the raspberry pi

1. First, create the volume that Portainer Server will use to store its database `docker volume create portainer_data`

2. Download and install the Portainer Server container: `docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest`

3. (opt) Use the docker-compose.yaml file to run the portainer server `docker compose up `

3. Check to see whether the Portainer Server container has started by running `docker ps`

4. Open the web browser and login at `https://localhost:9443`

### Reference Link
1. [Official Docker Documentation For Installation](https://docs.docker.com/engine/install/debian/#install-using-the-convenience-script)

2. [Post-installation steps for Linux](https://docs.docker.com/engine/install/linux-postinstall/)

3. [Configure Docker to start in boot](https://docs.docker.com/engine/install/linux-postinstall/#configure-docker-to-start-on-boot)

4 [Portainer Installation](https://docs.portainer.io/start/install/server/docker/linux)

