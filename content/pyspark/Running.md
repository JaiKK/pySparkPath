---
title: "Running"
date: 2021-02-14T08:44:28+11:00
draft: true

booktitle: "pySpark"
linkname: "2. Running"
shortdesc: "This page will guide you to the steps for running Docker container (With Image we built in previous tutorial)"
Weight: 2
---

## Use below command to run Docker container
```powershell

$> docker run -dit -p4040:4040 -p8888:8888 jai/pyspark bash

```
> After logging on container you can run below commands
```bash

$> spark-shell

```
```bash

$> spark-submit

```
```bash

$> pyspark

```
```bash

$> spark-sql

```
```bash

$> sparkR

```
```bash

$> spark-class

```

Below is to test Spark installation and test check examples
```bash

$> /opt/spark/bin/run-example run-example SparkPi 10

```
Below is to interact with HiveServer2 client.
```bash

$> beeline

```

To start Jupyter notebook server use below command
```bash

$> jupyter notebook --port=8888 --no-browser --ip=0.0.0.0 --allow-root

```

To start interactive bash shell
```bash

$> docker run -dit -p4040:4040 jai/pyspark bash

```