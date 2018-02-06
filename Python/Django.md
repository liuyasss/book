- 安装 mysql 的过程中出现 `OSError: mysql_config not found`,解决办法

  1. 安装libmysqlclient-dev包即可，如果还有问题，可以安装python-dev。

  ```
  apt-get install libmysqlclient-dev python3-dev
  ```

  2. 执行`sudo pip  install mysqlclient `  

