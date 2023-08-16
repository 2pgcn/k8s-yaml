helm repo add grafana https://grafana.github.io/helm-charts

### Install loki locally

```sh
helm upgrade --install loki grafana/loki-stack --set grafana.enabled=true,prometheus.enabled=true,prometheus.alertmanager.persistentVolume.enabled=false,prometheus.server.persistentVolume.enabled=false
```

### Change the grafana service to NodePort type and access it

```sh
kubectl edit svc loki-grafana -oyaml -n default
```

```sh
k get statefulset loki -o yaml > loki.yaml
```

### create loki pv/pvc
```shell
k create -f loki-pv.yaml
```
```yaml
#diff
name: storage
persistentVolumeClaim:
  claimName: loki-pv-claim
```
### update diff
```shell
k apply -f loki.yaml
```