# Elastic stack (ELK) on Docker swarm 

This is simple repository for creating a docker swarm with one manager and two worker nodes and deploying an ELK stack, which will give you the ability to analyze any data set by using searching/aggregation capabilities of Elasticsearch and the visualization power of kibana. 

## Requirements 
1. **Docker Engine** version 17.05 or newer 
2. **Docker Compose** version 1.20.0 or newer 
3. Host with an available 2CPU and 4GB Memory at least 

*:information_source:  I was using the [Play-with-docker](https://labs.play-with-docker.com/) website to run this ELK stack.*

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

- You can verify the nodes were added to the cluster, and the cluster information.
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

*:information_source: It may take a minute for kibana to initialize*

- On the web broswer enter the <http://localhost:5601>
* The defualt port of kibana is 5601.

**:warning: For the [play-with-docker](https://labs.play-with-docker.com/) you will need to press on the port number at the top of the page and a new tab with kibana will be open.**

## Initial setup
- Loging to kibana
*By default the stack is pre-configured with the following **privileged** bootstrap user:* 
 * user: *elastic* 
 * password: *changeme*

## Injecting date 
- Inject logstash log files to elasticsearch
```
cat /path/to/logfle.log | nc -n localhost 5000
```

* The default port for logstash input in 5000.

## Creating an index pattern 
- On the kibana web UI navigate to the _Discover_ on the left sidebar.
- You should be able to create an index pattern.
- Enter `logstash-*` to match the logstash indices.
- Select `@timestamp` as the time filter filed from the menu below. 
- Click `Create index pattern` and return to the _Discover_ page.
- View the log entries. 

## Cleanup
- To remove the ELK stack use the folowing command: 
```
docker stack rm myelk
```

**:information_source: To run the ELK stack with the filebeat extension, follow to instructions in the README file located in the extensions/filebeat directory.**

```
cd extensions/filebeat/
```
