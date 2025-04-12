# Redis

In doubt, check the [cheat sheet](https://redis.io/learn/howtos/quick-start/cheat-sheet)

## Redis CLI

### General Commands

| Command      | Description                |
| ------------ | -------------------------- |
| DEL key      | Delete key                 |
| EXISTS key   | Check if key exists        |
| EXPIRE key   | seconds Set key expiration |
| TTL key      | Get remaining time to live |
| TYPE key     | Get key type               |
| KEYS pattern | Find keys matching pattern |
| FLUSHDB      | Clear current database     |
| FLUSHALL     | Clear all databases        |
| SELECT index | Select database            |
| INFO         | Get server information     |

### Strings

| Command                      | Description                |
| ---------------------------- | -------------------------- |
| SET key value                | Set a string value         |
| GET key                      | Get a string value         |
| MSET key1 value1 key2 value2 | Set multiple string values |
| MGET key1 key2               | Get multiple string values |
| INCR key                     | Increment number by 1      |
| DECR key                     | Decrement number by 1      |
| INCRBY key amount            | Increment by custom amount |
| DECRBY key amount            | Decrement by custom amount |
| STRLEN key                   | Get string length          |
| APPEND key value             | Append to string           |

### Lists

| Command               | Description                  |
| --------------------- | ---------------------------- |
| LPUSH key value       | Push element to head         |
| RPUSH key value       | Push element to tail         |
| LPOP key              | Remove and get first element |
| RPOP key              | Remove and get last element  |
| LLEN key              | Get list length              |
| LRANGE key start stop | Get range of elements        |
| LINDEX key index      | Get element by index         |
| LSET key index value  | Set element at index         |
| LTRIM key start stop  | Trim list to specified range |
| LREM key count value  | Remove elements by value     |

### Sets

| Command              | Description                     |
| -------------------- | ------------------------------- |
| SADD key member      | Add member to set               |
| SREM key member      | Remove member from set          |
| SMEMBERS key         | Get all members                 |
| SISMEMBER key member | Check if member exists          |
| SCARD key            | Get set size                    |
| SINTER key1 key2     | Intersection between sets       |
| SUNION key1 key2     | Union between sets              |
| SDIFF key1 key2      | Difference between sets         |
| SPOP key             | Remove and return random member |
| SRANDMEMBER key      | Get random member               |

### Sorted Sets

| Command                      | Description                  |
| ---------------------------- | ---------------------------- |
| ZADD key score member        | Add member with score        |
| ZREM key member              | Remove member                |
| ZRANGE key start stop        | Get range by index           |
| ZREVRANGE key start stop     | Get range by index, reversed |
| ZRANK key member             | Get rank of member           |
| ZREVRANK key member          | Get reverse rank of member   |
| ZSCORE key member            | Get score of member          |
| ZCOUNT key min max           | Count members in score range |
| ZINCRBY key increment member | Increment score of member    |
| ZRANGEBYSCORE key min max    | Get members by score range   |

### Hashes

| Command                               | Description               |
| ------------------------------------- | ------------------------- |
| HSET key field value                  | Set field value           |
| HGET key field                        | Get field value           |
| HMSET key field1 value1 field2 value2 | Set multiple fields       |
| HMGET key field1 field2               | Get multiple fields       |
| HGETALL key                           | Get all fields and values |
| HDEL key field                        | Delete field              |
| HEXISTS key field                     | Check if field exists     |
| HKEYS key                             | Get all fields            |
| HVALS key                             | Get all values            |
| HLEN key                              | Get number of fields      |

### Json

| Command          | Description                          | Example                                         |
| ---------------- | ------------------------------------ | ----------------------------------------------- |
| `JSON.SET`       | Set/replace JSON value               | `JSON.SET user:1 . '{"name":"John", "age":30}'` |
| `JSON.GET`       | Get JSON value                       | `JSON.GET user:1 .name`                         |
| `JSON.DEL`       | Delete a JSON value                  | `JSON.DEL user:1 .address`                      |
| `JSON.TYPE`      | Get the type of JSON value           | `JSON.TYPE user:1 .age`                         |
| `JSON.NUMINCRBY` | Increment a number value             | `JSON.NUMINCRBY user:1 .age 1`                  |
| `JSON.STRAPPEND` | Append to a string value             | `JSON.STRAPPEND user:1 .name " Doe"`            |
| `JSON.STRLEN`    | Get length of string value           | `JSON.STRLEN user:1 .name`                      |
| `JSON.ARRAPPEND` | Append to an array                   | `JSON.ARRAPPEND user:1 .hobbies '"reading"'`    |
| `JSON.ARRLEN`    | Get array length                     | `JSON.ARRLEN user:1 .hobbies`                   |
| `JSON.ARRPOP`    | Remove and return element from array | `JSON.ARRPOP user:1 .hobbies`                   |
| `JSON.OBJKEYS`   | Get object keys                      | `JSON.OBJKEYS user:1 .`                         |
| `JSON.OBJLEN`    | Get number of keys in object         | `JSON.OBJLEN user:1 .`                          |
| `JSON.TOGGLE`    | Toggle boolean value                 | `JSON.TOGGLE user:1 .active`                    |
| `JSON.CLEAR`     | Clear container value                | `JSON.CLEAR user:1 .hobbies`                    |
| `JSON.MGET`      | Get from multiple keys               | `JSON.MGET user:1 user:2 .name`                 |
| `JSON.FORGET`    | Alias for JSON.DEL                   | `JSON.FORGET user:1 .temp`                      |
| `JSON.RESP`      | Get JSON in RESP protocol            | `JSON.RESP user:1 .`                            |

Note:

- The `.` in the examples represents the root path
- You can use paths like `.name`, `.address.street`, `.hobbies[0]`
- Values must be valid JSON strings when setting
- Some commands require RedisJSON module to be installed

## Redis Python

```python
import redis

r = redis.Redis(host='localhost', port=6379, db=0)

r.keys()
r.keys('PATTERN:*')

r.scan_iter('PATTERN:*') # if number of keys is too large

r.delete('KEY')

for key in r.scan_iter('PATTERN:*'):
    r.delete(key)

r.expire('mykey', 10) # expire in 10 seconds
```

### Strings

| Command | Description                  | Example                                        |
| ------- | ---------------------------- | ---------------------------------------------- |
| SET     | Set key to hold string value | `r.set('name', 'John')`                        |
| GET     | Get value of key             | `r.get('name')`                                |
| MSET    | Set multiple keys to values  | `r.mset({'key1': 'value1', 'key2': 'value2'})` |
| MGET    | Get values of multiple keys  | `r.mget(['key1', 'key2'])`                     |
| INCR    | Increment value by 1         | `r.incr('counter')`                            |
| DECR    | Decrement value by 1         | `r.decr('counter')`                            |
| EXPIRE  | Set key timeout in seconds   | `r.expire('name', 60)`                         |

### Lists

| Command | Description                     | Example                      |
| ------- | ------------------------------- | ---------------------------- |
| LPUSH   | Insert at the start of list     | `r.lpush('mylist', 'value')` |
| RPUSH   | Insert at the end of list       | `r.rpush('mylist', 'value')` |
| LPOP    | Remove and return first element | `r.lpop('mylist')`           |
| RPOP    | Remove and return last element  | `r.rpop('mylist')`           |
| LRANGE  | Get range of elements           | `r.lrange('mylist', 0, -1)`  |
| LLEN    | Get length of list              | `r.llen('mylist')`           |
| LINDEX  | Get element by index            | `r.lindex('mylist', 1)`      |

### Sets

| Command   | Description               | Example                               |
| --------- | ------------------------- | ------------------------------------- |
| SADD      | Add member(s) to set      | `r.sadd('myset', 'value1', 'value2')` |
| SREM      | Remove member(s) from set | `r.srem('myset', 'value1')`           |
| SMEMBERS  | Get all members of set    | `r.smembers('myset')`                 |
| SISMEMBER | Check if value is in set  | `r.sismember('myset', 'value1')`      |
| SCARD     | Get set size              | `r.scard('myset')`                    |
| SINTER    | Intersection of sets      | `r.sinter('set1', 'set2')`            |
| SUNION    | Union of sets             | `r.sunion('set1', 'set2')`            |

### Sorted Sets

| Command | Description                  | Example                                   |
| ------- | ---------------------------- | ----------------------------------------- |
| ZADD    | Add member with score        | `r.zadd('leaderboard', {'player1': 100})` |
| ZREM    | Remove member                | `r.zrem('leaderboard', 'player1')`        |
| ZRANGE  | Get range by index           | `r.zrange('leaderboard', 0, -1)`          |
| ZRANK   | Get rank of member           | `r.zrank('leaderboard', 'player1')`       |
| ZSCORE  | Get score of member          | `r.zscore('leaderboard', 'player1')`      |
| ZCOUNT  | Count members in score range | `r.zcount('leaderboard', 0, 100)`         |
| ZINCRBY | Increment score of member    | `r.zincrby('leaderboard', 10, 'player1')` |

### Hashes

| Command | Description               | Example                                          |
| ------- | ------------------------- | ------------------------------------------------ |
| HSET    | Set field in hash         | `r.hset('user:1', 'name', 'John')`               |
| HGET    | Get field from hash       | `r.hget('user:1', 'name')`                       |
| HMSET   | Set multiple fields       | `r.hmset('user:1', {'name': 'John', 'age': 30})` |
| HMGET   | Get multiple fields       | `r.hmget('user:1', ['name', 'age'])`             |
| HGETALL | Get all fields and values | `r.hgetall('user:1')`                            |
| HDEL    | Delete field(s)           | `r.hdel('user:1', 'age')`                        |
| HEXISTS | Check if field exists     | `r.hexists('user:1', 'name')`                    |

### General Keys

| Command | Description                | Example                          |
| ------- | -------------------------- | -------------------------------- |
| DEL     | Delete key(s)              | `r.delete('key1', 'key2')`       |
| EXISTS  | Check if key exists        | `r.exists('key1')`               |
| KEYS    | Find keys matching pattern | `r.keys('user:*')`               |
| TTL     | Get remaining time to live | `r.ttl('key1')`                  |
| TYPE    | Get type of value stored   | `r.type('key1')`                 |
| RENAME  | Rename key                 | `r.rename('old_key', 'new_key')` |

To use these commands, first establish a connection to Redis:

```python
import redis

# Connect to Redis
redis_client = redis.Redis(
    host='localhost',
    port=6379,
    db=0,
    decode_responses=True  # This automatically decodes responses to strings
)
```
