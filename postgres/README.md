## ** IN CONSTRUCTION ** 


docker-compose up
access db:

docker exec -it my_postgres psql -U postgres postgres
SELECT * FROM pg_create_logical_replication_slot('slot', 'test_decoding');


reference for PG CDC : https://www.postgresql.org/docs/9.5/logicaldecoding-example.html


build go app with vendor: go build -mod vendor 


kafka -> https://linuxhint.com/docker_compose_kafka/
https://github.com/abhirockzz/kafka-go-docker-quickstart/blob/master/producer/kafka-producer.go


$ docker exec -it kafka bash
$ ## To create a new topic named test
bash-4.4# kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic test
 
## To start a producer that publishes datastream from standard input to kafka
bash-4.4# kafka-console-producer.sh --broker-list localhost:9092 --topic test

##docker

docker build -t 133thiago/gocdc:latest .
docker push 133thiago/gocdc:latest