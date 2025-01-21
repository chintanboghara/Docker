### **Basic Docker Commands**
1. **Check Docker Version**
   ```bash
   docker --version
   ```

2. **Display System-Wide Information**
   ```bash
   docker info
   ```

3. **Run a Container**
   ```bash
   docker run <image_name>
   ```

4. **Run a Container in Interactive Mode**
   ```bash
   docker run -it <image_name> /bin/bash
   ```

5. **Run a Container in Detached Mode**
   ```bash
   docker run -d <image_name>
   ```

6. **List Running Containers**
   ```bash
   docker ps
   ```

7. **List All Containers (Running and Stopped)**
   ```bash
   docker ps -a
   ```

8. **Stop a Container**
   ```bash
   docker stop <container_id_or_name>
   ```

9. **Start a Stopped Container**
   ```bash
   docker start <container_id_or_name>
   ```

10. **Restart a Container**
    ```bash
    docker restart <container_id_or_name>
    ```

11. **Remove a Container**
    ```bash
    docker rm <container_id_or_name>
    ```

12. **Force Remove a Running Container**
    ```bash
    docker rm -f <container_id_or_name>
    ```

### **Image Management**
1. **List Images**
   ```bash
   docker images
   ```

2. **Pull an Image from Docker Hub**
   ```bash
   docker pull <image_name>
   ```

3. **Remove an Image**
   ```bash
   docker rmi <image_id_or_name>
   ```

4. **Build an Image from a Dockerfile**
   ```bash
   docker build -t <image_name> .
   ```

5. **Tag an Image**
   ```bash
   docker tag <image_id> <new_image_name>:<tag>
   ```

6. **Push an Image to Docker Hub**
   ```bash
   docker push <image_name>
   ```

### **Container Logs and Monitoring**
1. **View Container Logs**
   ```bash
   docker logs <container_id_or_name>
   ```

2. **Follow Container Logs in Real-Time**
   ```bash
   docker logs -f <container_id_or_name>
   ```

3. **Inspect a Container**
   ```bash
   docker inspect <container_id_or_name>
   ```

4. **View Resource Usage (Stats)**
   ```bash
   docker stats <container_id_or_name>
   ```

5. **Execute a Command in a Running Container**
   ```bash
   docker exec -it <container_id_or_name> <command>
   ```

### **Networking**
1. **List Networks**
   ```bash
   docker network ls
   ```

2. **Create a Network**
   ```bash
   docker network create <network_name>
   ```

3. **Connect a Container to a Network**
   ```bash
   docker network connect <network_name> <container_id_or_name>
   ```

4. **Disconnect a Container from a Network**
   ```bash
   docker network disconnect <network_name> <container_id_or_name>
   ```

5. **Inspect a Network**
   ```bash
   docker network inspect <network_name>
   ```

### **Volume Management**
1. **List Volumes**
   ```bash
   docker volume ls
   ```

2. **Create a Volume**
   ```bash
   docker volume create <volume_name>
   ```

3. **Inspect a Volume**
   ```bash
   docker volume inspect <volume_name>
   ```

4. **Remove a Volume**
   ```bash
   docker volume rm <volume_name>
   ```

5. **Remove Unused Volumes**
   ```bash
   docker volume prune
   ```

### **Docker Compose**
1. **Start Services**
   ```bash
   docker-compose up
   ```

2. **Start Services in Detached Mode**
   ```bash
   docker-compose up -d
   ```

3. **Stop Services**
   ```bash
   docker-compose down
   ```

4. **Rebuild and Restart Services**
   ```bash
   docker-compose up --build
   ```

5. **View Logs for a Service**
   ```bash
   docker-compose logs <service_name>
   ```

6. **List Running Services**
   ```bash
   docker-compose ps
   ```

### **Miscellaneous**
1. **Prune Unused Objects**
   ```bash
   docker system prune
   ```

2. **Prune Everything (Including Volumes and Images)**
   ```bash
   docker system prune -a --volumes
   ```

3. **Copy Files Between Host and Container**
   ```bash
   docker cp <file_path> <container_id_or_name>:<container_path>
   docker cp <container_id_or_name>:<container_path> <file_path>
   ```

4. **Export a Container to a Tar Archive**
   ```bash
   docker export <container_id_or_name> > <file_name>.tar
   ```

5. **Import a Container from a Tar Archive**
   ```bash
   docker import <file_name>.tar <image_name>:<tag>
   ```

### **Advanced Container Management**
1. **Pause a Running Container**
   ```bash
   docker pause <container_id_or_name>
   ```

2. **Unpause a Paused Container**
   ```bash
   docker unpause <container_id_or_name>
   ```

3. **Rename a Container**
   ```bash
   docker rename <old_name> <new_name>
   ```

4. **Update Container Resources (e.g., CPU, Memory)**
   ```bash
   docker update --cpus="1.5" --memory="512m" <container_id_or_name>
   ```

5. **Attach to a Running Container**
   ```bash
   docker attach <container_id_or_name>
   ```

6. **Detach from a Running Container (Without Stopping It)**
   - Press `Ctrl+P` followed by `Ctrl+Q`.

7. **Commit a Container to Create a New Image**
   ```bash
   docker commit <container_id_or_name> <new_image_name>:<tag>
   ```

8. **Check Changes in a Container’s Filesystem**
   ```bash
   docker diff <container_id_or_name>
   ```

### **Advanced Image Management**
1. **Save an Image to a Tar Archive**
   ```bash
   docker save -o <file_name>.tar <image_name>:<tag>
   ```

2. **Load an Image from a Tar Archive**
   ```bash
   docker load -i <file_name>.tar
   ```

3. **Remove All Unused Images**
   ```bash
   docker image prune -a
   ```

4. **List Image Layers**
   ```bash
   docker history <image_name>
   ```

5. **Flatten an Image (Reduce Layers)**
   ```bash
   docker export <container_id> | docker import - <flattened_image_name>:<tag>
   ```

### **Advanced Networking**
1. **Create a Network with a Specific Driver**
   ```bash
   docker network create --driver bridge <network_name>
   ```

2. **Remove All Unused Networks**
   ```bash
   docker network prune
   ```

3. **Create a Network with a Subnet and Gateway**
   ```bash
   docker network create --subnet 192.168.1.0/24 --gateway 192.168.1.1 <network_name>
   ```

4. **Attach a Container to a Network with a Specific IP**
   ```bash
   docker network connect --ip 192.168.1.10 <network_name> <container_id_or_name>
   ```

5. **Disconnect a Container from All Networks**
   ```bash
   docker network disconnect -f <network_name> <container_id_or_name>
   ```

### **Advanced Volume Management**
1. **Create a Volume with Specific Options**
   ```bash
   docker volume create --driver local --opt type=tmpfs --opt device=tmpfs --opt o=size=100m <volume_name>
   ```

2. **Backup a Volume**
   ```bash
   docker run --rm -v <volume_name>:/volume -v $(pwd):/backup busybox tar cvf /backup/backup.tar /volume
   ```

3. **Restore a Volume from a Backup**
   ```bash
   docker run --rm -v <volume_name>:/volume -v $(pwd):/backup busybox tar xvf /backup/backup.tar -C /volume
   ```

4. **List Volume Drivers**
   ```bash
   docker volume ls --format "{{.Driver}}"
   ```

### **Docker Swarm (Orchestration)**
1. **Initialize a Swarm**
   ```bash
   docker swarm init
   ```

2. **Join a Worker Node to a Swarm**
   ```bash
   docker swarm join --token <worker_token> <manager_ip>:<port>
   ```

3. **Join a Manager Node to a Swarm**
   ```bash
   docker swarm join --token <manager_token> <manager_ip>:<port>
   ```

4. **List Nodes in the Swarm**
   ```bash
   docker node ls
   ```

5. **Deploy a Stack**
   ```bash
   docker stack deploy -c <docker-compose-file> <stack_name>
   ```

6. **List Services in a Stack**
   ```bash
   docker stack services <stack_name>
   ```

7. **Remove a Stack**
   ```bash
   docker stack rm <stack_name>
   ```

8. **Scale a Service**
   ```bash
   docker service scale <service_name>=<replicas>
   ```

9. **Update a Service**
   ```bash
   docker service update --image <new_image> <service_name>
   ```

### **Docker Security**
1. **Run a Container in Read-Only Mode**
   ```bash
   docker run --read-only <image_name>
   ```

2. **Limit Container Capabilities**
   ```bash
   docker run --cap-drop=ALL --cap-add=<capability> <image_name>
   ```

3. **Run a Container with a Specific User**
   ```bash
   docker run --user <user_id> <image_name>
   ```

4. **Enable AppArmor or SELinux for a Container**
   ```bash
   docker run --security-opt apparmor=<profile> <image_name>
   docker run --security-opt seccomp=<profile> <image_name>
   ```

5. **Scan an Image for Vulnerabilities**
   ```bash
   docker scan <image_name>
   ```

### **Docker Registry**
1. **Log in to a Docker Registry**
   ```bash
   docker login <registry_url>
   ```

2. **Log out from a Docker Registry**
   ```bash
   docker logout <registry_url>
   ```

3. **List Repositories in a Private Registry**
   ```bash
   curl -u <username>:<password> https://<registry_url>/v2/_catalog
   ```

4. **Tag an Image for a Private Registry**
   ```bash
   docker tag <image_name> <registry_url>/<repository>:<tag>
   ```

5. **Push an Image to a Private Registry**
   ```bash
   docker push <registry_url>/<repository>:<tag>
   ```

### **Debugging and Troubleshooting**
1. **Check Docker Daemon Logs**
   ```bash
   journalctl -u docker.service
   ```

2. **Run a Container with Debugging Tools**
   ```bash
   docker run -it --rm busybox sh
   ```

3. **Inspect Docker Events**
   ```bash
   docker events
   ```

4. **Check Container Resource Usage**
   ```bash
   docker stats <container_id_or_name>
   ```

5. **Check Container Processes**
   ```bash
   docker top <container_id_or_name>
   ```

### **Docker Plugins**
1. **List Installed Plugins**
   ```bash
   docker plugin ls
   ```

2. **Install a Plugin**
   ```bash
   docker plugin install <plugin_name>
   ```

3. **Enable a Plugin**
   ```bash
   docker plugin enable <plugin_name>
   ```

4. **Disable a Plugin**
   ```bash
   docker plugin disable <plugin_name>
   ```

5. **Remove a Plugin**
   ```bash
   docker plugin rm <plugin_name>
   ```
