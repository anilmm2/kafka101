
# Kafka
This setup uses confluent's community version of kafka on docker.
Running the following setup needs *docker-desktop* installed.


## Running kafka broker in docker 
* This is a *server* component
* Create a new directory *kafka101* and copy *docker-compose.yml* into this directory
* cd to *kafka101* and run the following

```
docker-compose up -d
```


## Kafka CLI
* Following commands can be used to test your kafka setup.
  These are available in confluentinc/cp-kafka docker image that is used to run kafka broker.
* Run the following to create a shell into a running container.  
  kafka-* commands can be run in this shell.
* Multiple instances of this shell can be run.

```
docker exec -it kafka101-kafka-1 bash
```

NOTE: In some docker installations "-" might need to be replaced with "_"

* Following commands can be run in this shell

#### List topics
```
kafka-topics -list --bootstrap-server localhost:9092
```

#### Create topic
```
kafka-topics --create --topic quickstart-events --bootstrap-server localhost:9092
```
```
Created topic quickstart-events.
```
Try *List topics* now.

#### Get topic metadata
```
kafka-topics --describe --topic quickstart-events --bootstrap-server localhost:9092
```
```
Topic: quickstart-events	TopicId: njGCyB5NRlOL5LrWbM0S0g	PartitionCount: 1	ReplicationFactor: 1	Configs:
	Topic: quickstart-events	Partition: 0	Leader: 1	Replicas: 1	Isr: 1
```


#### Produce messages
* Type messages after running the following command
* Each line is a message
* End with ctrl+c
```
kafka-console-producer --topic quickstart-events --bootstrap-server localhost:9092
line 1
line 2

```

#### Consume messages
* This will list all the messages
```
kafka-console-consumer --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```

## Shutting down
* When done run the following to shut down the broker
```
docker-compose down
```

## Cleanup
* Data is stored in the docker volume *VOL_KAFKA_DATA*. This makes the data persistent across restarts.
To delete it run the following docker command after shutting down kafka broker.
```
docker volume rm kafka_VOL_KAFKA_DATA
```