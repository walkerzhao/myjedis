# jedis 源码学习
* 使用jedis,增删改查;
* 了解jedis的基本原理,连接池特性;
* jedis的接口封装,以及spring 对于jedis的进一步封装;
* 对于一般client端的封装思路,比如dcache,同步/异步处理等等;

# jedis连接池学习
## 连接池创建--JedisPool
* Jedis对象缓存到common-pool2中的对象池;
* jedisPool的构建过程:借助JedisFactory 工厂类去管理对象:创建/销毁/激活/有效性校验;
* JedisFactory实现了PooledObjectFactory接口,通过接口实现的方式,实现了解耦,自己的东西自己去实现,common pool不侵入任何逻辑;


## 连接池参数设置
jedis的连接池:JedisPoolConfig, 继承GenericObjectPoolConfig
* maxActive,池中最多多少个实例;
* maxIdle,池中最多有多少个空闲的jedis实例;
* whenExhaustedAction,当池中都被分配完的时候,采取的行为:抛异常/阻塞住或者到maxWait时抛出异常/新建jedis实例,maxActive无效;
* maxWait,申请一个jedis实例时候的最大等待时间;
* testOnBorrow, 提前进行validate的操作,保证borrow的时候,是可用的;
* testOnReturn
* testWhileIdle,扫描线程对空闲线程进行扫描,做移除操作;
* timeBetweenEvictionRunsMillis, 扫描的间隔时间时间;

## 对象实例化
* jedis对象的实例化:JedisFactory.makeObject

## 获取连接 & 归还连接
* getResource
* returnResource,这个方法在jedis 3.0将被废弃掉,使用 jedis.close即可.


# common pool源码学习
* common pool是apache的一个对象池化的组件.
* 几个概念:对象池(容器);对象池工厂(管理对象池);池对象(具体需要管理的对象,比如jedis对象);池对象工厂(管理池对象的);
* 有空可以和druid的连接池做对比;
https://blog.csdn.net/u011784767/article/details/78337448
https://blog.csdn.net/qq447995687/article/details/80233621



# redis协议
redis client和server端的交互息协议可以参考:https://www.cnblogs.com/smark/p/3247620.html

# redis性能压测
* redis benchmark压测工具:https://blog.csdn.net/zlfprogram/article/details/74338685


# 准备
* 本机安装启动redis_server&并使用redis_client去连接测试数据;
* 单步调试代码,了解jedis的运行流程;


# 疑问
* jedis的连接池是如何实现的?
* 每次使用都重新获取吗, 多个线程的操作可以共用吗,是否有线程安全问题?
* redis是否支持异步操作?
* 如何做全面的压测?


# 参考
* jedis源码剖析:https://www.jianshu.com/p/dcf1491afbe7