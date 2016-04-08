# Supported tags and respective `Dockerfile` links

-   [`latest`, `3.6`, `3.6.2` (*3.6/icestorm/Dockerfile*)](https://github.com/zeroc-ice/ice-dockerfiles/blob/master/3.6/icestorm/Dockerfile)


# What is IceStorm?

IceStorm is a publish-subscribe event distribution service that helps you create push applications using the [Ice](https://zeroc.com) RPC framework.

# How to use this image

## Start `icestorm` service

```
docker run --name some-icestorm -v /path/to/config:/config.icestorm:ro -d zeroc/icestorm
```

Refer to the  [IceStorm documenation](https://doc.zeroc.com/display/Ice/IceStorm) for more information on how to configure IceStorm.

## Database volume

The IceStorm container does its database data in a Docker volume mounted at `/db`.

```
docker run --name some-icestorm -v /path/to/config:/config.icestorm:ro -v/path/to/folder:/db -d zeroc/icestorm
```

## Sample Configuration

```
#
# The IceStorm service instance name.
#
IceStorm.InstanceName=MyIceStorm

#
# This property defines the endpoints on which the IceStorm
# TopicManager listens.
#
IceStorm.TopicManager.Endpoints=default -h localhost -p 10000
IceStorm.TopicManager.PublishedEndpoints=default -h <docker host ip> -p 10000

#
# This property defines the endpoints on which the topic
# publisher objects listen. If you want to federate
# IceStorm instances this must run on a fixed port (or use
# IceGrid).
#
IceStorm.Publish.Endpoints=tcp -h localhost -p 10001:udp -h localhost -p 10001
IceStorm.Publish.Endpoints=tcp -h <docker host ip> -p 10001:udp -h <docker host ip> -p 10001
#
# TopicManager Tracing
#
# 0 = no tracing
# 1 = trace topic creation, subscription, unsubscription
# 2 = like 1, but with more detailed subscription information
#
IceStorm.Trace.TopicManager=2

#
# Topic Tracing
#
# 0 = no tracing
# 1 = trace unsubscription diagnostics
# 2 = like 1, but with more detailed subscription information
#
IceStorm.Trace.Topic=1

#
# Subscriber Tracing
#
# 0 = no tracing
# 1 = subscriber diagnostics (subscription, unsubscription, event
#     propagation failures)
# 2 = like 1, but with more detailed subscription information
#
IceStorm.Trace.Subscriber=1

#
# Amount of time in milliseconds between flushes for batch mode
# transfer. The minimum allowable value is 100ms.
#
IceStorm.Flush.Timeout=2000

#
# Network Tracing
#
# 0 = no network tracing
# 1 = trace connection establishment and closure
# 2 = like 1, but more detailed
# 3 = like 2, but also trace data transfer
#
#Ice.Trace.Network=1

#
# This property defines the home directory of the LMDB
# database environment for the IceStorm service.
#
IceStorm.LMDB.Path=db

#
# IceMX configuration.
#
#Ice.Admin.Endpoints=tcp -h localhost -p 10004
Ice.Admin.InstanceName=icestorm
IceMX.Metrics.Debug.GroupBy=id
IceMX.Metrics.ByParent.GroupBy=parent
```