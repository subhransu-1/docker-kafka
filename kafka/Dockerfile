# Kafka and Zookeeper

FROM java:openjdk-8

ENV DEBIAN_FRONTEND noninteractive
ENV KAFKA_HOME /opt/kafka_2.12-3.2.1

# Install Kafka, Zookeeper and other needed things
RUN apt-get update && \
    apt-get install -y zookeeper wget supervisor dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    wget -q https://downloads.apache.org/kafka/3.2.1/kafka_2.12-3.2.1.tgz -O /tmp/kafka_2.12-3.2.1.tgz && \
    tar xfz /tmp/kafka_2.12-3.2.1.tgz -C /opt && \
    rm /tmp/kafka_2.12-3.2.1.tgz

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
ADD supervisor/kafka.conf supervisor/zookeeper.conf /etc/supervisor/conf.d/

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
