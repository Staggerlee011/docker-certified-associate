# logging drivers

## Standards

Default of: json-file  

Standard options in a windows machine are:

``` c#
 Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
```

To view the current driver run

``` c#
# linux
docker info | grep logging

# windows
docker info

```

## Update

To change the logging driver update: `/etc/docker.daemon.json`  

NOTE: `systemctl restart docker` needed after updating `daemon.json`

### Example daemon.json updates

``` c#
{
    "log-driver": "fluentd"
}
```

``` c#
{
    "log-driver": "json-file"
    "log-opts": {
        "max-size": "15m"
    }
}
```

## Configuring / override Logging at container

You can configure / override the logging settings at the container level as well as the host level via running the container with the `--log-driver` command

``` c#
docker run --log-driver syslog nginx
```

you can also configure / override the log options in the command as well

``` c#
docker run --log-driver json-file --log-opt max-size=15m nginx
```


## Popular logging-drivers

| Driver | Description |
|:- |:- |
|none	|        No logs are available for the container and docker logs does not return any output. |
|local	     |   Logs are stored in a custom format designed for minimal overhead.|
|json-file	|The logs are formatted as JSON. The default logging driver for Docker.|
|syslog	     |   Writes logging messages to the syslog facility. The syslog daemon mst be running on the host machine.|
|journald	 |   Writes log messages to journald. The journald daemon must be running on the host machine.|
|gelf	     |   Writes log messages to a Graylog Extended Log Format (GELF) endpoint such as Graylog or Logstash.|
|fluentd	 |       Writes log messages to fluentd (forward input). The fluentd daemon must be running on the host machine. |
|awslogs	 |       Writes log messages to Amazon CloudWatch Logs.|
|splunk	     |   Writes log messages to splunk using the HTTP Event Collector. |
|etwlogs	 |       Writes log messages as Event Tracing for Windows (ETW) events. Only |available on Windows platforms. |
|gcplogs	 |       Writes log messages to Google Cloud Platform (GCP) Logging. |
|logentries |	    Writes log messages to Rapid7 Logentries.|

