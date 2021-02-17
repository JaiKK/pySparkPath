---
title: "Installation"
date: 2021-01-31T23:33:26+11:00
draft: true

booktitle: "pySpark"
linkname: "1. Installation"
shortdesc: "These instruction will guide you to create a Docker image for Spark standalone system. This docker image will be used for all further tutorials."
Weight: 1
---

## Create Dockerfile
This installation method will cover installation of Spark in local system (Linux) and docker container. I have attached Dockerfile with this tutorial and explained each line and its purpose.

I have used Ubuntu for this tutorial but you can choose any linux distribution. Windows I'll cover is separate tutorial.

In this tutorial I have downloaded the spark installer (compressed file) for convenience. But I'll also add commands to download it directly from server while installation.

### Link to installer file: [spark-3.0.1-bin-hadoop2.7.tgz](https://www.strategylions.com.au/mirror/spark/spark-3.0.1/spark-3.0.1-bin-hadoop2.7.tgz)
 

```dockerfile

# Below line is to define the base image for installation

FROM ubuntu:20.04

# Below line is to define maintainer label

LABEL maintainer="jai@email.com"

# Below command will copy downloaded spark file to container. 
# This file should be placed next to Dockerfile.

COPY spark-3.0.1-bin-hadoop2.7.tgz /home

# Below command will update packages information of Ubuntu from all added repositories

RUN cd /home && apt-get update

# Below command will install jdk 8 which is a dependency for Spark.

RUN apt-get -y install openjdk-8-jdk

# Below command will install python and pip. Which are required for pySpark and Jupyter notebook.
# We also update the alternatives to access python and pip easy names rather than using there names with version numbers.
# By default "python3.8" and "pip3" named executables will be installed.

RUN cd /home &&\
    apt-get -y install python3.8 &&\
    update-alternatives --install /usr/bin/python python /usr/bin/python3.8 10 &&\
    apt-get -y install python3-pip  &&\
    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 10

# Below command will extract spark files from tar file and keep in it /opt/spark directory.
# We could have created a link for this folder, which way we could have installed multiple versions on Spark.
# This command will also install Jupyter, to use Notebook for PySpark.
# This will also install findspark module which will connect to local instance of Spark from Notebook.

RUN cd /home &&\
    tar -xzf spark-3.0.1-bin-hadoop2.7.tgz &&\
    mv spark-3.0.1-bin-hadoop2.7 /opt/spark &&\
    pip install jupyter &&\
    pip install findspark

# Below command will delete the installer file are this is no longer required.

RUN cd /home && rm spark-3.0.1-bin-hadoop2.7.tgz

# Below commands will setup environment variables.
# JAVA_HOME is as usual for java as Spark's dependency
# SPARK_HOME also important for findspark module when we'll try to find local runing instance.
# PYSPARK_DRIVER_PYTHON and PYSPARK_DRIVER_PYTHON_OPTS will be required for Jupyter Notebook.
# PYSPARK_DRIVER_PYTHON_OPTS port and ip options are important for this command to expose webUI out of container

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV PATH $PATH:$JAVA_HOME/bin
ENV SPARK_HOME /opt/spark
ENV PATH $SPARK_HOME/bin:$PATH
ENV PYSPARK_DRIVER_PYTHON 'jupyter'
ENV PYSPARK_DRIVER_PYTHON_OPTS 'notebook --port=8888 --no-browser --ip=0.0.0.0 --allow-root'


# Expose 4040 port for Spark WebUI

EXPOSE 4040

# Expose 8888 for Jupyter Notebook

EXPOSE 8888

# Expose 18080 for Spark History server

EXPOSE 18080

# Expose 8080 for Spark MASTER web-UI

EXPOSE 8080

# Expose 8081 for Spark Slave web-UI

EXPOSE 8081

# Expose 7077 for Spark MASTER server

EXPOSE 7077

```




## Create Docker image from Dockerfile

Use below command to create are Docker image from Dockerfile. *Make sure downloaded Spark installer is next to Dockerfile*.

```powershell

docker build -t jai/pyspark .

```

> To start interactive bash shell

```bash

$> docker run -dit -p4040:4040 jai/pyspark bash

```