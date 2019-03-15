# kafka-resources

Can a broke have multiple partitions of same topic ?

- Broker
	- These are the nodes (container, VMs) of the kafka cluster, also known as bootstrap servers
	- Topic - Replication (Leader, In-Sync Replicas)
		- Partitions (is this equal to number of Broker nodes deployed?)
		- Partitions have offsets, which is just the sequence or order of the data stored in them
	- Data in topics are immutable (cannot change it), they are ordered		

- Producers (acks=0, acks=1, acks=all)
	- Write data to a topic
	- Keys associated with the message decide which broker to store it on

- Messages
	- Sent by Producers
	- Have Key
	
- Consumers
	- Read data from topic
	- They read from a particular partition of the topic
	- If number of partitions are less than consumers, some consumer will be inactive, i.e., a consumer requires an available partition to read the data
	- Consumers can be grouped
	- Commit offsets to _consumer_offset, when a consumer reads the data
	- At most once, At least once, Exactly once