FROM ubuntu:latest

RUN apt-get update && apt-get install -y wget openjdk-8-jre

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/
ENV PATH $PATH:$JAVA_HOME/bin

RUN mkdir sparkdist
WORKDIR sparkdist
RUN wget https://www.apache.org/dyn/closer.lua/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz

CMD ["/bin/bash"]