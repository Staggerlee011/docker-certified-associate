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

