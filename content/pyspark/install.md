---
title: "Install"
date: 2021-01-27T21:34:27+11:00
draft: true

booktitle: "pySpark"
linkname: "Install (pip method)"
shortdesc: "Installation instruction for pySpark."
---

Create a folder named "pySpark".
Create a virtual environment "venv" in "pySpark" folder

```powershell
(base) C:\Users\Aadi\pyspark>.\venv\Scripts\activate.bat

(venv) (base) C:\Users\Aadi\pyspark>pip install pyspark

(base) C:\Users\Aadi\pyspark>.\venv\Scripts\activate.bat

(venv) (base) C:\Users\Aadi\pyspark>pip --version
pip 20.1.1 from c:\users\aadi\pyspark\venv\lib\site-packages\pip (python 3.8)
```

```powershell
(venv) (base) C:\Users\Aadi\pyspark>pip install pyspark
```
```
Collecting pyspark 
 Using cached pyspark-3.0.1.tar.gz (204.2 MB) 
Collecting py4j==0.10.9 
  Using cached py4j-0.10.9-py2.py3-none-any.whl (198 kB) 
Using legacy setup.py install for pyspark, since package 'wheel' is not installed. 
Installing collected packages: py4j, pyspark 
    Running setup.py install for pyspark ... done 
Successfully installed py4j-0.10.9 pyspark-3.0.1 
WARNING: You are using pip version 20.1.1; however, version 21.0 is available. 
You should consider upgrading via the 'c:\users\aadi\pyspark\venv\scripts\python.exe -m pip install --upgrade pip' command. 
```