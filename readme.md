# jedis 源码学习
* 使用jedis,增删改查;
* 了解jedis的基本原理,连接池特性;
* jedis的接口封装,以及spring 对于jedis的进一步封装;
* 对于一般client端的封装思路,比如dcache,同步/异步处理等等;

# jedis连接池学习
## 连接池创建--JedisPool
Jedis对象缓存到common-pool2中的对象池;


## 连接池参数设置
jedis的连接池:JedisPoolConfig, 继承GenericObjectPoolConfig
* maxActive,池中最多多少个实例;
* maxIdle,池中最多有多少个空闲的jedis实例;
* whenExhaustedAction,当池中都被分配完的时候,采取的行为:抛异常/阻塞住或者到maxWait时抛出异常/新建jedis实例,maxActive无效;
* maxWait,申请一个jedis实例时候的最大等待时间;
* testOnBorrow,

* jedis对象的实例化:JedisFactory.makeObject
* 获取连接 & 归还连接;
* 每次使用都重新获取吗?

# 准备
* 本机安装启动redis_server&并使用redis_client去连接测试数据;
* 单步调试代码,了解jedis的运行流程;


# 疑问
* jedis的连接池是如何实现的?


# 参考
* jedis源码剖析:https://www.jianshu.com/p/dcf1491afbe7