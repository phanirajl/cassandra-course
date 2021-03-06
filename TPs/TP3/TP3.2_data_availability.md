TP3.2) Data availability
========================

***Scenario***: *play with data replication*

### Cluster with no replication

The keyspace we created has been setup with a replication factor set to 1 (i.e. no replicatoin). 

Let's suppose one node is fallen...

* stop the node-2 docker (from a host terminal):
```
docker stop cassandra-node-2 
```
* Open a cqlsh from cassandra-node-1 (in [scope](http://localhost:4040)) , and query the data from 'paris': 
```
cqlsh> use my_keyspace ;
cqlsh:my_keyspace> SELECT * from temperature_by_city where city = 'paris' ;
```
* then,  query the data from 'berlin', and then, from 'londres'.
* finally, query the data from all cities:
```
cqlsh:my_keyspace> SELECT * from temperature_by_city;
```
What's happening ?

### Cluster with replication (RF=2)
***Scenario***: *use replication factor (RF) and consistency level (CL)*

Let's now have some data replication. 
* restart all nodes:
```
docker-compose up -d
```
* From any node create a new *my_keyspace_rf2* keyspace with replication (RF=2):
```
cqlsh> SOURCE '/TPs/TP3/create_keyspace_rf2.cql'
cqlsh> USE my_keyspace_rf2;
cqlsh> SOURCE '/TPs/TP1/create_table_temperature_by_city.cql'
cqlsh> SOURCE '/TPs/TP1/insert_dataset_for_temperature_by_city.cql'
```

* Again, shutdown a node, and query the data from 'paris', 'berlin' 'londres' as we earlier did [with no replication](#user-content-cluster-with-no-replication). Conclusion ?

[>> Next (TP3.3_tunable_consistency.md)](TP3.3_tunable_consistency.md)
