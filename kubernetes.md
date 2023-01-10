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
# Delete not running pod on the specific node
kubectl get pods -A -o wide --field-selector=status.phase!=Running | grep "ip-10-0-130-118.cn-northwest-1.compute.internal" | awk '{printf "kubectl -n %s delete pod %s\n",$1,$2}' | xargs -0 bash -c
dmesg -T | egrep -i 'killed process' -A100 -B100 # OOM killed messages

kubectl -n online-pipeline get pods --field-selector=status.phase!=Running # Find not running pods

kubectl -n online-pipeline exec -it indexer-0 -- bash -c 'ps -aux'

mysql -h mysql -uroot -p123456 -e "CREATE DATABASE IF NOT EXISTS business_engine"
mysql -h mysql -uroot -p123456 business_engine_old < "../business-engine/schemas/business_engine.sql"

kubectl create secret generic regcred --from-file=.dockerconfigjson=/root/.docker/config.json --type=kubernetes.io/dockerconfigjson -n mall-v3-qa

kubectl get nodes --show-labels
kubectl label nodes gpu620.aibee.cn seaweedfs-filer=true

scp "root@10.255.3.241:/mnt/data/prod/customer/K11/wuhan/gg/tracking/svonline/20191229/pb/*(ch05005|ch05006|ch05010|ch05011)*" ./

kubectl -n hive delete pod hive-cli --force --grace-period=0 # Terminate running hive-cli pod in hive namespace
```

### Get not running pod names

```bash
kubectl -n airbyte get pods --field-selector status.phase!=Running --no-headers -o custom-columns=":metadata.name"
```

## Issues

### EKS - EFS CSI - dynamic provisioning: `Operation not permitted`

当pod通过[aws-efs-csi-driver](https://github.com/kubernetes-sigs/aws-efs-csi-driver)以及dynamic provisioning挂载磁盘并进行ownership变更时出现`Operation not permitted`的报错.

原因分析：`aws-efs-csi-driver`的dynamic provisioning，是通过`EFS`的`access point`模式挂载卷。从`EFS`的角度来说，客户端不可修改其`uid/gid`. 如需变通，有两种方式：

1. 使用[static provisioning方式部署](https://www.cnsre.cn/posts/220110850573/#%E9%83%A8%E7%BD%B2%E9%9D%99%E6%80%81%E4%BE%9B%E7%BB%99)修改
2. 如果一定需要通过dynamic provisioning进行配置，
    * 2.1 需先创建对应的pvc，等待EFS的access point创建成功
    * 2.2 在EFS的access point页面，找到对应的uid/gid
    * 2.3 配置pod的 `spec.temmplate.spec.securityContext`

    ```bash
        spec: 
            template: 
                spec: 
                    securityContext: 
                        fsGroup: {gid}
                        runAsUser: {uid}
                        runAsGroup: {gid}
    ```

### NTP in Kubernetes Cluster

[https://medium.com/goglides/ntp-in-a-kubernetes-cluster-4c6c3e5c0c14](https://medium.com/goglides/ntp-in-a-kubernetes-cluster-4c6c3e5c0c14)

## References

1. [eks使用efs dynamic provisioning 创建非root容器提示 Operation not permitted](https://blog.csdn.net/weixin_47430049/article/details/122834893)
2. [Amazon EKS 中 EFS 持久性存储](https://www.cnsre.cn/posts/220110850573/#%E9%83%A8%E7%BD%B2%E9%9D%99%E6%80%81%E4%BE%9B%E7%BB%99)
