
## 运行节点

```
kurtosis run --enclave evatest2 github.com/ethpandaops/ethereum-package --args-file ./network_params.yaml --image-download always
```

* network_params.yaml

```
participants:
  - el_type: erigon
    cl_type: prysm
```

## 查询服务列表

```
kurtosis enclave ls
UUID           Name       Status     Creation Time
8f06ad964ea2   evatest2   RUNNING    Wed, 03 Sep 2025 06:07:31 UTC
```

docker ps
```
CONTAINER ID   IMAGE                                           COMMAND                  CREATED       STATUS       PORTS                                                                                                                                                                                                                                                                                                                                               NAMES
0241a6a23f63   gcr.io/offchainlabs/prysm/validator:stable      "/validator --accept…"   2 hours ago   Up 2 hours   0.0.0.0:32803->8080/tcp, [::]:32803->8080/tcp                                                                                                                                                                                                                                                                                                       vc-1-erigon-prysm--f94f7113c80644d88b266c7d1b59866e
3ace4bab8a04   gcr.io/offchainlabs/prysm/beacon-chain:stable   "sh -c 'exec /beacon…"   2 hours ago   Up 2 hours   0.0.0.0:32798->3500/tcp, [::]:32798->3500/tcp, 0.0.0.0:32799->4000/tcp, [::]:32799->4000/tcp, 0.0.0.0:32800->6060/tcp, [::]:32800->6060/tcp, 0.0.0.0:32801->8080/tcp, [::]:32801->8080/tcp, 0.0.0.0:32775->12000/udp, [::]:32775->12000/udp, 0.0.0.0:32776->13000/udp, 0.0.0.0:32802->13000/tcp, [::]:32776->13000/udp, [::]:32802->13000/tcp       cl-1-prysm-erigon--2b4ef41cfc7140a3b75b592c13c25fd6
7db3626b3af4   erigontech/erigon:latest                        "sh -c 'erigon init …"   2 hours ago   Up 2 hours   6060/tcp, 8080/tcp, 8546/tcp, 9090/tcp, 42069/tcp, 0.0.0.0:32794->8545/tcp, [::]:32794->8545/tcp, 0.0.0.0:32795->8551/tcp, [::]:32795->8551/tcp, 0.0.0.0:32796->9001/tcp, [::]:32796->9001/tcp, 0.0.0.0:32773->30303/udp, 0.0.0.0:32797->30303/tcp, [::]:32773->30303/udp, [::]:32797->30303/tcp, 0.0.0.0:32774->42069/udp, [::]:32774->42069/udp   el-1-erigon-prysm--3c49200371c446f59c6305d9a0cd69c9
7d37eb574aee   protolambda/eth2-val-tools:latest               "sleep 99999"            2 hours ago   Up 2 hours                                                                                                                                                                                                                                                                                                                                                       validator-key-generation-cl-validator-keystore--75af58b874dd4e86981e536ad6c221f6
7207faf2b412   kurtosistech/core:1.11.1                        "/bin/sh -c ./api-co…"   2 hours ago   Up 2 hours   0.0.0.0:32793->7443/tcp, [::]:32793->7443/tcp                                                                                                                                                                                                                                                                                                       kurtosis-api--8f06ad964ea245c89032fcd3466aa3f5
8b6d06d34286   fluent/fluent-bit:4.0.0                         "/fluent-bit/bin/flu…"   2 hours ago   Up 2 hours   2020/tcp                                                                                                                                                                                                                                                                                                                                            kurtosis-logs-collector--8f06ad964ea245c89032fcd3466aa3f5
773cbdc59eec   kurtosistech/engine:1.11.1                      "/bin/sh -c ./kurtos…"   2 hours ago   Up 2 hours   0.0.0.0:8081->8081/tcp, 0.0.0.0:9710-9711->9710-9711/tcp, 0.0.0.0:9779->9779/tcp                                                                                                                                                                                                                                                                    kurtosis-engine--e1b83a149a6646219f9b629f55eec9e8
8c5d9719d575   traefik:2.10.6                                  "/bin/sh -c 'mkdir -…"   2 hours ago   Up 2 hours   80/tcp, 0.0.0.0:9730-9731->9730-9731/tcp                                                                                                                                                                                                                                                                                                            kurtosis-reverse-proxy--e1b83a149a6646219f9b629f55eec9e8
7021f30912b8   timberio/vector:0.45.0-debian                   "/bin/sh -c '/usr/bi…"   2 hours ago   Up 2 hours                                                                                                                                                                                                                                                                                                                                                       kurtosis-logs-aggregator
```

## 查看服务运行命令

```
kurtosis service inspect evatest2 vc-1-erigon-prysm


Name: vc-1-erigon-prysm
UUID: f94f7113c806
Status: RUNNING
Image: gcr.io/offchainlabs/prysm/validator:stable
Ports:
  metrics: 8080/tcp -> http://127.0.0.1:32803
ENTRYPOINT:
  /validator
CMD:
  --accept-terms-of-use=true
  --chain-config-file=/network-configs/config.yaml
  --suggested-fee-recipient=0x8943545177806ED17B9F23F0a21ee5948eCaa776
  --beacon-rest-api-provider=http://172.16.8.12:3500
  --disable-monitoring=false
  --monitoring-host=0.0.0.0
  --monitoring-port=8080
  --beacon-rpc-provider=172.16.8.12:4000
  --wallet-dir=/validator-keys/prysm
  --wallet-password-file=/prysm-password/prysm-password.txt
ENV:
  PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  SSL_CERT_FILE: /etc/ssl/certs/ca-certificates.crt
```

## 进入容器

查看相应文件的内容配置

```
kurtosis service shell evatest2 vc-1-erigon-prysm


Found bash on container; creating bash shell...
root@0241a6a23f63:/#

```
