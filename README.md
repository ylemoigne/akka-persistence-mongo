Mongo Journal for Akka Persistence
==================================

A replicated [Akka Persistence](http://doc.akka.io/docs/akka/2.3-M2/scala/persistence.html) journal backed by [MongoDB Casbah](http://mongodb.github.io/casbah/).

Prerequisites
-------------

<table border="0">
  <tr>
    <td>Akka version: </td>
    <td>2.3-M2 or higher</td>
  </tr>
  <tr>
    <td>Mongo version: </td>
    <td>2.4.8 or higher</td>
  </tr>
</table>

Installation
------------

Build and install the journal plugin to your local Ivy cache with `sbt publishLocal` (requires sbt 0.13). It can then be included as dependency:

    libraryDependencies += "com.github.ddevore" %% "akka-persistence-mongo" % "0.1-SNAPSHOT"

Configuration
-------------

To activate the Mongo journal plugin, add the following line to your Akka `application.conf`:

    akka.persistence.journal.plugin = "casbah-journal"

This will run the journal with its default settings. The default settings can be changed with the following configuration keys:

- `casbah-journal.mongo-url`. A comma-separated list of contact points in a Cassandra cluster. Default value is `mongodb://localhost:27017/store.messages`.

For more information on configuring the `mongo-url` see [Connection String Uri Format](http://docs.mongodb.org/manual/reference/connection-string/).

The default write concern is `WriteConcern.Safe`. This will be configurable sometime in the future.

- `WriteConcern.Safe` will handle `Exceptions` are raised for network issues, and server errors; waits on a server for the write operation.
- To better understand MongoDB `WriteConcern` see [Write Concern](http://docs.mongodb.org/manual/core/write-concern/).

Status
------

- All operations required by the Akka Persistence [journal plugin API](http://doc.akka.io/docs/akka/2.3-M2/scala/persistence.html#journal-plugin-api) are supported.
- Message writes are batched to optimize throughput. When using channels, confirmation writes are not batched yet.
- Sharding is not yet supported.
- This should be considered **experimental** as Akka-Persistence is still changing and the underlying storage structure may change.