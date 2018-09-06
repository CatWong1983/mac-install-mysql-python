# mac-install-mysql-python
**在mac上安装mysql-python遇到了很多问题， 并且可能同样的安装流程在不同电脑有不同的错误， 
对此进行一个简单的记录，不一定适用所有人，但希望可以供大家有个参考**

1. 在安装MySQL- python之前先确定有没有安装mysql，运行下列代码
```
which mysql
```
如果有mysql的路径， 则进行下一步，如果没有则运行
```
brew install mysql
which mysql
```
如果还是找不到mysql路径，点击链接下载安装https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.12-macos10.13-x86_64.dmg

2. 执行
```
export PATH=$PATH:/usr/local/mysql/bin
```
3. 执行
```
sudo pip install MySQL-python
```
**报错：error：commond ‘cc' failed with exit status 1** 

4.执行
```
brew unlink mysql
brew isntall mysql-connector-c
```
如果报错
```
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink bin/mysql_config
Target /usr/local/bin/mysql_config
already exists. You may want to remove it:
  rm '/usr/local/bin/mysql_config'
```
再执行
```
rm '/usr/local/bin/mysql_config'
brew install mysql-connector-c
```

5. 执行
```
sed -i -e 's/libs="$libs -l "/libs="$libs -lmysqlclient -lssl -lcrypto"/g' /usr/local/bin/mysql_config
sudo pip install MySQL-python
```
如果报错：
```
error: [Errno 13] Permission denied: '/Library/Python/2.7/site-packages/_mysql.so'
```
执行：
```
sudo chown -R $USER /Library/Python/2.7
```
再执行：
```
sudo pip install MySQL-python
```
最后总结一下，必要的前置条件就是mysql，安装完mysql后我们借助mysql-connector-c来进行后续的安装，最后解决文件权限的问题（权限问题不一定谁都会遇到， 我在安装第二次的时候就没有遇到）。
