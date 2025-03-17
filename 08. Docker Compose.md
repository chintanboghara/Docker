# Docker Compose

**Docker Compose** is a tool that allows you to define and manage multi-container Docker applications. With Compose, you can define your application’s services, networks, and volumes in a YAML file, and then start all the services with a single command. This is especially useful for applications that consist of multiple services, such as a web server, database, cache, etc.

---

### Key Concepts in Docker Compose

1. **Services**: A service is typically a container or set of containers that work together to perform a specific task. For example, a web service and a database service could be part of the same application.
2. **Networks**: Networks allow containers to communicate with each other. Compose automatically creates a default network for your services, but you can also define custom networks.
3. **Volumes**: Volumes allow data to persist between container restarts and to be shared between containers.
4. **Docker Compose File (`docker-compose.yml`)**: This YAML file defines the configuration for all the services, networks, and volumes that make up your application.

---

### Basic `docker-compose.yml` Structure

A typical `docker-compose.yml` file consists of several sections: **version**, **services**, **networks**, and **volumes**.

Here’s an example of a simple `docker-compose.yml` file:

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    networks:
      - app-network

  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: examplepassword
    volumes:
      - db-data:/var/lib/mysql
    networks:
      - app-network

volumes:
  db-data:

networks:
  app-network:
```

### Explanation of the `docker-compose.yml` file:

- **version**: Specifies the version of the Compose file format (in this case, version 3).
- **services**: Defines the containers that make up your application.
  - **web**: This service uses the `nginx` image, exposes port 8080 on the host and port 80 in the container, and mounts a local directory (`./html`) to a directory inside the container (`/usr/share/nginx/html`).
  - **db**: This service uses the `mysql` image, sets an environment variable for the root password, and mounts a named volume (`db-data`) to persist database data.
- **volumes**: Defines the named volumes. The `db-data` volume is used to store MySQL data.
- **networks**: Defines custom networks. The `app-network` allows both `web` and `db` services to communicate with each other.

---

### Basic Docker Compose Commands

1. **Starting the Application**:  
   Once you’ve defined your `docker-compose.yml` file, you can start the services by running:

   ```bash
   docker-compose up
   ```

   This will:
   - Pull the necessary images if they don’t exist locally.
   - Create containers for each service.
   - Start all services in the foreground.

   To run the services in the background (detached mode), add the `-d` flag:

   ```bash
   docker-compose up -d
   ```

2. **Stopping the Application**:  
   To stop all the services, run:

   ```bash
   docker-compose down
   ```

   This will stop and remove all the containers, networks, and volumes created by `docker-compose up`.

3. **Viewing Logs**:  
   You can view the logs of all services or a specific service by running:

   ```bash
   docker-compose logs
   ```

   For specific service logs:

   ```bash
   docker-compose logs web
   ```

4. **Scaling Services**:  
   Docker Compose allows you to scale services by specifying how many containers (replicas) of a service you want to run. For example, to run 3 instances of the `web` service:

   ```bash
   docker-compose up --scale web=3
   ```

5. **Viewing Running Services**:  
   To see the status of running services and containers:

   ```bash
   docker-compose ps
   ```

6. **Building Images**:  
   If your `docker-compose.yml` file defines a service that requires building a custom image (e.g., using a `Dockerfile`), you can build the image using:

   ```bash
   docker-compose build
   ```

7. **Running a One-Off Command**:  
   To execute a one-off command in a running service, you can use `docker-compose exec`. For example, to open a bash shell in the `web` service:

   ```bash
   docker-compose exec web bash
   ```

---

### Example of Multi-Container Application

Here's an example of a more complex application that includes a web server (using Nginx), a PHP application, and a database (MySQL), all managed by Docker Compose.

#### `docker-compose.yml`:

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    networks:
      - app-network

  php:
    image: php:7.4-fpm
    volumes:
      - ./html:/var/www/html
    networks:
      - app-network

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: examplepassword
    volumes:
      - db-data:/var/lib/mysql
    networks:
      - app-network

volumes:
  db-data:

networks:
  app-network:
```

#### File Structure:

```
.
├── docker-compose.yml
└── html
    ├── index.php
```

#### Explanation:

- The `web` service runs Nginx and exposes port 8080. It shares the `html` directory from the host with `/usr/share/nginx/html` in the container.
- The `php` service runs PHP-FPM to process PHP code. It shares the same `html` directory as the `web` service.
- The `db` service runs a MySQL database with a persistent volume to store the database files.
- All services are connected to a common network, `app-network`.

In this example, you can visit `localhost:8080` to see the application served by Nginx, and the PHP application will interact with the MySQL database.

---

### Advanced Docker Compose Features

1. **Environment Variables**:  
   You can pass environment variables to services in the `docker-compose.yml` file or via a `.env` file.

   Example of `.env` file:
   ```env
   MYSQL_PASSWORD=examplepassword
   ```

   Reference in `docker-compose.yml`:
   ```yaml
   environment:
     MYSQL_ROOT_PASSWORD: ${MYSQL_PASSWORD}
   ```

2. **Override Configuration**:  
   Docker Compose allows you to override configurations in a secondary file. For example, you could have a `docker-compose.override.yml` for development-specific configurations:

   ```yaml
   version: '3'
   services:
     web:
       ports:
         - "8081:80"
   ```

   By default, Docker Compose automatically includes `docker-compose.override.yml` when you run `docker-compose up`.

3. **Depends On**:  
   The `depends_on` option is used to control the startup order of services. However, it doesn’t wait for a service to be fully ready before starting dependent services.

   ```yaml
   services:
     web:
       image: nginx
       depends_on:
         - db
   ```

4. **Health Checks**:  
   You can define a health check for a service to ensure that it is healthy before Docker Compose starts other services depending on it.

   ```yaml
   services:
     db:
       image: mysql
       healthcheck:
         test: ["CMD", "mysqladmin", "ping", "-u", "root", "-pexamplepassword"]
         interval: 30s
         retries: 3
   ```

---

### Conclusion

Docker Compose simplifies the management of multi-container applications by allowing you to define, run, and orchestrate multiple services using a single configuration file. Whether you're developing locally or deploying complex systems, Docker Compose can help you automate and streamline the setup and management of your application services, making it an essential tool in modern containerized workflows.
