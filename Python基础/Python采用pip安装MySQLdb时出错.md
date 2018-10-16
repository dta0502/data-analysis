# Python采用pip安装MySQLdb时出错

## 问题1

首先我采用pip安装：

```bash
pip install MySQLdb
```

结果出现以下错误：

```bash
Could not find a version that satisfies the requirement MySQLdb (from versions:)No matching distribution found for MySQLdb
```
## 解决方法

参考：[Error Loading MySQLdb Module and “pip install MySQLdb”](https://stackoverflow.com/questions/34030215/error-loading-mysqldb-module-and-pip-install-mysqldb)

```
Clearly installing pip install MySQL-python is the way to go. The problem is with the location of mysql_config.
```

## 问题2

根据以上解决方法：

```bash
pip install MySQL-python
```

结果出现以下错误：

```
Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-install-vnuxly73/MySQL-python/
```

## 解决办法

参考：[“pip install unroll”: “python setup.py egg_info” failed with error code 1](https://stackoverflow.com/questions/35991403/pip-install-unroll-python-setup-py-egg-info-failed-with-error-code-1)

升级以下pip：

```bash


python -m pip install --upgrade pip
pip install "package-name"
```

然后对`MySQL-python`进行pip安装即可：

```bash
pip install MySQL-python
```

