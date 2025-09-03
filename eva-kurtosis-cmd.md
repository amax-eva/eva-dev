
## erigon 执行层

> kurtosis service inspect evatest2 el-1-erigon-prysm

```
Name: el-1-erigon-prysm
UUID: 3c49200371c4
Status: RUNNING
Image: erigontech/erigon:latest
Ports:
  engine-rpc: 8551/tcp -> 127.0.0.1:32795
  metrics: 9001/tcp -> http://127.0.0.1:32796
  tcp-discovery: 30303/tcp -> 127.0.0.1:32797
  torrent: 42069/udp -> 127.0.0.1:32774
  udp-discovery: 30303/udp -> 127.0.0.1:32773
  ws-rpc: 8545/tcp -> 127.0.0.1:32794
ENTRYPOINT:
  sh
  -c
CMD:
  erigon init --datadir=/data/erigon/execution-data /network-configs/genesis.json && erigon --networkid=3151908 --log.console.verbosity=3 --datadir=/data/erigon/execution-data --port=30303 --http.api=eth,erigon,engine,web3,net,debug,trace,txpool,admin --http.vhosts=* --ws --allow-insecure-unlock --nat=extip:172.16.8.11 --http --http.addr=0.0.0.0 --http.corsdomain=* --http.port=8545 --authrpc.jwtsecret=/jwt/jwtsecret --authrpc.addr=0.0.0.0 --authrpc.port=8551 --authrpc.vhosts=* --externalcl --metrics --metrics.addr=0.0.0.0 --metrics.port=9001 --torrent.port=42069
ENV:
  PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```
