FROM openjdk:11-slim-buster

LABEL org.opencontainers.image.authors="augusto.orion@gmail.com"

RUN apt-get update && apt-get install openssh-server bash procps python3 sudo wget -y

RUN adduser hadoop --disabled-password && \
    echo "hadoop:hadoop" | chpasswd && \
    echo "hadoop     ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    cd /usr/bin/ && \
    sudo ln -s python3 python

COPY ssh_config /etc/ssh/ssh_config

USER hadoop

WORKDIR /home/hadoop

RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
    chmod -R og-wx ~/.ssh && \
    sudo ssh-keygen -A

ENV HADOOP_VER 3.3.1

RUN wget -q https://downloads.apache.org/hadoop/common/hadoop-${HADOOP_VER}/hadoop-${HADOOP_VER}.tar.gz && \
    tar zxvf hadoop-${HADOOP_VER}.tar.gz && \
    mv hadoop-${HADOOP_VER} hadoop && \
    rm hadoop-${HADOOP_VER}.tar.gz

ENV HADOOP_HOME /home/hadoop/hadoop
ENV JAVA_HOME /usr/local/openjdk-11/
ENV PATH $PATH:$JAVA_HOME/bin
ENV PATH $PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

COPY --chown=hadoop:hadoop config/* $HADOOP_HOME/etc/hadoop/
COPY --chown=hadoop:hadoop docker-entrypoint.sh .
RUN chmod +x ~/docker-entrypoint.sh

ENV HDFS_NAMENODE_USER hadoop
ENV HDFS_DATANODE_USER hadoop
ENV HDFS_SECONDARYNAMENODE_USER hadoop
ENV YARN_RESOURCEMANAGER_USER hadoop
ENV YARN_NODEMANAGER_USER hadoop


RUN echo "export JAVA_HOME=${JAVA_HOME}" >> ${HADOOP_HOME}/etc/hadoop/hadoop-env.sh && \
    echo "export HADOOP_HOME=${HADOOP_HOME}"  >> ${HADOOP_HOME}/etc/hadoop/hadoop-env.sh && \
    echo "export HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop/" >> ${HADOOP_HOME}/etc/hadoop/hadoop-env.sh && \
    echo "export JAVA_HOME=${JAVA_HOME}" >> /home/hadoop/.bashrc


CMD ["/home/hadoop/docker-entrypoint.sh"]