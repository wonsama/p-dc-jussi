# p-dc-jussi

> steem json-rpc20 api

스팀 rpc 통신을 위한 jussi 의 docker-compose 설정
개별 빌드를 하려고 한다면 [아래 링크]((https://github.com/steemit/jussi)를 참조 바랍니다.

## `docker-compoes.yml`

> [github : jussi](https://github.com/steemit/jussi) 과의 차이점

- 로그 수집을 위한 `StatsD` 설치 제외
- `redis` 는 relica(복제본) 설치는 하지 않음 (외부 조회 목적용으로 사용됨-해당 복제본만 port 노출)
- `JUSSI_UPSTREAM_CONFIG_FILE` 경로를 변경(기존 : /app/DEV_config.json)

## install

> 사전에 `docker` 와 `docker-compose` 가 설치 되어 있어야 된다.
> 최초 실행 시 `docker-compose up` 로 실행하여 현재 정상적으로 동작하는지 로그를 확인한 이후 `docker-compose up -d` 위와 같이 데몬 형태로 구동하는 것을 추천

```sh
git clone https://github.com/wonsama/p-dc-jussi.git
cd p-dc-jussi
mv config.json.sample config.json
docker-compose up -d
```

## config

> 필요에 따라 urls 에 접속할 주소를 추가 하여 사용하면 됨.
> 기본적으로는 변경 없어도 되나 `urls` 값을 수정하여 `jussi` 에서 서비스할 rpc 주소를 지정할 수 있다.

- 내가 `steemd` 라는 이름으로 서비스를 하겠다는 이야기 임
- `urls` 는 순차적으로 해당 주소로 connection 을 하겠다는 이야기 임.
- 즉 아래 예제는 내가 운영하는 서비스(`steemd`) 를 호출 한 이후, 실패하면 `https://api.steemit.com` 를 호출 하겠다는 뜻

```json
"name": "steemd",
"urls": [
    [
        "steemd",
        "https://api.steemit.com"
    ]
],
...

```

## StatsD

> https://planbs.tistory.com/entry/StatsD

StatsD는 로그 메트릭을 수집하는 영역에서 ProxySQL과 비슷한 용도로 쓰인다. UDP나 TCP를 통해 counter나 time과 같은 통계 데이터를 받아, Graphite같은 backend에 전송하는 Proxy다. 따라서 ProxySQL처럼 connection 중계가 아니라 통계적인 데이터 집계 처리 용도의 proxy로서 사용된다.

## reference

- [github : jussi](https://github.com/steemit/jussi)
- [Steem Node 정리 (Full node 2편) -설치](https://www.steemcoinpan.com/hive-101145/@ayogom/steem-node-full-node-2)
