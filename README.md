DataPlug
========

A simple graph data manager, in other words: on the fly schemaless multi-model data client with timeseries wannabees.

Inspired by InfluxDB, ElasticSearch and other cool stuffs that do not cover a little thing: Graphization !


Main requirements for devs
==========================

Dataplug supports the last updates of Arango and its python driver.

 + [Python driver for Arango](https://github.com/joowani/python-arango) version > 4
 + [ArangoDB](https://www.arangodb.com) version >= 3.3
	    A multi-model no-sql graph database



Installation
============

```
pip install dataplug
```

Quick start
===========

```
import dataplug

server_config = { "host":"localhost",
                  "port": 7144,
                  "username": "root",
                  "password":"autoGeneRatEd" }

# Creating a node, locally
A = dataplug.Node(domain="db1",
                  collection="collection1",
                  data={"name":"NODE_A", "value":3.14},
                  client_config=server_config)

# Saving it into database
if A.upsave():
    print(A.key())

# Creating another node
B = dataplug.Node(domain="db1",
                  collection="collection2",
                  data={"name":"NODE_B", "value":1.41},
                  client_config=server_config)

# Saving it into database
B.upsave()

# Creating an edge between these nodes
edgeAB = dataplug.Edge("db1", A, B)

# Adding information to the edge
edgeAB.add_field("strength", "high")

# Saving it into database
edgeAB.upsave()

```

Update your node data
=====================

 - That replaces data totally with newdata dictionnary:
 ```
    node.data = newdata
 ```

 - That searches of similar node in the database and updates/adds data:
 ```
    node.sync()
 ```

 - To append/update data with newdata use:
 ```
    node.data.update(newdata)
 ```

Testing
=======

```
pytest -v tests
```
