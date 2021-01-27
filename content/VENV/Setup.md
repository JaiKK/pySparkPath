---
title: "Setup"
date: 2021-01-27T19:32:42+11:00
draft: true

booktitle: "VENV"
linkname: "Setup"
shortdesc: "How to setup VENV in python for virtual environment."
---

Reference video: https://www.youtube.com/watch?v=APOPm01BVrk

Reference document: https://docs.python.org/3/library/venv.html

Command: python -m venv <environment name>

By convention its good to create virtual environment with name of "venv". This we can add in gitignore file as well.

```python
python -m venv venv 
```
First venv in above command is module name and second is the name of environment to be created.















(base) C:\Users\Aadi>python --version

(base) C:\Users\Aadi>python -m venv --help

(base) C:\Users\Aadi>mkdir pyspark

(base) C:\Users\Aadi>cd pyspark

(base) C:\Users\Aadi\pyspark>python -m venv venv

(base) C:\Users\Aadi\pyspark>.\venv\Scripts\activate.bat

(venv) (base) C:\Users\Aadi\pyspark>

(venv) (base) C:\Users\Aadi\pyspark>deactivate
(base) C:\Users\Aadi\pyspark>