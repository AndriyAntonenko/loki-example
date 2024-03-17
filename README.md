# Description

> This repo is the example of using Grafana loki as centralized logs storage for applications in docker swarm cluster.

To setup a cluster pls use `digital-ocean-cluster` repository. It is my another one repo with terraform spec to deploy swarm cluster to Digital ocean.
To run the service export env variables from the `.env.example` and run the commands below

```bash
# on each swarm node install grafana loki docker driver for logging
docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions

# setup secrets for grafana
echo "<grafana_admin_user>" | docker secret create grafana_admin_user -
echo "<grafana_admin_password>" | docker secret create grafana_admin_password -

# create loki config
docker config create loki_config loki-config.yaml

# run the docker stack
docker stack deploy -c ./docker-compose.yml monitoring
```
