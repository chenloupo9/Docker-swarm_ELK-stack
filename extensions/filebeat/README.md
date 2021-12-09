# Filebeat

Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers,
Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to
Elasticsearch or Logstash for indexing.

## Usage

To include Filebeat in the stack, run Docker Compose from the root of the repository with an additional command line
argument referencing the `filebeat-compose.yml` file:

```
cd ~/Docker-swarm_ELK-stack
docker-compose -f docker-compose.yml -f extensions/filebeat/filebeat-compose.yml up -d
```

## Configuring Filebeat

The Filebeat configuration is stored in [`config/filebeat.yml`](./config/filebeat.yml). You can modify this file with
the help of the [Configuration reference][filebeat-config].

## Initial setup
- Loging to kibana
*By default the stack is pre-configured with the following **privileged** bootstrap user:*
 * user: *elastic*
 * password: *changeme*

## Creating an index pattern
- On the kibana web UI navigate to the _Discover_ on the left sidebar.
- You should be able to create an index pattern.
- Enter `filebeat-*`.
- Select `@timestamp` as the time filter filed from the menu below.
- Click `Create index pattern` and return to the _Discover_ page.
- View the log entries.

## Cleanup
In order to entirely shutdown the stack and remove all persisted data, including the Elasticsearch volume, run the following command: 
```
docker-compose -f docker-compose.yml -f extensions/filebea/filebeat-compose.yml down -v
```

