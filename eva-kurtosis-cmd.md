
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
  erigon init --datadir=/data/erigon/execution-data /network-configs/genesis.json

  erigon --networkid=3151908
  --log.console.verbosity=3
  --datadir=/data/erigon/execution-data
  --port=30303
  --http.api=eth,erigon,engine,web3,net,debug,trace,txpool,admin
  --http.vhosts=*
  --ws
  --allow-insecure-unlock
  --nat=extip:172.16.8.11
  --http --http.addr=0.0.0.0
  --http.corsdomain=*
  --http.port=8545
  --authrpc.jwtsecret=/jwt/jwtsecret
  --authrpc.addr=0.0.0.0
  --authrpc.port=8551
  --authrpc.vhosts=*
  --externalcl
  --metrics
  --metrics.addr=0.0.0.0
  --metrics.port=9001
  --torrent.port=42069
ENV:
  PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

## beacon 共识层

> kurtosis service inspect evatest2 cl-1-prysm-erigon

```
Name: cl-1-prysm-erigon
UUID: 2b4ef41cfc71
Status: RUNNING
Image: gcr.io/offchainlabs/prysm/beacon-chain:stable
Ports:
  http: 3500/tcp -> http://127.0.0.1:32798
  metrics: 8080/tcp -> http://127.0.0.1:32801
  profiling: 6060/tcp -> 127.0.0.1:32800
  quic-discovery: 13000/udp -> 127.0.0.1:32776
  rpc: 4000/tcp -> 127.0.0.1:32799
  tcp-discovery: 13000/tcp -> 127.0.0.1:32802
  udp-discovery: 12000/udp -> 127.0.0.1:32775
ENTRYPOINT:
  sh
  -c
CMD:
  exec /beacon-chain --accept-terms-of-use=true
  --datadir=/data/prysm/beacon-data/
  --execution-endpoint=http://172.16.8.11:8551
  --rpc-host=0.0.0.0
  --rpc-port=4000
  --http-host=0.0.0.0
  --http-cors-domain=*
  --http-port=3500
  --p2p-host-ip=172.16.8.12
  --p2p-tcp-port=13000
  --p2p-udp-port=12000
  --p2p-quic-port=13000
  --min-sync-peers=0
  --verbosity=info
  --slots-per-archive-point=32
  --suggested-fee-recipient=0x8943545177806ED17B9F23F0a21ee5948eCaa776
  --jwt-secret=/jwt/jwtsecret
  --disable-monitoring=false
  --monitoring-host=0.0.0.0
  --monitoring-port=8080
  --pprof --pprofaddr=0.0.0.0
  --pprofport=6060
  --p2p-static-id=true
  --chain-config-file=/network-configs/config.yaml
  --genesis-state=/network-configs/genesis.ssz
  --contract-deployment-block=0
ENV:
  PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  SSL_CERT_FILE: /etc/ssl/certs/ca-certificates.crt
```

