FROM amazonlinux:2
FROM amazoncorretto:8
FROM maven:3.6-amazoncorretto-8

RUN yum install -y procps

WORKDIR /tmp/
ADD pom.xml /tmp
RUN curl -o ./spark-2.4.3-bin-without-hadoop.tgz https://archive.apache.org/dist/spark/spark-2.4.3/spark-2.4.3-bin-without-hadoop.tgz
RUN tar -xzf spark-2.4.3-bin-without-hadoop.tgz && \
    mv spark-2.4.3-bin-without-hadoop /opt/spark && \
    rm spark-2.4.3-bin-without-hadoop.tgz
RUN mvn dependency:copy-dependencies -DoutputDirectory=/opt/spark/jars/

RUN echo $'\n\
spark.eventLog.enabled                      true\n\
spark.history.ui.port                       18080\n\
' > /opt/spark/conf/spark-defaults.conf

RUN echo $'\n\
SPARK_DAEMON_MEMORY=$SPARK_DAEMON_MEMORY\n\
' > /opt/spark/conf/spark-env.sh

ENTRYPOINT ["/bin/bash", "-c"]:

