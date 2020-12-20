# Kubernetes

## List of Commands

```bash

# Delete PV/PVC/SC
kubectl get sc | tail -n +2 | grep -iF mall-realtime02 | awk '{print $1}' | xargs -I{} kubectl delete sc {}
kubectl -n mall-realtime02 get pvc | tail -n +2 | awk '{print $1}' | xargs -I{} kubectl -n mall-realtime02 delete pvc {}
kubectl get pv | tail -n +2 | grep -iF mall-realtime02 | awk '{print $1}' | xargs -I{} kubectl delete pv {}

```

## Kubernete Commands

```bash
dmesg -T | egrep -i 'killed process' -A100 -B100 # OOM killed messages

kubectl -n online-pipeline get pods --field-selector=status.phase!=Running # Find not running pods

kubectl -n online-pipeline exec -it indexer-0 -- bash -c 'ps -aux'

mysql -h mysql -uroot -p123456 -e "CREATE DATABASE IF NOT EXISTS business_engine"
mysql -h mysql -uroot -p123456 business_engine_old < "../business-engine/schemas/business_engine.sql"

kubectl create secret generic regcred --from-file=.dockerconfigjson=/root/.docker/config.json --type=kubernetes.io/dockerconfigjson -n mall-v3-qa

kubectl get nodes --show-labels
kubectl label nodes gpu620.aibee.cn seaweedfs-filer=true

scp "root@10.255.3.241:/mnt/data/prod/customer/K11/wuhan/gg/tracking/svonline/20191229/pb/*(ch05005|ch05006|ch05010|ch05011)*" ./

```

### SingleView

```bash
kubectl get pods -o wide | grep bodysdk64 | grep -v Running | awk '{print $1}' | xargs -I{} kubectl delete pod {} --force --grace-period=0 # Restart not running singleview pods
```
