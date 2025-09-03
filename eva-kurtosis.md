
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
