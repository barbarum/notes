# Kafka

## List of Commands

```bash
./bin/kafka-consumer-groups.sh --bootstrap-server kafka-n3:9092 --group business-engine-python --topic mall-merged-tracks --reset-offsets --shift-by 1 --execute
./bin/kafka-consumer-groups.sh --bootstrap-server kafka-n3:9092 --group business-engine-python --topic mall-merged-tracks --reset-offsets --to-latest --execute
./bin/kafka-consumer-groups.sh --bootstrap-server kafka-n3:9092 --group humanlocalization-python --topic mall-tracks --reset-offsets --shift-by 1 --execute


/opt/kafka_2.12-2.3.0/bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list localhost:9092 --topic mall-tracks
/opt/kafka_2.12-2.3.0/bin/kafka-topics.sh --zookeeper zookeeper:2181 --describe --topic mall-tracks

/opt/kafka_2.12-2.3.0/bin/kafka-consumer-groups.sh --bootstrap-server kafka:9092 --group trackaggregation --describe
/opt/kafka_2.12-2.3.0/bin/kafka-topics.sh --zookeeper zookeeper-n3:2181 --delete --topic mall-track
/opt/kafka_2.12-2.3.0/bin/kafka-consumer-groups.sh --bootstrap-server kafka:9092 --group trackaggregation --topic mall-tracks --reset-offsets --to-latest --execute
/opt/kafka_2.12-2.3.0/bin/kafka-consumer-groups.sh --bootstrap-server kafka:9092 --group trackaggregation --topic mall-tracks --reset-offsets --shift-by -100 --execute
/opt/kafka_2.12-2.3.0/bin/kafka-consumer-groups.sh --bootstrap-server kafka-n3:9092 --topic mall-tracks --delete --group LocalizeTracks

bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list localhost:9092 --topic mall-tracks --time -1

# Get timestamp offset information
/opt/kafka_2.12-2.3.0/bin/kafka-run-class.sh kafka.tools.DumpLogSegments --deep-iteration --print-data-log --files /var/lib/kafka/mall-tracks-1/00000000000002536641.timeindex
```
