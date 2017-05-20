# Redis使用手册
关于redis的介绍，可以参考：www.redis.cn

## 目录
- [下载与安装](#downloadAndInstall)
    - [普通安装与可能出现的问题](#normalinstall)
    - [集群安装](#clusterInstall)


## <a name="downloadAndInstall">下载与安装</a>
### <a name="normalinstall">普通安装与可能出现的问题</a>
下载很简单，去官网下载即可。

安装：
```
tar -zxf <安装包>
cd <redis目录>
make
```

启动：安装包目录执行命令
```
./src/redis-server
```
上述方法启动以后，终端退出则redis退出。
后台方式启动：
```
vi <redis目录>/redis.conf
在命令模式下输入『/daemonize』,找到 daemonize no 这一行，将no改成yes
```

<span style="color: red;">安装时候可能出现的问题：</span>
异常一：make[2]: cc: Command not found
异常原因：没有安装gcc
解决方案：yum install gcc-c++

异常二：zmalloc.h:51:31: error: jemalloc/jemalloc.h: No such file or directory
异常原因：一些编译依赖或原来编译遗留出现的问题
解决方案：make distclean。清理一下，然后再make。
在make成功以后，需要make test。在make test出现异常。

异常三：couldn't execute "tclsh8.5": no such file or directory
异常原因：没有安装tcl
解决方案：yum install -y tcl。

### <a name="clusterInstall">集群安装</a>
#### 1. 修改配置
修改redis.conf文件
```
port 7000  
bind redis所在服务器IP地址
cluster-enabled yes  
cluster-config-file nodes.conf  
cluster-node-timeout 5000  
appendonly yes
```
然后将整个redis目录拷贝到其他服务器上去，<span style="color: red;">并修改配置文件中的bind参数，值为redis所在服务器IP地址</span>

#### 2. 安装ruby环境
该环境是搭建redis集群的必须环境，是官方推荐的使用方式。
选取任意一台redis服务器进行搭建即可。但是注意，以后关于集群的搭建操作都要在这台服务器上。
```
yum install ruby
yum install rubygems
gem install redis
```
mac系统可以使用brew安装
```
brew install ruby
这时候，rubygems也会被安装，直接执行gem install redis即可
```

#### 3. 安装集群
##### 3.1 启动所有的redis服务器
##### 3.2 所有redis服务器开放6379和16379端口
##### 3.3 执行命令
```
./redis_home/src/redis-trib.rb create --replicas 0 192.168.0.34:6379 192.168.0.35:6379 192.168.0.36:6379
```
上述0代表数据块备份数，如果没有slave，则设置0
后面的参数是所有redis服务器的IP地址与6379端口号。端口号可以自己在redis.conf文件中定义。默认为6379。
<span style="font-weight: bold; color: red;">执行完该命令后，以后redis服务器启动自动就会以集群方式启动。</span>

