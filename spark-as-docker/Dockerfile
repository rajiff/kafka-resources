FROM ubuntu:latest

RUN apt-get update && apt-get -y upgrade

RUN apt-get install -y wget openjdk-8-jre python3 curl

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/
ENV PATH $PATH:$JAVA_HOME/bin

RUN java -version
RUN python3 --version

RUN mkdir sparkdist
WORKDIR sparkdist
ADD http://mirrors.estointernet.in/apache/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz /sparkdist/spark-2.4.0-bin-hadoop2.7.tgz
# RUN curl -o /sparkdist/spark-2.4.0-bin-hadoop2.7.tgz http://mirrors.estointernet.in/apache/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz
RUN tar xvf /sparkdist/spark-2.4.0-bin-hadoop2.7.tgz && rm /sparkdist/spark-2.4.0-bin-hadoop2.7.tgz

CMD ["/bin/bash"]