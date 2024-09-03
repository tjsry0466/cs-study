# Redis 명령어 정리

Redis는 다양한 자료구조를 지원하며, 각 자료구조에 따라 여러 명령어를 제공합니다. 아래는 Redis의 주요 명령어를 자료구조별로 정리한 내용입니다.

## 1. Key 관련 명령어

Redis의 모든 데이터는 "키-값" 쌍으로 저장되며, 키를 조작하기 위한 다양한 명령어를 제공합니다.

- **DEL key [key ...]**: 하나 또는 여러 개의 키를 삭제합니다.
- **DUMP key**: 주어진 키의 값을 직렬화된 형식으로 반환합니다.
- **EXISTS key [key ...]**: 하나 또는 여러 키가 존재하는지 확인합니다.
- **EXPIRE key seconds**: 특정 키의 TTL(Time To Live)을 초 단위로 설정합니다.
- **EXPIREAT key timestamp**: UNIX 타임스탬프를 기준으로 TTL을 설정합니다.
- **KEYS pattern**: 특정 패턴에 일치하는 모든 키를 찾습니다.
- **MOVE key db**: 키를 현재 데이터베이스에서 지정된 데이터베이스로 이동합니다.
- **PERSIST key**: 특정 키의 TTL을 제거하여, 해당 키가 영구적으로 유지되도록 합니다.
- **PTTL key**: 특정 키의 TTL을 밀리초 단위로 반환합니다.
- **RENAME key newkey**: 키의 이름을 변경합니다.
- **SORT key [options]**: 특정 리스트, 셋, 또는 정렬된 셋을 정렬합니다.
- **TTL key**: 특정 키의 TTL을 초 단위로 반환합니다.
- **TYPE key**: 특정 키의 데이터 타입을 반환합니다.

## 2. String 관련 명령어

String은 Redis에서 가장 기본적인 데이터 타입으로, 다양한 조작이 가능합니다.

- **APPEND key value**: 키에 연결된 값에 추가 데이터를 덧붙입니다.
- **BITCOUNT key [start end]**: 문자열의 비트 값에서 1의 개수를 계산합니다.
- **BITOP operation destkey key [key ...]**: 여러 문자열의 비트 연산을 수행합니다.
- **DECR key**: 키의 값을 1 감소시킵니다.
- **DECRBY key decrement**: 키의 값을 지정된 감소량만큼 줄입니다.
- **GET key**: 키에 저장된 값을 반환합니다.
- **GETBIT key offset**: 문자열 값에서 특정 비트의 값을 반환합니다.
- **GETRANGE key start end**: 문자열의 지정된 범위 내의 부분 문자열을 반환합니다.
- **GETSET key value**: 이전 값을 반환하고, 새로운 값을 설정합니다.
- **INCR key**: 키의 값을 1 증가시킵니다.
- **INCRBY key increment**: 키의 값을 지정된 증가량만큼 늘립니다.
- **INCRBYFLOAT key increment**: 키의 값을 소수점 증가량만큼 늘립니다.
- **MGET key [key ...]**: 여러 키의 값을 한 번에 반환합니다.
- **MSET key value [key value ...]**: 여러 키를 한 번에 설정합니다.
- **MSETNX key value [key value ...]**: 모든 키가 존재하지 않을 때만 여러 키를 한 번에 설정합니다.
- **PSETEX key milliseconds value**: 키의 값을 설정하고, TTL을 밀리초 단위로 설정합니다.
- **SET key value [options]**: 키의 값을 설정하고 옵션에 따라 TTL을 설정합니다.
- **SETBIT key offset value**: 문자열 값에서 특정 비트를 설정합니다.
- **SETEX key seconds value**: 값을 설정하고, TTL을 초 단위로 설정합니다.
- **SETNX key value**: 키가 존재하지 않을 때만 값을 설정합니다.
- **SETRANGE key offset value**: 문자열 값에서 지정된 오프셋에 값을 설정합니다.
- **STRLEN key**: 문자열 값의 길이를 반환합니다.

## 3. List 관련 명령어

List는 순서가 있는 데이터의 모음을 관리하며, 큐 또는 스택과 같은 기능을 제공합니다.

- **BLPOP key [key ...] timeout**: 하나 이상의 리스트에서 값을 블로킹하여 팝합니다.
- **BRPOP key [key ...] timeout**: 하나 이상의 리스트에서 값을 블로킹하여 오른쪽에서 팝합니다.
- **BRPOPLPUSH source destination timeout**: 리스트의 오른쪽에서 팝하여 다른 리스트의 왼쪽에 삽입합니다.
- **LINDEX key index**: 리스트에서 지정된 인덱스의 값을 반환합니다.
- **LINSERT key BEFORE | AFTER pivot value**: 리스트의 특정 위치에 값을 삽입합니다.
- **LLEN key**: 리스트의 길이를 반환합니다.
- **LPOP key**: 리스트의 왼쪽에서 값을 팝합니다.
- **LPUSH key value [value ...]**: 리스트의 왼쪽에 값을 추가합니다.
- **LPUSHX key value**: 키가 존재할 때만 리스트의 왼쪽에 값을 추가합니다.
- **LRANGE key start stop**: 리스트의 지정된 범위 내의 값을 반환합니다.
- **LREM key count value**: 리스트에서 지정된 값과 일치하는 요소를 제거합니다.
- **LSET key index value**: 리스트에서 지정된 위치의 값을 설정합니다.
- **LTRIM key start stop**: 리스트를 지정된 범위로 잘라냅니다.
- **RPOP key**: 리스트의 오른쪽에서 값을 팝합니다.
- **RPOPLPUSH source destination**: 리스트의 오른쪽에서 팝하여 다른 리스트의 왼쪽에 삽입합니다.
- **RPUSH key value [value ...]**: 리스트의 오른쪽에 값을 추가합니다.
- **RPUSHX key value**: 키가 존재할 때만 리스트의 오른쪽에 값을 추가합니다.

## 4. Hash 관련 명령어

Hash는 필드와 값 쌍을 관리하는 자료구조로, 하나의 키 아래 여러 필드를 저장할 수 있습니다.

- **HDEL key field [field ...]**: 하나 이상의 필드를 제거합니다.
- **HEXISTS key field**: 필드가 존재하는지 확인합니다.
- **HGET key field**: 필드의 값을 반환합니다.
- **HGETALL key**: 키에 저장된 모든 필드와 값을 반환합니다.
- **HINCRBY key field increment**: 필드의 값을 지정된 증가량만큼 늘립니다.
- **HINCRBYFLOAT key field increment**: 필드의 값을 소수점 증가량만큼 늘립니다.
- **HKEYS key**: 키에 저장된 모든 필드 이름을 반환합니다.
- **HLEN key**: 키에 저장된 필드의 수를 반환합니다.
- **HMGET key field [field ...]**: 하나 이상의 필드를 가져옵니다.
- **HMSET key field value [field value ...]**: 여러 필드를 한 번에 설정합니다.
- **HSET key field value**: 필드의 값을 설정합니다.
- **HSETNX key field value**: 필드가 존재하지 않을 때만 값을 설정합니다.
- **HVALS key**: 키에 저장된 모든 값을 반환합니다.

## 5. Set 관련 명령어

Set은 중복되지 않은 문자열의 모음으로, 집합 연산을 지원합니다.

- **SADD key member [member ...]**: 집합에 하나 이상의 요소를 추가합니다.
- **SCARD key**: 집합의 크기를 반환합니다.
- **SDIFF key [key ...]**: 집합 간의 차집합을 반환합니다.
- **SDIFFSTORE destination key [key ...]**: 차집합 결과를 다른 집합에 저장합니다.
- **SINTER key [key ...]**: 집합 간의 교집합을 반환합니다.
- **SINTERSTORE destination key [key ...]**: 교집합 결과를 다른 집합에 저장합니다.
- **SISMEMBER key member**: 집합에 특정 요소가 포함되어 있는지 확인합니다.
- **SMEMBERS key**: 집합의 모든 요소를 반환합니다.
- **SMOVE source destination member**: 한 집합에서 다른 집합으로 요소를 이동합니다.
- **SPOP key [count]**: 집합에서 하나 이상의 요소를 제거하고 반환합니다.
- **SRANDMEMBER key [count]**: 집합에서 하나 이상의 무작위 요소를 반환합니다.
- **SREM key member [member ...]**: 집합에서 하나 이상의 요소를 제거합니다.
- **SUNION key [key ...]**: 집합 간의 합집합을 반환합니다.
- **SUNIONSTORE destination key [key ...]**: 합집합 결과를 다른 집합에 저장합니다.

## 6. Sorted Set 관련 명령어

Sorted Set은 Set과 유사하지만, 각 요소에 점수를 부여하여 정렬된 상태로 저장합니다.

- **ZADD key [NX | XX] [CH] [INCR] score member [score member ...]**: 정렬된 집합에 하나 이상의 요소를 추가합니다.
- **ZCARD key**: 정렬된 집합의 크기를 반환합니다.
- **ZCOUNT key min max**: 주어진 점수 범위 내의 요소 수를 반환합니다.
- **ZINCRBY key increment member**: 정렬된 집합에서 지정된 요소의 점수를 증가시킵니다.
- **ZINTERSTORE destination numkeys key [key ...] [options]**: 여러 정렬된 집합의 교집합을 계산하고 저장합니다.
- **ZLEXCOUNT key min max**: 사전 순서 범위 내의 요소 수를 반환합니다.
- **ZRANGE key start stop [WITHSCORES]**: 정렬된 집합에서 지정된 범위의 요소를 반환합니다.
- **ZRANGEBYLEX key min max [LIMIT offset count]**: 사전 순서 범위 내의 요소를 반환합니다.
- **ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT offset count]**: 점수 범위 내의 요소를 반환합니다.
- **ZRANK key member**: 정렬된 집합에서 지정된 요소의 순위를 반환합니다.
- **ZREM key member [member ...]**: 정렬된 집합에서 하나 이상의 요소를 제거합니다.
- **ZREMRANGEBYLEX key min max**: 사전 순서 범위 내의 요소를 제거합니다.
- **ZREMRANGEBYRANK key start stop**: 순위 범위 내의 요소를 제거합니다.
- **ZREMRANGEBYSCORE key min max**: 점수 범위 내의 요소를 제거합니다.
- **ZREVRANGE key start stop [WITHSCORES]**: 정렬된 집합에서 지정된 범위의 요소를 역순으로 반환합니다.
- **ZREVRANGEBYSCORE key max min [WITHSCORES]**: 점수 범위 내의 요소를 역순으로 반환합니다.
- **ZREVRANK key member**: 정렬된 집합에서 지정된 요소의 역순 순위를 반환합니다.
- **ZSCORE key member**: 정렬된 집합에서 지정된 요소의 점수를 반환합니다.
- **ZUNIONSTORE destination numkeys key [key ...] [options]**: 여러 정렬된 집합의 합집합을 계산하고 저장합니다.

## 7. Pub/Sub 관련 명령어

Redis는 Pub/Sub 메시징 패턴을 지원합니다.

- **PSUBSCRIBE pattern [pattern ...]**: 주어진 패턴과 일치하는 모든 채널을 구독합니다.
- **PUBSUB subcommand [argument [argument ...]]**: Pub/Sub 시스템을 검사합니다.
- **PUBLISH channel message**: 특정 채널에 메시지를 게시합니다.
- **PUNSUBSCRIBE [pattern [pattern ...]]**: 주어진 패턴과 일치하는 모든 채널의 구독을 취소합니다.
- **SUBSCRIBE channel [channel ...]**: 하나 이상의 채널을 구독합니다.
- **UNSUBSCRIBE [channel [channel ...]]**: 하나 이상의 채널의 구독을 취소합니다.

## 8. Transaction 관련 명령어

Redis는 간단한 트랜잭션 기능을 제공합니다.

- **DISCARD**: 트랜잭션 큐를 비우고 트랜잭션을 취소합니다.
- **EXEC**: 트랜잭션 큐에 있는 모든 명령어를 실행합니다.
- **MULTI**: 새로운 트랜잭션을 시작합니다.
- **UNWATCH**: 모든 키에 대한 WATCH를 취소합니다.
- **WATCH key [key ...]**: 하나 이상의 키를 감시하여 다른 클라이언트가 수정하면 트랜잭션이 실패하게 만듭니다.

## 9. 스크립트 관련 명령어

Redis는 Lua 스크립트를 실행할 수 있습니다.

- **EVAL script numkeys key [key ...] arg [arg ...]**: Lua 스크립트를 실행합니다.
- **EVALSHA sha1 numkeys key [key ...] arg [arg ...]**: 저장된 Lua 스크립트를 실행합니다.
- **SCRIPT EXISTS sha1 [sha1 ...]**: 하나 이상의 스크립트가 캐시에 있는지 확인합니다.
- **SCRIPT FLUSH**: 모든 Lua 스크립트를 캐시에서 제거합니다.
- **SCRIPT KILL**: 실행 중인 Lua 스크립트를 중단합니다.
- **SCRIPT LOAD script**: Lua 스크립트를 서버에 로드하고, SHA1 해시를 반환합니다.

## 10. Connection 관련 명령어

클라이언트와 Redis 서버 간의 연결을 관리합니다.

- **AUTH password**: 서버 인증을 수행합니다.
- **ECHO message**: 메시지를 반환합니다.
- **PING [message]**: 서버의 응답을 확인합니다.
- **QUIT**: 연결을 종료합니다.
- **SELECT index**: 데이터베이스를 선택합니다.

## 11. Server 관련 명령어

Redis 서버를 관리하는 다양한 명령어입니다.

- **BGREWRITEAOF**: AOF 파일을 백그라운드에서 다시 작성합니다.
- **BGSAVE**: 데이터베이스를 백그라운드에서 디스크에 저장합니다.
- **CLIENT KILL [ip:port]**: 특정 클라이언트를 연결 종료합니다.
- **CLIENT LIST**: 현재 연결된 모든 클라이언트를 나열합니다.
- **CONFIG GET parameter**: 구성 매개변수 값을 가져옵니다.
- **CONFIG SET parameter value**: 구성 매개변수 값을 설정합니다.
- **DBSIZE**: 현재 데이터베이스의 키 개수를 반환합니다.
- **FLUSHALL**: 모든 데이터베이스의 모든 키를 삭제합니다.
- **FLUSHDB**: 현재 데이터베이스의 모든 키를 삭제합니다.
- **INFO [section]**: Redis 서버의 정보를 제공합니다.
- **LASTSAVE**: 데이터베이스가 마지막으로 저장된 시간을 반환합니다.
- **MONITOR**: 모든 Redis 명령어를 실시간으로 출력합니다.
- **SAVE**: 데이터베이스를 디스크에 저장합니다.
- **SHUTDOWN [NOSAVE | SAVE]**: 서버를 종료합니다.
- **SLAVEOF host port**: 현재 서버를 다른 서버의 슬레이브로 설정합니다.
- **SLOWLOG subcommand [argument]**: 슬로우 로그를 관리합니다.
- **TIME**: 서버의 현재 시간을 반환합니다.
