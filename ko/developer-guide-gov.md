## Database > EasyCache > 개발자 가이드

## 클라이언트 접속

같은 VPC 서브넷을 이용하는 인스턴스의 애플리케이션에서 접속할 수 있습니다.
Redis를 기반으로 만든 EasyCache는 다양한 개발 언어를 지원합니다.

### JAVA

Jedis는 JAVA용 Redis 클라이언트입니다.

다음은 설치에 필요한 JAR 파일입니다.
* jedis-2.9.0.jar
* commons-pool2-2.4.2.jar

**접속 코드**

```
 public static void main( String[] args ) {
    Jedis jedis = new Jedis("localhost", 6379);
    jedis.set("foo", "bar");
}
```

### PHP

Predis는 PHP용 Redis 클라이언트입니다.

**접속 코드**

```
$client = new Predis\Client('tcp://127.0.0.1:6379');
$client->set('hogehoge','fugafuga');
```
또는
```
$client = new Predis\Client([
    'scheme' => 'tcp',
    'host'   => '192.168.10.33',
    'port'   => 6379,
]);
$client->set('hogehoge','fugafuga');
```

### Python

redis-py는 Python의 Redis 클라이언트입니다.
redis-py는 아래와 같이 설치합니다.

```
$ pip install redis
```

**접속 코드**

```
import redis

r = r = redis.StrictRedis(host='localhost', port=6379, db=0)
r.set('hoge', 'moge')
```
또는
```
import redis

pool = redis.ConnectionPool(host='localhost', port=6379, db=0)
r = redis.StrictRedis(connection_pool=pool)
r.set('hoge', 'moge')
```

## 인스턴스에서 EasyCache for Redis 서버에 접속

같은 VPC 서브넷 내에서만 Redis 서버에 접속할 수 있습니다. 
같은 VPC 서브넷에 있는 인스턴스를 생성합니다.

Redis 클라이언트를 이용하려면 각 OS별로 Redis를 설치해야 합니다.

```
CentOS 경우
yum -y install epel-release   
yum -y install redis
```
설치가 완료되면 제대로 설치되었는지 확인합니다.
```
redis-cli -v
```

접속할 복제 그룹를 선택하고 상세 정보에서 **접속 정보** 탭을 누룹니다. 
 ![rep_de_005.PNG](https://static.toastoven.net/prod_easycache/19.12.06/rep_connection_info_001.PNG)

* 사설/공인 명령어 중 선택하고 **복사** 버튼을 클릭해 명령어를 복사합니다. 복사한 명령어를 인스턴스의 명령어(커맨드) 창에 붙여 넣습니다.
* Redis 서버에 접속합니다. 
* 비밀번호에서 **보기** 버튼을 클릭하면 비밀번호가 표시되고 **복사** 버튼이 활성화됩니다.
* **복사** 버튼을 클릭하면 비밀번호를 복사합니다.
* AUTH 명령어를 이용해 인증합니다.
    * AUTH {복사한 비밀번호}
    
## Redis 명령어 제한

아래와 같은 명령어를 사용하면 서비스에 치명적인 영향을 줄 수 있어 이용에 제한됩니다.

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

key 또는 아이템이 대용량(수십만 개 이상)일 때 아래와 같은 명령어를 사용하면 성능이 저하되거나 시스템이 멈출 수 있습니다.

* KEYS
* FLUSHALL, FLUSHDB
* Delete Collections
* Get All Collections

## 메모리 관리

시스템 메모리 사용률이 80%를 초과하면 인스턴스의 메모리가 부족하지 않도록 다음과 같이 조치해야 합니다.

* 메모리 사용량을 모니터링해야 합니다. EasyCache 알람 기능을 알아보세요.
* 인스턴스에 activedefrag 사용을 설정합니다.
* 인스턴스의 maxmemory 한도를 낮추어야 합니다.
* 적절한 maxmemory-policy 선택
   * 휘발성 데이터를 저장하는 경우 volatile-* 제거 정책 중 하나를 선택합니다. 휘발성이 아닌 데이터를 저장하는 경우 allkeys-* 정책 중 하나를 선택합니다.
* 인스턴스 확장 안내에 따라 인스턴스 용량을 늘립니다.
