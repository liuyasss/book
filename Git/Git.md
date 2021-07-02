## Git

```shell
# 增加tag
git tag -a v1.02.03 -m "version 1.02.03;add print"
git push [origin] --tags

# 删除tag
git tag -d [tag]
git push origin :refs/tags/v1.11.01

# tag
# 关于tag的时间操作
git log --tags --decorate --simplify-by-decoration 
git log --tags --simplify-by-decoration --pretty="format:%d - %cr" 
```



