# image: rabbitmq:3.4

# Set base image
FROM ubuntu:14.04

MAINTAINER Nhat Nguyen <nminhnhat2008@gmail.com>

ENV RABBITMQ_VERSION 3.5.4-1

ADD bin/rabbitmq-start /usr/local/bin/

RUN apt-get update &&\
    apt-get install -y wget &&\
    echo "deb http://www.rabbitmq.com/debian/ testing main" >> /etc/apt/sources.list &&\
    wget http://www.rabbitmq.com/rabbitmq-signing-key-public.asc &&\
    apt-key add rabbitmq-signing-key-public.asc &&\
    apt-get update &&\
    apt-get install -y rabbitmq-server=${RABBITMQ_VERSION} &&\
    rabbitmq-plugins enable rabbitmq_management &&\
    chmod +x /usr/local/bin/rabbitmq-start &&\
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Add script to set Rabbitmq password
ADD set_rabbitmq_password.sh /set_rabbitmq_password.sh
RUN chmod 755 /set_rabbitmq_password.sh

# Define environment variables.
ENV RABBITMQ_LOG_BASE /data/log

#This base directory contains sub-directories for 
#the RabbitMQ server's Mnesia database files
ENV RABBITMQ_MNESIA_BASE /data/mnesia

# Define mount points.
VOLUME ["/data/log", "/data/mnesia"]

# Define working directory.
WORKDIR /data

EXPOSE 5672 15672

CMD ["rabbitmq-start"]