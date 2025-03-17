## Basic Docker Commands

### Check Docker Version
```bash
docker --version
```
*Example: Running this may output: "Docker version 20.10.12, build e91ed57".*

### Display System-Wide Information
```bash
docker info
```
*Example: Displays details such as the number of containers, images, storage driver, etc.*

### Run a Container
```bash
docker run <image_name>
```
*Example: `docker run hello-world`*

### Run a Container in Interactive Mode
```bash
docker run -it <image_name> /bin/bash
```
*Example: `docker run -it ubuntu /bin/bash`*

### Run a Container in Detached Mode
```bash
docker run -d <image_name>
```
*Example: `docker run -d nginx`*

### List Running Containers
```bash
docker ps
```
*Example: `docker ps` shows all currently running containers.*

### List All Containers (Running and Stopped)
```bash
docker ps -a
```
*Example: `docker ps -a` lists every container regardless of status.*

### Stop a Container
```bash
docker stop <container_id_or_name>
```
*Example: `docker stop my_container` stops the container named "my_container".*

### Start a Stopped Container
```bash
docker start <container_id_or_name>
```
*Example: `docker start my_container` restarts a stopped container.*

### Restart a Container
```bash
docker restart <container_id_or_name>
```
*Example: `docker restart my_container`*

### Remove a Container
```bash
docker rm <container_id_or_name>
```
*Example: `docker rm my_container` deletes the container named "my_container".*

### Force Remove a Running Container
```bash
docker rm -f <container_id_or_name>
```
*Example: `docker rm -f my_container` forcefully removes a running container.*

### Run a Container with Port Mapping
```bash
docker run -p 8080:80 <image_name>
```
*Example: `docker run -p 8080:80 nginx` maps host port 8080 to container port 80.*

### Run a Container with Environment Variables
```bash
docker run -e MY_VAR=value <image_name>
```
*Example: `docker run -e MY_VAR=hello ubuntu` sets the environment variable MY_VAR to "hello".*

### Run a Container with a Volume Mounted
```bash
docker run -v /host/path:/container/path <image_name>
```
*Example: `docker run -v /tmp/data:/data ubuntu` mounts the host directory `/tmp/data` into the container’s `/data` folder.*

### Run a Container with a Custom Name
```bash
docker run --name my_container <image_name>
```
*Example: `docker run --name my_custom_container nginx` names the container "my_custom_container".*

### Run a Container and Automatically Remove It After Exit
```bash
docker run --rm <image_name>
```
*Example: `docker run --rm hello-world` removes the container automatically when it exits.*

## Image Management

### List Images
```bash
docker images
```
*Example: `docker images` lists all images stored locally.*

### Pull an Image from Docker Hub
```bash
docker pull <image_name>
```
*Example: `docker pull ubuntu` downloads the latest Ubuntu image.*

### Remove an Image
```bash
docker rmi <image_id_or_name>
```
*Example: `docker rmi ubuntu` removes the Ubuntu image from your system.*

### Build an Image from a Dockerfile
```bash
docker build -t <image_name> .
```
*Example: `docker build -t myapp .` builds an image named "myapp" from the Dockerfile in the current directory.*

### Tag an Image
```bash
docker tag <image_id> <new_image_name>:<tag>
```
*Example: `docker tag 123abc myrepo/myapp:latest` tags an image with a new name and tag.*

### Push an Image to Docker Hub
```bash
docker push <image_name>
```
*Example: `docker push myrepo/myapp:latest` uploads the image to Docker Hub.*

### Search Docker Hub for Images
```bash
docker search ubuntu
```
*Example: `docker search ubuntu` returns a list of Ubuntu-related images.*

### Build an Image Without Using Cache
```bash
docker build --no-cache -t <image_name> .
```
*Example: `docker build --no-cache -t myapp .` rebuilds the image without using any cached layers.*

## Container Logs and Monitoring

### View Container Logs
```bash
docker logs <container_id_or_name>
```
*Example: `docker logs my_container` displays the logs from "my_container".*

### Follow Container Logs in Real-Time
```bash
docker logs -f <container_id_or_name>
```
*Example: `docker logs -f my_container` continuously outputs new log entries.*

### Inspect a Container
```bash
docker inspect <container_id_or_name>
```
*Example: `docker inspect my_container` outputs detailed configuration information.*

### View Resource Usage (Stats)
```bash
docker stats <container_id_or_name>
```
*Example: `docker stats my_container` shows live resource usage such as CPU and memory.*

### Execute a Command in a Running Container
```bash
docker exec -it <container_id_or_name> <command>
```
*Example: `docker exec -it my_container ls /` runs the `ls /` command inside the container.*

## Networking

### List Networks
```bash
docker network ls
```
*Example: `docker network ls` displays all Docker networks.*

### Create a Network
```bash
docker network create <network_name>
```
*Example: `docker network create my_network` creates a new network called "my_network".*

### Connect a Container to a Network
```bash
docker network connect <network_name> <container_id_or_name>
```
*Example: `docker network connect my_network my_container` connects "my_container" to "my_network".*

### Disconnect a Container from a Network
```bash
docker network disconnect <network_name> <container_id_or_name>
```
*Example: `docker network disconnect my_network my_container` disconnects the container from the network.*

### Inspect a Network
```bash
docker network inspect <network_name>
```
*Example: `docker network inspect my_network` shows detailed information about "my_network".*

## Volume Management

### List Volumes
```bash
docker volume ls
```
*Example: `docker volume ls` lists all Docker volumes.*

### Create a Volume
```bash
docker volume create <volume_name>
```
*Example: `docker volume create my_volume` creates a volume named "my_volume".*

### Inspect a Volume
```bash
docker volume inspect <volume_name>
```
*Example: `docker volume inspect my_volume` displays details about "my_volume".*

### Remove a Volume
```bash
docker volume rm <volume_name>
```
*Example: `docker volume rm my_volume` deletes the volume "my_volume".*

### Remove Unused Volumes
```bash
docker volume prune
```
*Example: `docker volume prune` removes all unused volumes.*

## Docker Compose

### Start Services
```bash
docker-compose up
```
*Example: `docker-compose up` starts all services defined in the docker-compose.yml file.*

### Start Services in Detached Mode
```bash
docker-compose up -d
```
*Example: `docker-compose up -d` starts the services in the background.*

### Stop Services
```bash
docker-compose down
```
*Example: `docker-compose down` stops and removes containers, networks, and volumes created by Docker Compose.*

### Rebuild and Restart Services
```bash
docker-compose up --build
```
*Example: `docker-compose up --build` forces a rebuild of images and starts services.*

### View Logs for a Service
```bash
docker-compose logs <service_name>
```
*Example: `docker-compose logs web` shows logs for the "web" service.*

### List Running Services
```bash
docker-compose ps
```
*Example: `docker-compose ps` lists the status of services defined in the Compose file.*

## Miscellaneous

### Prune Unused Objects
```bash
docker system prune
```
*Example: `docker system prune` cleans up stopped containers, networks, and dangling images.*

### Prune Everything (Including Volumes and Images)
```bash
docker system prune -a --volumes
```
*Example: `docker system prune -a --volumes` removes all unused objects, images, and volumes.*

### Copy Files Between Host and Container
```bash
docker cp <file_path> <container_id_or_name>:<container_path>
docker cp <container_id_or_name>:<container_path> <file_path>
```
*Example: `docker cp /host/file.txt my_container:/container/file.txt` and vice versa.*

### Export a Container to a Tar Archive
```bash
docker export <container_id_or_name> > <file_name>.tar
```
*Example: `docker export my_container > my_container_backup.tar` exports the container's filesystem to a tar file.*

### Import a Container from a Tar Archive
```bash
docker import <file_name>.tar <image_name>:<tag>
```
*Example: `docker import my_container_backup.tar myimage:latest` creates an image from a tar archive.*

### Display Docker Disk Usage
```bash
docker system df
```
*Example: `docker system df` shows disk usage for images, containers, and volumes.*

## Advanced Container Management

### Pause a Running Container
```bash
docker pause <container_id_or_name>
```
*Example: `docker pause my_container` pauses the container's processes.*

### Unpause a Paused Container
```bash
docker unpause <container_id_or_name>
```
*Example: `docker unpause my_container` resumes the container's processes.*

### Rename a Container
```bash
docker rename <old_name> <new_name>
```
*Example: `docker rename old_container new_container` renames the container.*

### Update Container Resources (e.g., CPU, Memory)
```bash
docker update --cpus="1.5" --memory="512m" <container_id_or_name>
```
*Example: `docker update --cpus=2 --memory=1g my_container` adjusts resource limits.*

### Attach to a Running Container
```bash
docker attach <container_id_or_name>
```
*Example: `docker attach my_container` attaches your terminal to a running container.*

### Detach from a Running Container (Without Stopping It)
*Press `Ctrl+P` followed by `Ctrl+Q`.*
*Example: While attached, press the key combination to detach without stopping the container.*

### Commit a Container to Create a New Image
```bash
docker commit <container_id_or_name> <new_image_name>:<tag>
```
*Example: `docker commit my_container myimage:backup` creates a new image from "my_container".*

### Check Changes in a Container’s Filesystem
```bash
docker diff <container_id_or_name>
```
*Example: `docker diff my_container` lists filesystem changes made in the container.*

### Kill a Running Container
```bash
docker kill <container_id_or_name>
```
*Example: `docker kill my_container` sends a SIGKILL to the container.*

### Wait for a Container to Exit
```bash
docker wait <container_id_or_name>
```
*Example: `docker wait my_container` blocks until the container stops and outputs its exit code.*

### Prune Stopped Containers
```bash
docker container prune
```
*Example: `docker container prune` removes all stopped containers.*

## Advanced Image Management

### Save an Image to a Tar Archive
```bash
docker save -o <file_name>.tar <image_name>:<tag>
```
*Example: `docker save -o ubuntu.tar ubuntu:latest` saves the Ubuntu image to a tar file.*

### Load an Image from a Tar Archive
```bash
docker load -i <file_name>.tar
```
*Example: `docker load -i ubuntu.tar` loads an image from a tar archive.*

### Remove All Unused Images
```bash
docker image prune -a
```
*Example: `docker image prune -a` removes all images not used by any container.*

### Remove Dangling Images
```bash
docker image prune
```
*Example: `docker image prune` deletes dangling (untagged) images.*

### List Image Layers
```bash
docker history <image_name>
```
*Example: `docker history ubuntu` shows the layer history of the Ubuntu image.*

### Flatten an Image (Reduce Layers)
```bash
docker export <container_id> | docker import - <flattened_image_name>:<tag>
```
*Example: `docker export my_container | docker import - myimage:flattened` creates a flattened image from a container.*

## Advanced Networking

### Create a Network with a Specific Driver
```bash
docker network create --driver bridge <network_name>
```
*Example: `docker network create --driver bridge custom_bridge` creates a network using the bridge driver.*

### Remove All Unused Networks
```bash
docker network prune
```
*Example: `docker network prune` removes networks that are not in use.*

### Create a Network with a Subnet and Gateway
```bash
docker network create --subnet 192.168.1.0/24 --gateway 192.168.1.1 <network_name>
```
*Example: `docker network create --subnet 192.168.1.0/24 --gateway 192.168.1.1 my_custom_network` creates a custom network with specific IP settings.*

### Attach a Container to a Network with a Specific IP
```bash
docker network connect --ip 192.168.1.10 <network_name> <container_id_or_name>
```
*Example: `docker network connect --ip 192.168.1.10 my_network my_container` assigns a fixed IP address to a container.*

### Disconnect a Container from All Networks
```bash
docker network disconnect -f <network_name> <container_id_or_name>
```
*Example: `docker network disconnect -f my_network my_container` forcefully disconnects the container from the network.*

## Advanced Volume Management

### Create a Volume with Specific Options
```bash
docker volume create --driver local --opt type=tmpfs --opt device=tmpfs --opt o=size=100m <volume_name>
```
*Example: `docker volume create --driver local --opt type=tmpfs --opt device=tmpfs --opt o=size=100m tmp_volume` creates a temporary volume.*

### Backup a Volume
```bash
docker run --rm -v <volume_name>:/volume -v $(pwd):/backup busybox tar cvf /backup/backup.tar /volume
```
*Example: `docker run --rm -v my_volume:/volume -v $(pwd):/backup busybox tar cvf /backup/backup.tar /volume` backs up "my_volume" to a tar file.*

### Restore a Volume from a Backup
```bash
docker run --rm -v <volume_name>:/volume -v $(pwd):/backup busybox tar xvf /backup/backup.tar -C /volume
```
*Example: `docker run --rm -v my_volume:/volume -v $(pwd):/backup busybox tar xvf /backup/backup.tar -C /volume` restores a volume from backup.*

### List Volume Drivers
```bash
docker volume ls --format "{{.Driver}}"
```
*Example: `docker volume ls --format "{{.Driver}}"` lists the driver for each volume.*

## Docker Swarm (Orchestration)

### Initialize a Swarm
```bash
docker swarm init
```
*Example: `docker swarm init` sets up the current node as a swarm manager.*

### Join a Worker Node to a Swarm
```bash
docker swarm join --token <worker_token> <manager_ip>:<port>
```
*Example: `docker swarm join --token SWMTKN-1-0xyz... 192.168.1.2:2377` joins a worker node to the swarm.*

### Join a Manager Node to a Swarm
```bash
docker swarm join --token <manager_token> <manager_ip>:<port>
```
*Example: `docker swarm join --token SWMTKN-1-abc... 192.168.1.2:2377` adds a manager node to the swarm.*

### List Nodes in the Swarm
```bash
docker node ls
```
*Example: `docker node ls` shows all nodes participating in the swarm.*

### Deploy a Stack
```bash
docker stack deploy -c <docker-compose-file> <stack_name>
```
*Example: `docker stack deploy -c docker-compose.yml mystack` deploys a stack named "mystack".*

### List Services in a Stack
```bash
docker stack services <stack_name>
```
*Example: `docker stack services mystack` lists services in the "mystack" stack.*

### Remove a Stack
```bash
docker stack rm <stack_name>
```
*Example: `docker stack rm mystack` removes the stack "mystack".*

### Scale a Service
```bash
docker service scale <service_name>=<replicas>
```
*Example: `docker service scale web=3` scales the "web" service to 3 replicas.*

### Update a Service
```bash
docker service update --image <new_image> <service_name>
```
*Example: `docker service update --image myrepo/web:latest web` updates the service image for "web".*

## Docker Security

### Run a Container in Read-Only Mode
```bash
docker run --read-only <image_name>
```
*Example: `docker run --read-only nginx` runs an nginx container with a read-only filesystem.*

### Limit Container Capabilities
```bash
docker run --cap-drop=ALL --cap-add=<capability> <image_name>
```
*Example: `docker run --cap-drop=ALL --cap-add=NET_ADMIN alpine` drops all capabilities except NET_ADMIN.*

### Run a Container with a Specific User
```bash
docker run --user <user_id> <image_name>
```
*Example: `docker run --user 1001 ubuntu` runs the container as the user with UID 1001.*

### Enable AppArmor or SELinux for a Container
```bash
docker run --security-opt apparmor=<profile> <image_name>
docker run --security-opt seccomp=<profile> <image_name>
```
*Example: `docker run --security-opt apparmor=my_profile nginx` applies the AppArmor profile "my_profile".*

### Scan an Image for Vulnerabilities
```bash
docker scan <image_name>
```
*Example: `docker scan node` scans the Node.js image for vulnerabilities.*

## Docker Registry

### Log in to a Docker Registry
```bash
docker login <registry_url>
```
*Example: `docker login registry.hub.docker.com` logs you into Docker Hub.*

### Log out from a Docker Registry
```bash
docker logout <registry_url>
```
*Example: `docker logout registry.hub.docker.com` logs you out from Docker Hub.*

### List Repositories in a Private Registry
```bash
curl -u <username>:<password> https://<registry_url>/v2/_catalog
```
*Example: `curl -u myuser:mypass https://myregistry.com/v2/_catalog` lists repositories in a private registry.*

### Tag an Image for a Private Registry
```bash
docker tag <image_name> <registry_url>/<repository>:<tag>
```
*Example: `docker tag myapp registry.mycompany.com/myapp:latest` tags an image for a private registry.*

### Push an Image to a Private Registry
```bash
docker push <registry_url>/<repository>:<tag>
```
*Example: `docker push registry.mycompany.com/myapp:latest` uploads the image to the private registry.*

## Debugging and Troubleshooting

### Check Docker Daemon Logs
```bash
journalctl -u docker.service
```
*Example: `journalctl -u docker.service` displays Docker daemon logs (Linux systems).*

### Run a Container with Debugging Tools
```bash
docker run -it --rm busybox sh
```
*Example: `docker run -it --rm busybox sh` starts a temporary container with a shell for debugging.*

### Inspect Docker Events
```bash
docker events
```
*Example: `docker events` outputs real-time Docker event logs.*

### Check Container Resource Usage
```bash
docker stats <container_id_or_name>
```
*Example: `docker stats my_container` shows live resource usage statistics for "my_container".*

### Check Container Processes
```bash
docker top <container_id_or_name>
```
*Example: `docker top my_container` lists processes running inside "my_container".*

## Docker Plugins

### List Installed Plugins
```bash
docker plugin ls
```
*Example: `docker plugin ls` displays a list of all installed plugins.*

### Install a Plugin
```bash
docker plugin install <plugin_name>
```
*Example: `docker plugin install vieux/sshfs` installs the SSHFS plugin.*

### Enable a Plugin
```bash
docker plugin enable <plugin_name>
```
*Example: `docker plugin enable vieux/sshfs` enables the installed SSHFS plugin.*

### Disable a Plugin
```bash
docker plugin disable <plugin_name>
```
*Example: `docker plugin disable vieux/sshfs` disables the SSHFS plugin.*

### Remove a Plugin
```bash
docker plugin rm <plugin_name>
```
*Example: `docker plugin rm vieux/sshfs` removes the SSHFS plugin from your system.*

## Docker Buildx Commands

### Create a New Builder Instance
```bash
docker buildx create --use --name mybuilder
```
*Example: `docker buildx create --use --name mybuilder` creates and uses a new builder instance named "mybuilder".*

### List Builder Instances
```bash
docker buildx ls
```
*Example: `docker buildx ls` shows all available builder instances.*

### Inspect a Builder Instance
```bash
docker buildx inspect mybuilder --bootstrap
```
*Example: `docker buildx inspect mybuilder --bootstrap` inspects and bootstraps the builder instance "mybuilder".*

### Build a Multi-Platform Image Using Buildx
```bash
docker buildx build --platform linux/amd64,linux/arm64 -t myimage:latest .
```
*Example: `docker buildx build --platform linux/amd64,linux/arm64 -t myimage:latest .` builds an image for multiple platforms.*

## Docker Manifest Commands

### Create a Manifest List
```bash
docker manifest create myimage:latest myimage:amd64 myimage:arm64
```
*Example: `docker manifest create myimage:latest myimage:amd64 myimage:arm64` creates a manifest list for different architectures.*

### Annotate a Manifest Entry
```bash
docker manifest annotate myimage:latest myimage:arm64 --os linux --arch arm64
```
*Example: `docker manifest annotate myimage:latest myimage:arm64 --os linux --arch arm64` annotates the ARM64 entry in the manifest.*

### Push a Manifest List
```bash
docker manifest push myimage:latest
```
*Example: `docker manifest push myimage:latest` pushes the manifest list to the registry.*

## Docker Secrets

### Create a Secret
```bash
docker secret create my_secret my_secret_file.txt
```
*Example: `docker secret create my_secret my_secret_file.txt` creates a secret from a file.*

### List Secrets
```bash
docker secret ls
```
*Example: `docker secret ls` lists all Docker secrets in the swarm.*

### Inspect a Secret
```bash
docker secret inspect my_secret
```
*Example: `docker secret inspect my_secret` shows detailed information about "my_secret".*

### Remove a Secret
```bash
docker secret rm my_secret
```
*Example: `docker secret rm my_secret` deletes the secret named "my_secret".*

## Docker Configs

### Create a Config
```bash
docker config create my_config my_config_file.txt
```
*Example: `docker config create my_config my_config_file.txt` creates a configuration named "my_config" from the specified file.*

### List Configs
```bash
docker config ls
```
*Example: `docker config ls` lists all configurations in the swarm.*

### Inspect a Config
```bash
docker config inspect my_config
```
*Example: `docker config inspect my_config` displays details about "my_config".*

### Remove a Config
```bash
docker config rm my_config
```
*Example: `docker config rm my_config` removes the configuration "my_config".*

## Docker Content Trust

### Sign an Image
```bash
docker trust sign <image_name>:<tag>
```
*Example: `docker trust sign myimage:latest` digitally signs the image "myimage:latest".*

### Inspect Trust Data for an Image
```bash
docker trust inspect <image_name>:<tag>
```
*Example: `docker trust inspect myimage:latest` shows trust metadata for "myimage:latest".*
