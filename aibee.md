# AIBEE

## Login to dev servers

```bash
ssh -t dwei@gpu604.aibee.cn "cd aibee/mall-solution/mall-indexer; bash" # gpu604 

bin/clean.sh conf/cfg2/dev/gpu604.aibee.cn/dwei/application.yaml && bin/build.sh 

bin/run.sh hdfs --hdfs /staging/customer/WANDA/bj/tzwd/tracking/lite/20190728/09041517/sv/pb --start 090000 --end 123000 --config conf/cfg2/dev/gpu604.aibee.cn/dwei/application.yaml --process_count 8 # DID
sleep 2h && bin/run.sh hdfs --hdfs /staging/customer/WANDA/bj/tzwd/tracking/lite/20190728/08292126/sv/pb --start 114000 --end 115000 --config conf/cfg2/dev/gpu604.aibee.cn/dwei/application.yaml --process_count 8 &

bin/docker.sh -d python src/pid_group_merge.py --conf conf/cfg2/dev/gpu604.aibee.cn/dwei/application.yaml

## Ingest events
bin/docker.sh -d python scripts/ingestion/ingest_events.py --conf conf/cfg2/dev/gpu604.aibee.cn/dwei/application.yaml --src /ssd/detection_events/ 
```

## 解除labels

```bash
cpu- gpu- notmaster- post-processing- zookeeper-volume-1- zookeeper-volume-2- zookeeper-volume-3- kafka-volume-1- kafka-volume-2- kafka-volume-3- seaweedfs-master-1- seaweedfs-master-2- seaweedfs-master-3- zookeeper- kafka- seaweedfs-master- seaweedfs-volume- notmaster- mall- data-vpn- mysql- mongo- seaweedfs-filer- airflow-
```

## 针对3台CPU服务器，分别执行以下命令

```bash
kubectl label nodes gpu620.aibee.cn cpu=true zookeeper-volume=1 kafka-volume=1 seaweedfs-master-volume=1 zookeeper=true kafka=true seaweedfs-master=true seaweedfs-volume=true notmaster=true post-processing=true
kubectl label nodes gpu621.aibee.cn cpu=true zookeeper-volume=2 kafka-volume=2 seaweedfs-master-volume=2 zookeeper=true kafka=true seaweedfs-master=true seaweedfs-volume=true notmaster=true mall=true seaweedfs-filer=true mysql=true mongo=true
kubectl label nodes gpu622.aibee.cn cpu=true zookeeper-volume=3 kafka-volume=3 seaweedfs-master-volume=3 zookeeper=true kafka=true seaweedfs-master=true seaweedfs-volume=true notmaster=true post-processing=true airflow=true


kubectl label nodes gpu624.aibee.cn cpu=true zookeeper-volume=1 kafka-volume=1 seaweedfs-master-volume=1 zookeeper=true kafka=true seaweedfs-master=true seaweedfs-volume=true notmaster=true post-processing=true
kubectl label nodes gpu625.aibee.cn cpu=true zookeeper-volume=2 kafka-volume=2 seaweedfs-master-volume=2 zookeeper=true kafka=true seaweedfs-master=true seaweedfs-volume=true notmaster=true mall=true seaweedfs-filer=true mysql=true mongo=true


kubectl label nodes <your-cpu-server> cpu- gpu- notmaster- post-processing- zookeeper-volume-1- zookeeper-volume-2- zookeeper-volume-3- kafka-volume-1- kafka-volume-2- kafka-volume-3- seaweedfs-master-1- seaweedfs-master-2- seaweedfs-master-3- zookeeper- kafka- seaweedfs-master- seaweedfs-volume- notmaster- mall- data-vpn- mysql- mongo- seaweedfs-filer- airflow- datavpn-
```

## 针对1台GPU服务器，执行以下命令

```bash
kubectl label nodes gpu623.aibee.cn gpu=true notmaster=true post-processing=true 
```

## 删除PP某摄像头数据

```bash
cd /mnt/data/prod/customer/GZCI/guangzhou/mowgz/tracking/singleview/{date} 
rm -v ch21021*
```
