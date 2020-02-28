FROM hazelcast/hazelcast:3.9.2

ENV BUCKET4J_VERSION 4.9.0
ENV BUCKET4J_HZ_ARTIFACT_ID="bucket4j-hazelcast-3"
ENV JCACHE_VERSION 1.1.0

ENV HZ_LIB $HZ_HOME/lib
RUN mkdir -p $HZ_LIB
WORKDIR $HZ_LIB


# Download jcache and bucket4j jars from maven repo.
ADD https://repo1.maven.org/maven2/com/hazelcast/hazelcast-all/$HZ_VERSION/hazelcast-all-$HZ_VERSION.jar $HZ_LIB
ADD https://repo.maven.apache.org/maven2/javax/cache/cache-api/$JCACHE_VERSION/cache-api-$JCACHE_VERSION.jar $HZ_LIB
ADD https://repo.maven.apache.org/maven2/com/github/vladimir-bukhtoyarov/bucket4j-core/$BUCKET4J_VERSION/bucket4j-core-$BUCKET4J_VERSION.jar $HZ_LIB
ADD https://repo.maven.apache.org/maven2/com/github/vladimir-bukhtoyarov/bucket4j-jcache/$BUCKET4J_VERSION/bucket4j-jcache-$BUCKET4J_VERSION.jar $HZ_LIB
ADD https://repo.maven.apache.org/maven2/com/github/vladimir-bukhtoyarov/$BUCKET4J_HZ_ARTIFACT_ID/$BUCKET4J_VERSION/$BUCKET4J_HZ_ARTIFACT_ID-$BUCKET4J_VERSION.jar $HZ_LIB


#Original server.sh expected all eternal libs to be in a folder set by the CLASSPATH env variable. This is misleading and captured here: https://github.com/hazelcast/hazelcast-docker/issues/45
ENV CLASSPATH $HZ_LIB

WORKDIR $HZ_HOME

# Add your custom hazelcast.xml
ADD hazelcast.xml $HZ_HOME

RUN echo "CONTAINER_IP=\$(ip route get 8.8.8.8 | awk '{print \$NF; exit}')" >> ./server.sh.temp
RUN echo "export JAVA_OPTS=\"\${JAVA_OPTS} -Dhazelcast.config=/opt/hazelcast/hazelcast.xml -Dhazelcast.port=5701 -Dhazelcast.ip=\$CONTAINER_IP\"" >> ./server.sh.temp
RUN echo "$(cat ./server.sh)" >> ./server.sh.temp
RUN echo "$(cat ./server.sh.temp)" > ./server.sh

# Run hazelcast
CMD ./server.sh
EXPOSE 5701

#docker run -e "JAVA_OPTS=\"-Dhazelcast.config=/opt/hazelcast/hazelcast.xml -Dhazelcast.port=5701\"" -ti hazelcast-test-v2:latest