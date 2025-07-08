### July 2nd week 2025
- Only kafka consumers need a group id, producers don't need it and a consumer isn't required to have a match in ids (apart from topic_name) to receive message.
  - this is for load balancing, resource mgmt within group etc
- KafkaJS lib allows to create producers and consumers in a node app
  - create a kafka instance with `const kafka = new Kafka(/*connection settings*/)` and
  - create producer with `const producer = kafka.producer()`
  - send message with `producer.send({ topic: topicName, messages: []})`
- 
