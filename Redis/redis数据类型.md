## string

#### 添加

[添加单个](redis6.0.5.tar.gz)：

语法：set key value [expiraion EX seconds|PX milliseconds] [NX|XX]

解析：添加数据的同时设置数据的有效期EX表示以秒为单位PX表示以毫秒为单位

语法：setex key seconds value

解析：添加数据同时设置有效期

语法：psetex key millisseconds value

解析：添加数据的同时设置有效期

[添加多个](redis6.0.5.tar.gz)：

语法：mset key1 value1 key2 value2 [key value ...]

实例：mset name1 zhangsan name2 lishi

[追加](redis6.0.5.tar.gz)：

语法：append key value

返回值：追加后value的字符长度

[数值](redis6.0.5.tar.gz)：

[+1](redis6.0.5.tar.gz)	语法：incr key

返回值：+1后的值

[+2](redis6.0.5.tar.gz) 语法：incrby key decrement

解析decrement	要加的数值

实例：年龄增加：incr age

[+0.5](redis6.0.5.tar.gz) 语法：incrbyfloat key increment

[-1](redis6.0.5.tar.gz) 语法：decr key

返回值：-1执行后的值

-[2](redis6.0.5.tar.gz)	语法：decrby key decrement

解析decrement	要减去的数值

[说明](redis6.0.5.tar.gz)：incrby 与 decrby用于操作自定义数值，具体时加操作或者时减操作，主要取决与操作数值的正副形

[说明](redis6.0.5.tar.gz)：执行set key value 命令时，如果当前key已经存在则覆盖

#### 查询

[查询单个](redis6.0.5.tar.gz)：

语法：get key

[查询多个](redis6.0.5.tar.gz)：

语法：mget key1 key2 [key ...]

实例：mget name1 name2

[查询全部](redis6.0.5.tar.gz)：

语法：keys *

[查询value长度](redis6.0.5.tar.gz)：

语法：strlen key

#### 删除

[删除](redis6.0.5.tar.gz)：

语法：del key1 key2 [key ...]

## hash

#### 添加

[添加单个](redis6.0.5.tar.gz)：

语法：hset key filed value [filed value ...]

解析：filed字段value属性

[添加多个](redis6.0.5.tar.gz)：

语法：hmset key filed value

解析：filed字段value属性

[判断是否存在后再添加](redis6.0.5.tar.gz)：

语法：hsetnx key  filed value

作用：如果当前filed值存在，则不操作，反之则添加，返回值

返回值：0：false没有添加	1：true成功添加

#### 查询

[查询单个](redis6.0.5.tar.gz)：

语法：hget key filed

[查询多个](redis6.0.5.tar.gz)：

语法：hmget key filed [filed ...]

[查询字段数量](redis6.0.5.tar.gz)：

语法：hlen key

[查询hash中的所有数据](redis6.0.5.tar.gz)：

语法：hgetall key

返回值：所有filed和value，奇数为filed，偶数为

[查询所有filed值](redis6.0.5.tar.gz):

语法：hkeys key

[查询所有value值](redis6.0.5.tar.gz)：

语法：hvals key

#### 判断字段是否存在

语法：hexists key filed

返回值：0：false不存在	1：ture存在

#### 数值

[+1](redis6.0.5.tar.gz)	语法：hincrby key filed increment

数值：increment操作的数值

[+0.5](redis6.0.5.tar.gz)	语法：hincrbyfloat key filed increment

#### 删除

语法：hdel key filed [filed ...]

返回值：成功删除的个数

## List

从左边拿第一个：

语法：lpop key

从右边拿第一个：

语法：rpop key

从左边添加：

语法：lpush key element [element ...]

从右边添加：

语法：

#### 查询：

查询所有长度：

语法：lrange key staus stop

给定时间内，从左边多个数组一个一个取出：

语法：blpop key [key ...] timeout

#### 删除：

移除：语法：lrem key count value

​				解析：cout个数	value值

## set

去重

#### 添加：

添加多个成员：

语法：sadd key member [member ...]

解析：member成员 重复时返回值为没有的个数

#### 查询：

查询全部：set members

语法：smembers key 

查询成员长度：

语法：scard key

判断：

语法：sismember key member

解析：判断元素是否存在

随机查询元素：

语法：srandmember key [countman]

#### 取出

语法：spop key [count]

解析：count个数 随机取出元素

#### 交并差

交集和差集

[交集]()：

语法：sinter key [key ...]

解析：将指定集合列表进行比较，返回相同元素

[取得交集并添加到另一个集合]()：

语法：sinterstore destination key [key ...]

解析：将指定所有集合的交集并存储在destination集合中

 返回值：交集的个数

[并集]()：

语法：sunion key [key ...]

[取得并集并添加到另一个集合]()：

语法：sunionstore destination key [key ...]

[差集]()：

语法：sdiff key [key ...]

[取得差集并添加到另一个集合]()：

语法：sdiffstore destination key [key ...]

## sorted set

#### 添加

语法：zadd key  score member [score member ...]

解析：score排序序号 menber成员 

#### 查询

[升序查询]()：

语法：zrange key start stop [WITHSCORES]

解析：[WITHSCORES] 表示同时输出score和member的值，并默认按升序排序

[倒序查询]()：反转

语法：zrevrange key start stop [WITHSCORE]

[排序升序条件]()：sorted set by score

语法：zrangebyscore key min max [WITHSCORES] [LIMIT offset count]

解析：根据score升序查询，且score的取值在min和man之间min<score<max

​				WITHSCORES：同时查询输出score的值

​				LIMIT offset count：再次过滤从offset索引开始取count条

[排序倒序条件]()：sorted set by score

语法：zrevrangebybyscore key min max [WITHSCORES] [LIMIT offset count]

解析：根据score倒序查询，且score的取值在max和min之间max<score<min

​				WITHSCORES：同时查询输出score的值

​				LIMIT offset count：再次过滤从offset索引开始取count条

[查询个数]()：

语法：zcard key

[根据条件查询个数]()：

语法：zcount key min max

[索引顺序查询指定索引]()：

语法：zrank key member

[索引倒叙查询指定索引]()：

语法：zrevrank key member

[根据成员查询分数]()：

语法：zscore key member

#### 移除  remove

[根据成员来删除]()：

语法：zrem key member [member ..]

返回值：成功移除的个数

[根据分数条件来移除]()：

语法：zremrangebyscore key min max

[根据索引来删除]()：

语法：zremrangebyrank key start stop 

解析：根据索引删除从start到stop的元素

#### 交并差

[交集]()：

语法：zinterstore destination numkeys key [key ...] [WEIGHTS weight] [AGGREGATE SUM|MIN|MAX]

解析：取出交集并且保存到destination集合中，默认相同的score相加

​				numkeys：需要取出交集的个数

​				[AGGREGATE SUM|MIN|MAX]：SUM取score和 MIN取score最小 MAN取score最大

[并集]()：

语法：zunionstore destination numkeys key [key ...] [WEIGHTS weight] [AGGREGATE SUM|MIN|MAX]

解析：取出并集并且保存到destination集合中，默认相同的score相加

​				numkeys：需要取出并集的个数

​				[AGGREGATE SUM|MIN|MAX]：SUM取score和 MIN取score最小 MAN取score最大

#### 数值

语法：zincrby key increment member

解析；increment的值加到score

## 数据有效期

[设置指定key有效期	时间单位为秒]()：

语法：expire key seconds

返回值：-1：永久	-2key：不存在	0：失败	1：成功

[设置指定key有效期	时间单位为毫秒]()：

语法：pexpire key millseconds

返回值：-1：永久	-2key：不存在	0：失败	1：成功

## key基本操作

删除key：

del key

获取key的类型：

type key

判断key是否存在：

exists key [key ...]

查询key的有效期：



移除key的过期时间：



通配符匹配key：



匹配全部key：



匹配单个字符：



匹配指定列表符号：

