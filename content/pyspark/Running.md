---
title: "Running"
date: 2021-02-14T08:44:28+11:00
draft: true

booktitle: "pySpark"
linkname: "2. Running"
shortdesc: "This page will guide you to the steps for running Docker container (With Image we built in previous tutorial)"
Weight: 2
---

After installation its time to test our Spark installation. we'll test in below order:

1. Notebook
1. SHELL
1. Cluster

## Use below command to run Docker container

```powershell

C:\> docker run -dit -p4040:4040 -p8888:8888 -p18080:18080 -p8080:8080 -p8081:8081 -p7077:7077 --name pySparkCluster --hostname pySparkCluster jai/pyspark bash

```
Pay attention that we have mapped all port to localhost and defined container hostname to 'pySparkCluster'. This is important mainly to manage URL's as by default they have IP address. With this hostname set we'll update our local host file to map this hostname to localhost.

> Update file ***"c:\Windows\System32\drivers\etc\hosts"*** and add below line at the end of the file.

***
```
127.0.0.1 pySparkCluster
```
***

> Now logon to container, using below command.

```powershell

C:\> docker attach pySparkCluster

```

> After logging on container check few essential things, run printenv command and check specially "PYSPARK_DRIVER_PYTHON" and "PYSPARK_DRIVER_PYTHON_OPTS" variables are set.

```bash

$> printenv
PYSPARK_DRIVER_PYTHON=jupyter
HOSTNAME=pySparkCluster
HOME=/root
TERM=xterm
PATH=/opt/spark/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/jvm/java-8-openjdk-amd64/bin
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
PYSPARK_DRIVER_PYTHON_OPTS=notebook --port=8888 --no-browser --ip=0.0.0.0 --allow-root
PWD=/
SPARK_HOME=/opt/spark

```

> If "PYSPARK_DRIVER_PYTHON" environment is set and you run pyspark it'll run on Jupyter notebook else if these variables are not set then pyspark will run on IPython shell. We'll test both. Run below command and open the received URL (with hostname **pySparkCluster** for convenience) in browser. Check chapters for Notebooks for connections and testing pyspark code in Notebook.

```bash

$> pyspark

[I 12:00:34.370 NotebookApp] Writing notebook server cookie secret to /root/.local/share/jupyter/runtime/notebook_cookie_secret
[I 12:00:37.699 NotebookApp] Serving notebooks from local directory: /
[I 12:00:37.699 NotebookApp] Jupyter Notebook 6.2.0 is running at:
[I 12:00:37.699 NotebookApp] http://pySparkCluster:8888/?token=8db6ca8fb458ad6e926f9fdfa9fe4f2b72dac4f84c1bc77a
[I 12:00:37.699 NotebookApp]  or http://127.0.0.1:8888/?token=8db6ca8fb458ad6e926f9fdfa9fe4f2b72dac4f84c1bc77a
[I 12:00:37.700 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 12:00:37.719 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///root/.local/share/jupyter/runtime/nbserver-204-open.html
    Or copy and paste one of these URLs:
        http://pySparkCluster:8888/?token=8db6ca8fb458ad6e926f9fdfa9fe4f2b72dac4f84c1bc77a
     or http://127.0.0.1:8888/?token=8db6ca8fb458ad6e926f9fdfa9fe4f2b72dac4f84c1bc77a
```

> To test pyspark shell in IPython make sure "PYSPARK_DRIVER_PYTHON" and "PYSPARK_DRIVER_PYTHON_OPTS" environment variables are not set. Use ```unset``` command to unset environment variables and run pyspark.

```bash
$> unset PYSPARK_DRIVER_PYTHON
$> unset PYSPARK_DRIVER_PYTHON_OPTS

$> pyspark

Python 3.8.5 (default, Jul 28 2020, 12:59:40)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
21/02/17 12:09:33 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Using Spark's default log4j profile: org/apache/spark/log4j-defaults.properties
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /__ / .__/\_,_/_/ /_/\_\   version 3.0.1
      /_/

Using Python version 3.8.5 (default, Jul 28 2020 12:59:40)
SparkSession available as 'spark'.
>>>


```
> Hint: Use quit() to quit from pyspark shell


> To test Scala shell run below command.

```bash

$> spark-shell

```
> Hint: Use :quit to quit from scala spark shell and :help for more details

> ((Need to update below for program submission on cluster ))

```bash

$> spark-submit

```

> ((Need to update below for SQL context ))

```bash

$> spark-sql

```

> ((Need to update below for R support ))

```bash

$> sparkR

```

> ((Need to update below  ))

```bash

$> spark-class

```

> Below is to test Spark installation and test check examples

```bash

$> /opt/spark/bin/run-example run-example SparkPi 10

```
> Below is to interact with HiveServer2 client.

```bash

$> beeline

```

> To start Jupyter notebook server with pyspark context use below command (In this method you have to create the spark context manually in Notebook)

```bash

$> jupyter notebook --port=8888 --no-browser --ip=0.0.0.0 --allow-root

```
