# Hazelcast for Bucket 4J Quick Start
Same as https://github.com/hazelcast/hazelcast-docker/blob/master/hazelcast-oss/Dockerfile with the addition of:
1. hazelcast.xml with the ability to expose the TCP port to the external world
2. JCcache and Bucket4j jars added to the classpath to make it easy to use with Bucket4J

# Running

```
docker run --name my-hazelcast -d -e JAVA_OPTS="-Dhazelcast.config=/opt/hazelcast/hazelcast.xml -Dhazelcast.ip=`ip route get 8.8.8.8 | awk '{print $NF; exit}'` -Dhazelcast.port=5701" -ti fsamir/hazelcast-bucket4j:3.9.2

```


# Building
```
 docker build  -t fsamir/hazelcast-bucket4j:3.9.2 .

```