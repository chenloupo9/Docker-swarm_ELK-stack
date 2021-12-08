# Elastic stack (ELK) on Docker swarm 

This is simple repository for creating a docker swarm with one manager and two worker nodes and deploying an ELK stack, which will give you the ability to analyze any data set by using searching/aggregation capabilities of Elasticsearch and the visualization power of kibana. 

## Requirements 
1. **Docker Engine** version 17.05 or newer 
2. **Docker Compose** version 1.20.0 or newer 
3. Host with an available 2CPU and 4GB Memory at least 

*:information_source:  I was using the [Play-with-docker](https://labs.play-with-docker.com/) website to run this ELK stack.

## Creating Docker swarm cluster
- On the manager node create an cluster with the command
```
docker swarm init --advertise-addr <manager-ip-address> --listen-addr <manager-ip-address>:2377
```

- The output of the command will create an token to add worker nodes to the cluster.copy the command to the worker nodes you wish to add and run it.
**you can re-create that command to add a worker node with the following command** 
```
docker swarm join-token worker
```

- You can verify the nodes were added to the cluster and it infromation
```
docker node ls
docker info
```

## Deploying ELK stack 
- Clone the git repository
```
git clone https://github.com/chenloupo9/Docker-swarm_ELK-stack.git
```

- Move to the Docker-swarm_ELK-stack
```
cd Docker-swarm_ELK-stack
```

- Deploy the ELK stack and name it myelk
```
docker stack deploy -c docker-stack.yml myelk
```

*:information_source:


