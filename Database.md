# 基礎數據類型之: String
單個string類型的儲存空間為512MB
## string基本操作
* 添加或修改數據：set key value
* 獲取數據：get key
* 刪除數據：del key
* 添加/修改多個數據：mset key1 value1 key2 value2...
* 獲取多個數據：mget key1 key2 ...

# 基礎數據類型之：Hash
* 儲存需求： 對一系列儲存的數據進行編排，方便管理，典型應用儲存對象信息
* 儲存結構：一個儲存空間儲存多個鍵值對數據
* hash類型：底層使用`哈希表結構`實現數據儲存
## hash儲存結構優化
* 如果field數量較少，儲存結構優化為類數組結構
* 如果field數量較多，儲存結構使用HashMap結構
### hash類型基本操作
* 添加/修改數據：hset key field value
* 獲取數據：
1. hget key field
2. hgetall key
* 刪除數據：hdel key field [field2]...
* 添加或刪除多個數據：hmset key field1 value1 field2 value2 ...
* 獲取多個數據：hmget key field1 field2...
* 如果key值下的field存在則不做操作，不存在則添加進去：hsetnx key field value

# 基礎數據類型之：list
* 數據儲存需求：儲存多個數據，並對數據進入儲存最關鍵的順序進行區分
* 需要的儲存結構：一個儲存空間儲存多個數據，並且數據可以體現進入順序
* list類型：保存多個數據，底層使用雙向鍊表儲存結構實現
## list基本操作
* 添加/修改數據：
1. lpush key value1 value2 [value3] ... //從list鍊表左側添加 
2. rpush key value1 value2 [value3] ... //從list右側添加
* 獲取數據：lrange key start stop //指定鍊表起始結束位置中的value
* //在獲取未知長的的list類型的時候，想查看所有的value可以使用 -1表示倒數第一個：lrange key start -1 
* lindex key index //獲取鍊表中指定位置的值 
* llen key //獲取鍊表的長度
* 獲取並移除數據： 
1. lpop key
2. rpop key
* 移除指定數據：lrem key count value

# 基礎數據類型之：set
* 儲存需求：儲存大量的數據，在`查詢`方面提供更高的效率
* 儲存結構：能夠保存大量的數據，高效的內部儲存機制，便於查詢
* set類型：與hash儲存結構完全相同，僅儲存鍵，不儲存值（nil）,並且值不允許為空
## set基本操作
* 添加不重複的數據：sadd key value
* 獲取儲存的所有數據：smembers key
* 刪除數據：strem key member1 [member2]
* 獲取集合數據總量：scard key
* 判斷集合中是否包含指定數據：sismember key member
* 隨機獲取集合中指定數量的數據：srandmember key [count]

# 基礎數據類型：sortedSet
* 儲存需求：數據排序有利於數據的展示效果，需要提供一種可以根據自身特徵進行排序的方式
* 儲存結構：可以保存排序的數據
* 儲存類型：在set的儲存結構上添加可排序欄位
## sortedSet基本操作
* 添加數據：zadd key scorel member [score2 member2]
* 獲取全部數據： 
1. zrange key start stop [witchscores]
2. zrevrange key star stop [witchscores]
* 刪除數據：zrem key member [member ...]
* 按條件查詢數據：
1. zrangebyscore key min max [withscores] [limit] 
2. zrevrangebyscore key max min [withscores]
* 條件刪除數據：zremrangebyrank key start stop //start stop 表示索引的開始結束位置
* zremrangebyscore key min max //min max表示排序的最小到最大位置
* 獲取集合數據數量：
1. zcard key
2. zcount key min max

# Redis特性
* 速度快
> Redis使用標準C編寫實現，而且將所有數據加載到內存中，所以速度非常快。官方提供的數據表明，在一個普通的Linux機器上，Redis讀寫速度分別達到81000 / s和110000 / s。
***
* 數據結構
> 可以將Redis看做`數據結構服務器`，目前Redis支持5種數據結構。
***
* 持久化
> 由於所有數據保持在內存中，所以對數據的更新將初始地保存到磁盤上，Redis提供了一些策略來保存數據，根據時間或更新次數。數據超過了內存，使用了swap保存數據。
`memcacache`無法持久化，`mongo`是部分在內存。
***
* 自動操作
> Redis對不同數據類型的操作是自動的，因此設置或增加鍵值，從一個集合中增加或刪除一個元素都能安全的操作。
***
* 支持多種語言
> Redis支持多種語言，例如：`Ruby、Python、Twisted、Python、PHP、Erlang、Tcl、Perl、Lua、Java、Scala、Clojure`...等。
***
* 主-從復制
> Redis支持簡單而快速的主-從復制。官方提供了一個數據，Slave在21秒即完成了對Amazon網站10Gkey set的複制。
***
* Sharding
> 很容易將數據分佈到多個Redis實例中，而主要看該語言是否支持。目前支持Sharding功能的語言只有PHP，Ruby和Scala。

* [Redis基本操作](https://kknews.cc/code/oke3a2o.html)
* [Python連接至資料庫的方法](https://kknews.cc/zh-tw/code/5vyo8y8.html)
* [Android Studio連接至資料庫的方法](https://mnya.tw/cc/word/1480.html)