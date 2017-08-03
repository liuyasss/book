## MongoDB 相关

- Ubuntu 下的安装和使用

```
http://blog.csdn.net/flyfish111222/article/details/51886787
```

- 查看版本

```sql
mongo -version
```

- 启动和关闭mongodb命令如下：

```sql
service mongodb start
service mongodb stop
```

- 默认设置MongoDB是随Ubuntu启动自动启动的。输入以下命令查看是否启动成功：

```
pgrep mongo -l   #注意：-l是英文字母l，不是阿拉伯数字1
```

- 卸载MongoDB

```
sudo apt-get --purge remove mongodb mongodb-clients mongodb-server
```

