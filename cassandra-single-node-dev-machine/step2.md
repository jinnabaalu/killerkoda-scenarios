Now we try to connect to the the cassandra container to check the status of the cassandra node. 

Container is nothing but a standalone environment on a different virtual machine, so we can connect to running container just to like connect to any machine with ssh using `docker exec -it cassandra bash`{{execute}}

We will enter into the container root user, with all cassandra related configurations and installations in place. This gives us a feel of virtual machine having cassandra installed in it. now lets run `nodetool` commands. 

*Nodetool*, is a command line interface for managing the cluster. 

- Check the status of the nodes `nodetool status`{{execute}}
- Describe Cluster `nodetool describecluster`{{execute}}
- Check the Garbage collection stats `nodetool gcstats`{{execute}}
- Cleanup the keyspaces and partition keys no longer belong to cluster `nodetool cleanup`{{execute}}
- Flush one or more tables from the keyspace or all data `nodetool flush`{{execute}}

*Cassandra Query Language - CQL*, used as a client to connect the cassandra. Let's run some cql command to create the keyspace and tables. 

- Initialize the CQL Client with `cqlsh`{{execute}}

- Create cycling keyspace on a single node evaluation cluster: `CREATE KEYSPACE IF NOT EXISTS cycling WITH REPLICATION = { 'class' : 'NetworkTopologyStrategy', 'dc1' : 3, 'dc2' : 2};`{{execute}}

- Use the keyspace `USE cycling;`{{execute}}

- Update a keyspace in the cluster and change its replication strategy options 

`CREATE KEYSPACE cycling
  WITH REPLICATION = { 
   'class' : 'SimpleStrategy', 
   'replication_factor' : 1 
  };`{{execute}}

- Create the cyclist_name table with UUID as the primary key

`
CREATE TABLE cycling.cyclist_name ( 
   id UUID PRIMARY KEY, 
   lastname text, 
   firstname text );
`{{execute}}

- Add IF NOT EXISTS to the command to ensure that the operation is not performed if a row with the same primary key already exists

`
INSERT INTO cycling.cyclist_name (id, lastname, firstname) 
   VALUES (c4b65263-fe58-4846-83e8-f0e1c13d518f, 'RATTO', 'Rissella') 
IF NOT EXISTS; 
`{{execute}}

- Use a simple SELECT query to display all data from a table

`
SELECT * FROM cycling.cyclist_name;
`{{execute}}
