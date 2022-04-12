# p-dc-jussi

> steem json-rpc20 api

스팀 rpc 통신을 위한 jussi 의 docker-compose 설정
개별 빌드를 하려고 한다면 [아래 링크]((https://github.com/steemit/jussi)를 참조 바랍니다.

## `docker-compoes.yml` 과 `docker-compoes.yml.ori` 차이

- 로그 수집을 위한 `StatsD` 설치 제외
- `redis` 는 relica(복제본) 설치는 하지 않음 (외부 조회 목적용으로 사용됨-해당 복제본만 port 노출)
- `JUSSI_UPSTREAM_CONFIG_FILE` 경로를 변경(기존 : /app/DEV_config.json)

## install

```sh
git clone https://github.com/wonsama/p-dc-jussi.git
```

## StatsD

> https://planbs.tistory.com/entry/StatsD

StatsD는 로그 메트릭을 수집하는 영역에서 ProxySQL과 비슷한 용도로 쓰인다. UDP나 TCP를 통해 counter나 time과 같은 통계 데이터를 받아, Graphite같은 backend에 전송하는 Proxy다. 따라서 ProxySQL처럼 connection 중계가 아니라 통계적인 데이터 집계 처리 용도의 proxy로서 사용된다.

## reference

- [github : jussi](https://github.com/steemit/jussi)
- [Steem Node 정리 (Full node 2편) -설치](https://www.steemcoinpan.com/hive-101145/@ayogom/steem-node-full-node-2)
