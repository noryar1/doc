# Redis使用手册
关于redis的介绍，可以参考：www.redis.cn


## 目录
- [简介](#introduction)
    - [redis是什么](#whatis)
- [下载与安装](#downloadAndInstall)
    - [普通安装与可能出现的问题](#normalinstall)
    - [集群安装](#clusterInstall)
- [基本配置](#config)
- [监控](#monitor)
    - [redis live](#redis-live)
    - [redis stat](#redis-stat)

## <a name = "introduction">简介</a>
### <a name = "whatis">redis是什么</a>
Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统。

用途：
1. 数据库。
2. 缓存。
3. 消息中间件

支持的数据类型:
1. 字符串(String)。
2. 散列(hash)。
3. 列表(lists)。
4. 集合(sets)。
5. 有序集合(sorted sets)与范围查询。
6. bitmaps。
7. hyperloglogs
8. 地理空间(geospatial)索引半径查询。

## <a name="downloadAndInstall">下载与安装</a>
### <a name="normalinstall">普通安装与可能出现的问题</a>
下载很简单，去官网下载即可。

#### 安装：
```
tar -zxf <安装包>
cd <redis目录>
make
```

#### 启动：安装包目录执行命令
```
./src/redis-server
```
上述方法启动以后，终端退出则redis退出。
后台方式启动：
```
vi <redis目录>/redis.conf
在命令模式下输入『/daemonize』,找到 daemonize no 这一行，将no改成yes
```

#### 安装时候可能出现的问题
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

#### 4. 集群安装中可能出现的问题
redis集群创建执行一直等待 <span style="color: red;">Waiting for the cluster to join</span>很久都没有反应
原因：
redis集群不仅需要开通redis客户端连接的端口，而且需要开通集群总线端口
集群总线端口为redis客户端连接的端口 + 10000
如redis端口为6379
则集群总线端口为16379
故，所有服务器的点需要开通redis的客户端连接端口和集群总线端口
注意：iptables 放开，如果有安全组，也要放开这两个端口

[ERR] Node XXXXXX is not empty. Either the node already knows other nodes (check with CLUSTER NODES) or contains some key in database 0
解决方法是删除生成的配置文件nodes.conf，如果不行则说明现在创建的结点包括了旧集群的结点信息，需要删除redis的持久化文件后再重启redis，比如：appendonly.aof、dump.rdb


## <a name = "config">基本配置</a>
redis.conf 配置项说明如下：

1. Redis默认不是以守护进程的方式运行，可以通过该配置项修改，使用yes启用守护进程
```
    daemonize no
```
2. 当Redis以守护进程方式运行时，Redis默认会把pid写入/var/run/redis.pid文件，可以通过pidfile指定
```
    pidfile /var/run/redis.pid
```
3. 指定Redis监听端口，默认端口为6379，作者在自己的一篇博文中解释了为什么选用6379作为默认端口，因为6379在手机按键上MERZ对应的号码，而MERZ取自意大利歌女Alessia Merz的名字
```
    port 6379
```
4. 绑定的主机地址
```
    bind 127.0.0.1
```
5. 当客户端闲置多长时间后关闭连接，如果指定为0，表示关闭该功能
```
    timeout 300
```
6. 指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为verbose
```
    loglevel verbose
```
7. 日志记录方式，默认为标准输出，如果配置Redis为守护进程方式运行，而这里又配置为日志记录方式为标准输出，则日志将会发送给/dev/null
```
    logfile stdout
```
8. 设置数据库的数量，默认数据库为0，可以使用SELECT <dbid>命令在连接上指定数据库id
```
    databases 16
```
9. 指定在多长时间内，有多少次更新操作，就将数据同步到数据文件，可以多个条件配合
```
    save <seconds> <changes>
    Redis默认配置文件中提供了三个条件：
    save 900 1
    save 300 10
    save 60 10000
    分别表示900秒（15分钟）内有1个更改，300秒（5分钟）内有10个更改以及60秒内有10000个更改。
```
10. 指定存储至本地数据库时是否压缩数据，默认为yes，Redis采用LZF压缩，如果为了节省CPU时间，可以关闭该选项，但会导致数据库文件变的巨大
```
    rdbcompression yes
```
11. 指定本地数据库文件名，默认值为dump.rdb
```
    dbfilename dump.rdb
```
12. 指定本地数据库存放目录
```
    dir ./
```
13. 设置当本机为slav服务时，设置master服务的IP地址及端口，在Redis启动时，它会自动从master进行数据同步
```
    slaveof <masterip> <masterport>
```
14. 当master服务设置了密码保护时，slav服务连接master的密码
```
    masterauth <master-password>
```
15. 设置Redis连接密码，如果配置了连接密码，客户端在连接Redis时需要通过AUTH <password>命令提供密码，默认关闭
```
    requirepass foobared
```
16. 设置同一时间最大客户端连接数，默认无限制，Redis可以同时打开的客户端连接数为Redis进程可以打开的最大文件描述符数，如果设置 maxclients 0，表示不作限制。当客户端连接数到达限制时，Redis会关闭新的连接并向客户端返回max number of clients reached错误信息
```
    maxclients 128
```
17. 指定Redis最大内存限制，Redis在启动时会把数据加载到内存中，达到最大内存后，Redis会先尝试清除已到期或即将到期的Key，当此方法处理 后，仍然到达最大内存设置，将无法再进行写入操作，但仍然可以进行读取操作。Redis新的vm机制，会把Key存放内存，Value会存放在swap区
```
    maxmemory <bytes>
```
18. 指定是否在每次更新操作后进行日志记录，Redis在默认情况下是异步的把数据写入磁盘，如果不开启，可能会在断电时导致一段时间内的数据丢失。因为 redis本身同步数据文件是按上面save条件来同步的，所以有的数据会在一段时间内只存在于内存中。默认为no
```
    appendonly no
```
19. 指定更新日志文件名，默认为appendonly.aof
```
    appendfilename appendonly.aof
```
20. 指定更新日志条件，共有3个可选值： 
```
    no：表示等操作系统进行数据缓存同步到磁盘（快） 
    always：表示每次更新操作后手动调用fsync()将数据写到磁盘（慢，安全） 
    everysec：表示每秒同步一次（折衷，默认值）
    appendfsync everysec
```
21. 指定是否启用虚拟内存机制，默认值为no，简单的介绍一下，VM机制将数据分页存放，由Redis将访问量较少的页即冷数据swap到磁盘上，访问多的页面由磁盘自动换出到内存中（在后面的文章我会仔细分析Redis的VM机制）
```
    vm-enabled no
```
22. 虚拟内存文件路径，默认值为/tmp/redis.swap，不可多个Redis实例共享
```
    vm-swap-file /tmp/redis.swap
```
23. 将所有大于vm-max-memory的数据存入虚拟内存,无论vm-max-memory设置多小,所有索引数据都是内存存储的(Redis的索引数据 就是keys),也就是说,当vm-max-memory设置为0的时候,其实是所有value都存在于磁盘。默认值为0
```
    vm-max-memory 0
```
24. Redis swap文件分成了很多的page，一个对象可以保存在多个page上面，但一个page上不能被多个对象共享，vm-page-size是要根据存储的 数据大小来设定的，作者建议如果存储很多小对象，page大小最好设置为32或者64bytes；如果存储很大大对象，则可以使用更大的page，如果不 确定，就使用默认值
```
    vm-page-size 32
```
25. 设置swap文件中的page数量，由于页表（一种表示页面空闲或使用的bitmap）是在放在内存中的，，在磁盘上每8个pages将消耗1byte的内存。
```
    vm-pages 134217728
```
26. 设置访问swap文件的线程数,最好不要超过机器的核数,如果设置为0,那么所有对swap文件的操作都是串行的，可能会造成比较长时间的延迟。默认值为4
```
    vm-max-threads 4
```
27. 设置在向客户端应答时，是否把较小的包合并为一个包发送，默认为开启
```
    glueoutputbuf yes
```
28. 指定在超过一定的数量或者最大的元素超过某一临界值时，采用一种特殊的哈希算法
```
    hash-max-zipmap-entries 64
    hash-max-zipmap-value 512
```
29. 指定是否激活重置哈希，默认为开启（后面在介绍Redis的哈希算法时具体介绍）
```
    activerehashing yes
```
30. 指定包含其它的配置文件，可以在同一主机上多个Redis实例之间使用同一份配置文件，而同时各个实例又拥有自己的特定配置文件
```
    include /path/to/local.conf
```


## <a name = "monitor">监控</a>
### <a name = "redis-live">redis live</a>
该方案使用monitor实现，对性能会有影响。

### <a name = "redis-stat">redis stat</a>
该方案使用『info』实现，对性能影响小。
redis stat是韩国人写的，github地址：https://github.com/junegunn/redis-stat