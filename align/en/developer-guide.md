## Database > EasyCache > Developer Guide

## Client Access

EasyCache can be accessed from applications in instances using the same VPC subnet.
Since EasyCache is based on Redis, it supports various development programming languages.

### JAVA

Jedis is a Redis client for JAVA.

The following is the JAR files required for installation.
* jedis-2.9.0.jar
* commons-pool2-2.4.2.jar

**Code Example for Access**

```
 public static void main( String[] args ) {
    Jedis jedis = new Jedis("localhost", 6379);
    jedis.set("foo", "bar");
}
```

### PHP

Predis is a Redis client for PHP.

**Code Example for Access**

```
$client = new Predis\Client('tcp://127.0.0.1:6379');
$client->set('hogehoge','fugafuga');
```
Or
```
$client = new Predis\Client([
    'scheme' => 'tcp',
    'host'   => '192.168.10.33',
    'port'   => 6379,
]);
$client->set('hogehoge','fugafuga');
```

### Python

redis-py is a Redis client for Python.
redis-py can be installed as follows.

```
$ pip install redis
```

**Code Example for Access**

```
import redis

r = r = redis.StrictRedis(host='localhost', port=6379, db=0)
r.set('hoge', 'moge')
```
Or
```
import redis

pool = redis.ConnectionPool(host='localhost', port=6379, db=0)
r = redis.StrictRedis(connection_pool=pool)
r.set('hoge', 'moge')
```

## Access EasyCache for Redis Server from an Instance

A Redis server can be accessed only from within the same VPC subnet.
Create an instance in the same VPC subnet.

To use a Redis client, you must install Redis for each OS.

```
For CentOS:
yum -y install epel-release
yum -y install redis
```
When the installation is finished, check that it is installed properly.
```
redis-cli -v
```

Select the replication group to access and click the **Access Information** tab in the details.
 ![rep_de_005.PNG](https://static.toastoven.net/prod_easycache/19.12.06/rep_connection_info_001.PNG)

* Select the one between private and public commands and click the **Copy** button to copy the command. Paste the copied command on the instance's command window.
* Connect to the Redis server.
* When you click **Show** button on the password, the password is displayed and the **Copy** button is enabled.
* Click the **Copy** button to copy the password.
* Authenticate using the AUTH command.
    * AUTH {copied password}

## Redis Command Restriction

Use of the following commands is restricted as it may have a fatal impact on the service.

* BGREWRITEAOF
* BGSAVE
* CONFIG
* DEBUG
* MIGRATE
* SAVE
* SHUTDOWN
* SLAVEOF
* REPLICAOF
* SYNC

When the number of key or item is large (more than hundreds of thousands), the performance may decrease or the system may hang if the following commands are used.

* KEYS
* FLUSHALL, FLUSHDB
* Delete Collections
* Get All Collections

## Memory Management

If the system memory usage exceeds 80%, you must do the following to prevent out-of-memory situation on your instance.

* You should monitor the memory usage. Learn about the EasyCache alarm function.
* Enable activedefrag on the instance.
* You should lower the maxmemory limit of the instance.
* Choose an appropriate maxmemory-policy
    * If you are storing volatile data, choose one of the volatile-* eviction policies. If you are storing non-volatile data, choose one of the allkeys-* policies.
* Follow the instance scaling instructions to increase instance capacity.
