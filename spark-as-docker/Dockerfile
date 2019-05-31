FROM ubuntu:latest

RUN apt-get update && apt-get -y upgrade

RUN apt-get install -y wget openjdk-8-jre python3 curl

RUN mkdir -p /sparkdist
WORKDIR sparkdist
# Commented ADD as every time we build, it downloads again and rebuilds there onwards, however with curl thats not the issue
# ADD http://mirrors.estointernet.in/apache/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz /sparkdist/spark-2.4.0-bin-hadoop2.7.tgz
RUN curl -o /sparkdist/spark-2.4.0-bin-hadoop2.7.tgz http://mirrors.estointernet.in/apache/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz

RUN mkdir -p /spark
WORKDIR /spark
RUN tar xvf /sparkdist/spark-2.4.0-bin-hadoop2.7.tgz -C /spark --strip-components=1 && rm /sparkdist/spark-2.4.0-bin-hadoop2.7.tgz

RUN chown -R root:root /spark

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/jre/
ENV PATH $PATH:$JAVA_HOME

RUN java -version
RUN python3 --version

RUN mkdir -p /user/spark && chown -R root:root /user/spark
RUN mkdir -p /conf && chown -R root:root /conf

# Python by default has installed only as python3, hence create an aliased executable link for it
RUN ln /usr/bin/python /usr/bin/python3

# CMD ["/bin/bash"]
CMD ["/spark/bin/spark-class", "org.apache.spark.deploy.master.Master"]