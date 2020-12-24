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
- Create a keyspace `CREATE KEYSPACE IF NOT EXISTS cycling WITH REPLICATION = { 'class' : 'NetworkTopologyStrategy', 'datacenter1' : 3 };`{{execute}}
- Use the keyspace `USE cycling;`{{execute}}
- Update a keyspace in the cluster and change its replication strategy options `ALTER KEYSPACE system_auth WITH REPLICATION = {'class' : 'NetworkTopologyStrategy', 'dc1' : 3, 'dc2' : 2};`{{execute}}
- Create tables
`
CREATE TABLE cycling.cyclist_alt_stats ( id UUID PRIMARY KEY, lastname text, birthday timestamp, nationality text, weight text, height text );

CREATE TABLE cycling.whimsey ( id UUID PRIMARY KEY, lastname text, cyclist_teams set<text>, events list<text>, teams map<int,text> );

CREATE TABLE cycling.route (race_id int, race_name text, point_id int, lat_long tuple<text, tuple<float,float>>, PRIMARY KEY (race_id, point_id));
`{{execute}}

- Insert and Query the data in cassandra
`
CREATE TABLE cycling.rank_by_year_and_name ( 
  race_year int, 
  race_name text, 
  cyclist_name text, 
  rank int, 
  PRIMARY KEY ((race_year, race_name), rank) );

INSERT INTO cycling.rank_by_year_and_name (race_year, race_name, cyclist_name, rank) 
   VALUES (2015, 'Tour of Japan - Stage 4 - Minami > Shinshu', 'Benjamin PRADES', 1);
INSERT INTO cycling.rank_by_year_and_name (race_year, race_name, cyclist_name, rank) 
   VALUES (2015, 'Tour of Japan - Stage 4 - Minami > Shinshu', 'Adam PHELAN', 2);
INSERT INTO cycling.rank_by_year_and_name (race_year, race_name, cyclist_name, rank) 
   VALUES (2015, 'Tour of Japan - Stage 4 - Minami > Shinshu', 'Thomas LEBAS', 3);
INSERT INTO cycling.rank_by_year_and_name (race_year, race_name, cyclist_name, rank) 
   VALUES (2015, 'Giro d''Italia - Stage 11 - Forli > Imola', 'Ilnur ZAKARIN', 1);
INSERT INTO cycling.rank_by_year_and_name (race_year, race_name, cyclist_name, rank) 
   VALUES (2015, 'Giro d''Italia - Stage 11 - Forli > Imola', 'Carlos BETANCUR', 2);
INSERT INTO cycling.rank_by_year_and_name (race_year, race_name, cyclist_name, rank) 
   VALUES (2014, '4th Tour of Beijing', 'Phillippe GILBERT', 1);
INSERT INTO cycling.rank_by_year_and_name (race_year, race_name, cyclist_name, rank)  
   VALUES (2014, '4th Tour of Beijing', 'Daniel MARTIN', 2);
INSERT INTO cycling.rank_by_year_and_name (race_year, race_name, cyclist_name, rank)  
   VALUES (2014, '4th Tour of Beijing', 'Johan Esteban CHAVES', 3);
`{{execute}}
- Use a simple SELECT query to display all data from a table.
`
SELECT * FROM cycling.cyclist_category;
`{{execute}}

- The example below illustrates how to create a query that uses category as a filter.
`
SELECT * FROM cycling.cyclist_category WHERE category = 'SPRINT';
`{{execute}}
- Pick the columns to display instead of choosing all data and limit
`
cqlsh> SELECT category, points, lastname FROM cycling.cyclist_category LIMIT 3;
`{{execute}}
