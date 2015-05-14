---
layout: post
title: "redis"
description: ""
category: 技术分享
tags: [redis]
---
{% include JB/setup %}
# 搭建Redis以及使用
---

####Redis的安装

* 在官网下载tar.gz的文件，并且解压，进入解压目录，执行 make&&make install，在make成功以后，会在src目录下多出一些可执行文件：redis-server，redis-cli等等。

* 用cp命令复制到usr目录下运行。

>cp redis-server /usr/local/bin/

>cp redis-cli /usr/local/bin/

* 新建目录，存放配置文件

<!--break-->

>mkdir /etc/redis

>mkdir /var/redis

>mkdir /var/redis/log

>mkdir /var/redis/run

>mkdir /var/redis/6379

* 在redis解压根目录中找到配置文件模板，复制到如下位置。

>cp redis.conf /etc/redis/6379.conf

* 因为在etc目录下文件只读，所以建议先在其他目录更改conf文件，然后在cp到redis

>daemonize yes

>pidfile /var/redis/run/redis_6379.pid

>logfile /var/redis/log/redis_6379.log

>dir /var/redis/6379

* 最后运行redis：

>```$ redis-server /etc/redis/6379.conf```

* 启动redis-cli：

>```/usr/local/bin/redis-cli```

####命令示例

* 1. KEYS/RENAME/DEL/EXISTS/MOVE/RENAMENX:

#####在Shell命令行下启动Redis客户端工具。

> /> redis-cli

#####清空当前选择的数据库，以便于对后面示例的理解。

>    redis 127.0.0.1:6379> flushdb

>    OK
 
#####添加String类型的模拟数据。

>    redis 127.0.0.1:6379> set mykey 2
 
>   OK
 
>   redis 127.0.0.1:6379> set mykey2 "hello"

>    OK
 
#####添加Set类型的模拟数据。
 
>   redis 127.0.0.1:6379> sadd mysetkey 1 2 3
 
>   (integer) 3
 
#####添加Hash类型的模拟数据。

>    redis 127.0.0.1:6379> hset mmtest username "stephen"
 
>   (integer) 1
 
#####根据参数中的模式，获取当前数据库中符合该模式的所有key，从输出可以看出，该命令在执行时并不区分与Key关联的Value类型。

>    redis 127.0.0.1:6379> keys my*
 
>   1) "mysetkey"

>    2) "mykey"

>    3) "mykey2"

#####删除了两个Keys。
 
>   redis 127.0.0.1:6379> del mykey mykey2
 
>   (integer) 2
 
#####查看一下刚刚删除的Key是否还存在，从返回结果看，mykey确实已经删除了。
 
>   redis 127.0.0.1:6379> exists mykey
 
>   (integer) 0

#####查看一下没有删除的Key，以和上面的命令结果进行比较。
 
>   redis 127.0.0.1:6379> exists mysetkey

>    (integer) 1
 
#####将当前数据库中的mysetkey键移入到ID为1的数据库中，从结果可以看出已经移动成功。

>    redis 127.0.0.1:6379> move mysetkey 1
 
>   (integer) 1
#####打开ID为1的数据库。

>   redis 127.0.0.1:6379> select 1
 
>   OK
 
#####查看一下刚刚移动过来的Key是否存在，从返回结果看已经存在了。

>    redis 127.0.0.1:6379[1]> exists mysetkey
 
>   (integer) 1
 
#####在重新打开ID为0的缺省数据库。

>    redis 127.0.0.1:6379[1]> select 0
 
>   OK
 
#####查看一下刚刚移走的Key是否已经不存在，从返回结果看已经移走。

>    redis 127.0.0.1:6379> exists mysetkey
 
>   (integer) 0
 
#####准备新的测试数据。    
    
>    redis 127.0.0.1:6379> set mykey "hello"
 
>   OK
    
#####将mykey改名为mykey1
    
>    redis 127.0.0.1:6379> rename mykey mykey1
    
>    OK
    
#####由于mykey已经被重新命名，再次获取将返回nil。

>    redis 127.0.0.1:6379> get mykey

>    (nil)

#####通过新的键名获取。

>    redis 127.0.0.1:6379> get mykey1
 
>   "hello"

#####由于mykey已经不存在了，所以返回错误信息。

>    redis 127.0.0.1:6379> rename mykey mykey1

>    (error) ERR no such key

#####为renamenx准备测试key

>    redis 127.0.0.1:6379> set oldkey "hello"

>    OK

>    redis 127.0.0.1:6379> set newkey "world"

>    OK

#####由于newkey已经存在，因此该命令未能成功执行。

>    redis 127.0.0.1:6379> renamenx oldkey newkey

>    (integer) 0

#####查看newkey的值，发现它也没有被renamenx覆盖。

>    redis 127.0.0.1:6379> get newkey

>    "world"
       
* 2. PERSIST/EXPIRE/EXPIREAT/TTL:   
 
#####为后面的示例准备的测试数据。
    
>    redis 127.0.0.1:6379> set mykey "hello"

>    OK

#####将该键的超时设置为100秒。

>    redis 127.0.0.1:6379> expire mykey 100
 
>   (integer) 1
#####通过ttl命令查看一下还剩下多少秒。

>    redis 127.0.0.1:6379> ttl mykey

>    (integer) 97

#####立刻执行persist命令，该存在超时的键变成持久化的键，即将该Key的超时去掉。

>    redis 127.0.0.1:6379> persist mykey
 
>    (integer) 1
#####ttl的返回值告诉我们，该键已经没有超时了。
    
>    redis 127.0.0.1:6379> ttl mykey
    
>    (integer) -1

#####为后面的expire命令准备数据。
    
>    redis 127.0.0.1:6379> del mykey

>    (integer) 1

>    redis 127.0.0.1:6379> set mykey "hello"

>    OK

#####设置该键的超时被100秒。
    
>    redis 127.0.0.1:6379> expire mykey 100
    
>    (integer) 1

#####用ttl命令看一下当前还剩下多少秒，从结果中可以看出还剩下96秒。

>    redis 127.0.0.1:6379> ttl mykey

>    (integer) 96

#####重新更新该键的超时时间为20秒，从返回值可以看出该命令执行成功。

>    redis 127.0.0.1:6379> expire mykey 20

>    (integer) 1

#####再用ttl确认一下，从结果中可以看出果然被更新了。

>    redis 127.0.0.1:6379> ttl mykey

>    (integer) 17

#####立刻更新该键的值，以使其超时无效。

>    redis 127.0.0.1:6379> set mykey "world"
 
>    OK

#####从ttl的结果可以看出，在上一条修改该键的命令执行后，该键的超时也无效了。

>    redis 127.0.0.1:6379> ttl mykey

>    (integer) -1

* 3. TYPE/RANDOMKEY/SORT:

#####由于mm键在数据库中不存在，因此该命令返回none。

>    redis 127.0.0.1:6379> type mm
 
>    none

#####mykey的值是字符串类型，因此返回string。
    
>    redis 127.0.0.1:6379> type mykey

>    string

#####准备一个值是set类型的键。
    
>    redis 127.0.0.1:6379> sadd mysetkey 1 2
   
>    (integer) 2
    
#####mysetkey的键是set，因此返回字符串set。

>    redis 127.0.0.1:6379> type mysetkey
 
>    set

#####返回数据库中的任意键。

>    redis 127.0.0.1:6379> randomkey

>    "oldkey"
#####清空当前打开的数据库。
    
>    redis 127.0.0.1:6379> flushdb
    
>    OK

#####由于没有数据了，因此返回nil。
    
>    redis 127.0.0.1:6379> randomkey
    
>    (nil)
