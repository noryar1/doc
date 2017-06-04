# mysql安装文档

## 目录
- [mac安装](#mac)


## <a name="mac">mac安装</a>
### 常规安装
1. 安装版本: mysql-5.7.18-macos10.12-x86_64.dmg
2. 安装方式: 无脑下一步安装
3. 在偏好设置中启动/关闭mysql服务

### 自定义安装
1. 重复上述步骤1和步骤2
2. 进入安装目录: ``cd /usr/local/mysql``，该目录是软连接，具体目录在/usr/local/mysql-版本-xxx目录
3. 自定义my.cnf文件
```shell
sudo cd /etc
sudo touch my.cnf
sudo vi my.cnf
```
然后加入下面的文件内容<a href="my.cnf" target="_blank">my.cnf</a>
4. 初始化MySQL 
```shell
cd /usr/local
chown -R MAC用户名:staff mysql*
cd /usr/local/mysql
./bin/mysqld --initialize --user=mac --datadir=/usr/local/mysql/data --basedir=/usr/local/mysql/
```
   这个时候命令行会提示随机的密码，然后使用这个密码登入MySQL
```
cd bin
mysql -uroot -p
输入密码，回车
SET PASSWORD = PASSWORD('root');
ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
FLUSH PRIVILEGES;
```
5. 启动/关闭mysql
   mysql目录下的support-files目录下有mysql.server，可以通过``./support-files/mysql.server start``
   或``./supprot-files/mysql.server stop``进行启动或关闭操作。
