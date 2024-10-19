# Learning :
[Redis for Beginners - Net Ninja](https://www.youtube.com/playlist?list=PL4cUxeGkcC9h3V2eqhi8rRdIDJshP-b4P)
[Redis Crash Course - Web Dev Simplified](https://www.youtube.com/watch?v=jgpVdJB2sKQ&t=1018s)

Redis is like Map in JS, *`KEY = VALUE`* and *`VALUE`* is usually/default stored as string
# Terminal Commands :
- Open WSL :                               `wsl`
- Start Redis server :                    `redis-server`
- Open Redis server :                   `redis-cli`
- Quit CLI :                                   `quit`
- SET pair :                                   `SET KEY VALUE`
- GET VALUE :                              `GET KEY`
- DELETE VALUE :                         `DEL KEY`
- CHECK IF KEY EXIST :                 `EXISTS KEY`
- LIST ALL KEYS :                           `KEYS *`
- DELETE WHOLE REDIS DATA :   `flushall`

> Expiration (time limit) of a key :
- `ttl KEY` === `-1` then key exist but don't have expiration time
- `ttl KEY` === `-2` then key don't exist
- `ttl KEY` === positive integer is seconds left.
- to set expiration time of stored KEY ==> `expire KEY 10` here 10 is 10sec
- to set expiration time of ***NEW*** KEY   ==> `setex KEY 10 VALUE`

> List (***doubly queue***) :
- `lpush KEY VALUE` ==> make an array of name `KEY`(if not exist) and push `VALUE` at the *START* of array.
- `rpush KEY VALUE` ==> make an array of name `KEY`(if not exist) and push `VALUE` at the *END* of array.
- `lrange KEY 0 -1` ==> list all values in array.
- `LPOP KEY` ==> pops out first element.
- `RPOP KEY` ==> pops out last element.

> Sets (like maths sets allow only unique values) :
- `SADD KEY VALUE` ==> creates set `KEY` if not exist and then add `VALUE`
- `SMEMBERS KEY` ==> list all values in set `KEY`.
- `SREM KEY VALUE` ==> removes `VALUE` from `KEY` set.

> Hashes (key value pairs inside a key value pair (but hashes can't be nested))
- `HSET KEY KEY VALUE` === `KEY = { KEY: VALUE }`
- Example : `HSET person name kyle` === `person = { name: kyle }`
- `HGET person name` outputs `kyle`.
- `HSET person age 26` 
- `HGETALL person` outputs :
```shell
"name"
"kyle"
"age"
"26"
```
- `HDEL person age`  ==> deletes age from person.
- `HEXIST person age` ==> (checks if age exist) outputs 0 as age is deleted.

