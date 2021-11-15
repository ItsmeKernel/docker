# Hadoop Single Node Cluster

This image allows you to create a run Apache Hadoop in single node cluster mode.

# Features

The latest image features:

- OpenJDK 11
- Hadoop 3.3.1
  
# Creating and running a container

`docker run -it --name hdfs -p 9864:9864 -p 9870:9870 -p 8088:8088 -p 2222:22 --hostname localhost augusto1982/hadoop-single-node`