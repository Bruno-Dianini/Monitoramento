README
This is a docker-compose file for setting up a forum API with Redis, MySQL, Nginx, Prometheus, Grafana, and a client.

Prerequisites

Docker
Docker-compose

Setup

Clone the repository and navigate to its directory.
Run the command docker-compose up -d to build and start the containers in detached mode.

Architecture

Networks

There are five networks defined in the docker-compose file:

database: network for MySQL container.
cache: network for Redis container.
api: network for the API and Grafana containers.
monit: network for the Prometheus and Grafana containers.
proxy: network for the Nginx container.

Services

redis-forum-api: Redis container for storing cache data.
mysql-forum-api: MySQL container for storing the forum's database.
app-forum-api: API container built from a Dockerfile with the forum's application code. It depends on the MySQL container, and it has a healthcheck endpoint.
proxy-forum-api: Nginx container for proxying requests to the API container. It depends on the API container.
prometheus-forum-api: Prometheus container for monitoring the API container. It depends on the Nginx container.
grafana-forum-api: Grafana container for visualizing the data collected by Prometheus. It depends on the Prometheus container.
client-forum-api: Container built from a Dockerfile with the client-side code.

Each service has its own configuration, such as the image used, container name, volumes, networks, and dependencies.

Ports

The following ports are exposed:

Redis: 6379
MySQL: 3306
API: 8080
Nginx: 80
Prometheus: 9090
Grafana: 3000

Volumes

The following volumes are used:

./mysql: directory with SQL scripts for initializing the MySQL container.
./nginx/nginx.conf: Nginx configuration file.
./nginx/proxy.conf: Nginx configuration file for proxying requests to the API container.
./prometheus/prometheus.yml: Prometheus configuration file.
./prometheus/prometheus_data: directory for storing Prometheus data.
./grafana: directory for storing Grafana data.

Authors

Bruno Dianini
