# Hazelcast for Bucket 4J Quick Start

Hazelcast Docker image with JCache and Bucket4J jars in the classpath, for people willing to quickly use Bucket4J with a remote Hazlecast Server.

It is the same as the [original Hazelcast docker image](https://github.com/hazelcast/hazelcast-docker/blob/master/hazelcast-oss/Dockerfile ) with the addition of:
1. hazelcast.xml with the ability to expose the TCP port to the external world based on this [Stackoverflow post](https://stackoverflow.com/a/47868251/815022)
2. JCcache and Bucket4j jars added to the classpath to make it easy to use with Bucket4J. More details in this [Github issue](https://github.com/hazelcast/hazelcast-docker/issues/50)


Docker image available at:
https://hub.docker.com/r/fsamir/hazelcast-bucket4j/

# Running

```
docker run --name my-hazelcast -d -e JAVA_OPTS="-Dhazelcast.config=/opt/hazelcast/hazelcast.xml -Dhazelcast.ip=`ip route get 8.8.8.8 | awk '{print $NF; exit}'` -Dhazelcast.port=5701" -ti fsamir/hazelcast-bucket4j:3.9.2

```


# Building
```
 docker build  -t fsamir/hazelcast-bucket4j:3.9.2 .

```