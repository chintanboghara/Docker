# Monitoring and Logging in Docker

Monitoring and logging are essential for maintaining and troubleshooting containerized applications in Docker. They provide insights into the performance, behavior, and issues of your containers and infrastructure. Docker offers built-in tools for logging and monitoring, and you can integrate third-party solutions for more comprehensive features.

---

### Docker Logging

Docker has a built-in logging mechanism that captures standard output (`stdout`) and standard error (`stderr`) streams from containers. These logs can be viewed using Docker CLI commands or sent to external logging systems for analysis.

#### 1. **Docker Logging Drivers**
Docker supports multiple logging drivers that determine how and where logs are stored. Some common logging drivers include:

| Logging Driver     | Description                                                |
|--------------------|------------------------------------------------------------|
| `json-file`        | Default driver; stores logs as JSON files on the host.     |
| `syslog`           | Sends logs to the syslog server.                           |
| `journald`         | Sends logs to `systemd`'s `journald`.                      |
| `gelf`             | Sends logs to a Graylog Extended Log Format (GELF) server. |
| `fluentd`          | Sends logs to Fluentd.                                     |
| `awslogs`          | Sends logs to AWS CloudWatch.                              |
| `splunk`           | Sends logs to Splunk.                                      |
| `none`             | Disables logging for the container.                        |

You can specify the logging driver globally or per container.

##### Setting a Logging Driver Globally
Edit the Docker daemon configuration file (`/etc/docker/daemon.json`) to set a global logging driver:

```json
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
```

Restart the Docker daemon for the changes to take effect:

```bash
sudo systemctl restart docker
```

##### Setting a Logging Driver Per Container
You can set a specific logging driver when running a container:

```bash
docker run --log-driver=json-file --log-opt max-size=10m --log-opt max-file=3 nginx
```

---

#### 2. **Viewing Container Logs**
Use the `docker logs` command to view logs from a running or stopped container:

```bash
docker logs <container-id>
```

Additional options:
- **Follow logs in real-time**:
  ```bash
  docker logs -f <container-id>
  ```
- **Show a limited number of log lines**:
  ```bash
  docker logs --tail 100 <container-id>
  ```
- **View logs with timestamps**:
  ```bash
  docker logs --timestamps <container-id>
  ```

---

### Docker Monitoring

Monitoring Docker involves tracking the performance of containers, images, networks, and the Docker engine itself. Docker provides basic metrics, but for advanced monitoring, you can use tools like Prometheus, Grafana, or Datadog.

#### 1. **Docker Stats Command**
Docker provides a `stats` command to monitor container resource usage in real-time:

```bash
docker stats
```

Output includes:
- **CPU usage** (%)
- **Memory usage/limit**
- **Network I/O**
- **Block I/O**
- **PIDs**

To monitor specific containers:

```bash
docker stats <container-id1> <container-id2>
```

---

#### 2. **Docker API for Monitoring**
Docker's REST API provides detailed metrics and state information about containers and the Docker engine. Example:

```bash
curl --unix-socket /var/run/docker.sock http://localhost/containers/json
```

---

#### 3. **Third-Party Monitoring Tools**
For large-scale Docker deployments, consider these tools for enhanced monitoring:

- **Prometheus and Grafana**:
  - Prometheus scrapes metrics from Docker and visualizes them using Grafana.
  - Export metrics using cAdvisor, which is purpose-built for container monitoring.

- **Datadog**:
  - A cloud-based monitoring tool that provides real-time metrics, alerts, and dashboards for Docker containers.
  - Datadog’s agent collects container metrics and integrates with orchestrators like Kubernetes.

- **ELK Stack (Elasticsearch, Logstash, Kibana)**:
  - Logstash collects and processes logs.
  - Elasticsearch indexes logs for querying.
  - Kibana visualizes logs and metrics.

- **Sysdig**:
  - Provides deep visibility into Docker containers.
  - Includes runtime security monitoring and troubleshooting features.

---

### Logging and Monitoring Best Practices

1. **Centralized Logging**:
   - Use a centralized logging solution like ELK, Fluentd, or Splunk to aggregate container logs across nodes.

2. **Log Rotation**:
   - Prevent log files from consuming excessive disk space by enabling log rotation using the `json-file` logging driver:
     ```bash
     docker run --log-opt max-size=10m --log-opt max-file=3 nginx
     ```

3. **Monitor Resource Utilization**:
   - Regularly monitor CPU, memory, disk I/O, and network usage to identify performance bottlenecks.

4. **Set Alerts**:
   - Configure alerts for anomalies like high resource utilization, container restarts, or crashes.

5. **Use Labels for Filtering**:
   - Add meaningful labels to containers for easier log filtering and monitoring.

   Example:
   ```bash
   docker run --label app=webserver nginx
   ```

6. **Secure Logs**:
   - Ensure logs don’t expose sensitive information like passwords or tokens. Use tools like Vault to manage secrets.

7. **Automate Monitoring**:
   - Use orchestration tools (e.g., Kubernetes) with built-in monitoring capabilities to automate scaling and performance management.

---

### Example: Setting Up Centralized Monitoring with Prometheus and Grafana

1. **Install cAdvisor**:
   Run the `google/cadvisor` container to export Docker metrics:

   ```bash
   docker run -d \
     --name=cadvisor \
     --volume=/:/rootfs:ro \
     --volume=/var/run:/var/run:ro \
     --volume=/sys:/sys:ro \
     --volume=/var/lib/docker/:/var/lib/docker:ro \
     --publish=8080:8080 \
     gcr.io/cadvisor/cadvisor
   ```

2. **Run Prometheus**:
   Create a `prometheus.yml` configuration file to scrape metrics from cAdvisor:

   ```yaml
   scrape_configs:
     - job_name: 'cadvisor'
       static_configs:
         - targets: ['localhost:8080']
   ```

   Start Prometheus:

   ```bash
   docker run -d \
     --name=prometheus \
     -p 9090:9090 \
     -v $(pwd)/prometheus.yml:/etc/prometheus/prometheus.yml \
     prom/prometheus
   ```

3. **Run Grafana**:
   Run Grafana and configure it to use Prometheus as a data source:

   ```bash
   docker run -d -p 3000:3000 grafana/grafana
   ```

4. **Visualize Metrics**:
   Use Grafana dashboards to monitor your Docker containers.

---

### Conclusion

Effective monitoring and logging in Docker are critical for maintaining reliable, high-performing containerized applications. While Docker provides basic tools like `docker logs` and `docker stats`, integrating with third-party tools allows for comprehensive observability, including alerting, metrics visualization, and centralized log management. Combining these strategies ensures a robust, scalable, and secure container environment.
