# Restrictions<a name="EN-US_TOPIC_0000001216722064"></a>

Publication-subscription is implemented based on logical replication and inherits all restrictions of logical replication. In addition, publication-subscription has the following additional restrictions or missing functions.

-   Database schemas and DDL commands are not replicated. Initial schemas can be manually copied by using  **pg\_dump --schema-only**. Subsequent schema changes need to be manually synchronized.
-   Sequence data is not replicated. The data in serial or identifier columns backed by the sequence in the background will be replicated as part of the table, but the sequence itself will still display the start value on the subscriber. If the subscriber is used as a read-only database, this is usually not a problem. However, if some kind of switchover or failover to the subscriber database is intended, the sequence needs to be updated to the latest value, either by copying the current data from the publisher \(perhaps using  **pg\_dump**\) or by determining a sufficiently large value from the tables themselves.
-   Only tables, including partitioned tables, can be replicated. Attempts to replicate other types of relations, such as views, materialized views, or foreign tables, will result in errors.
-   Multiple subscriptions in the same database cannot subscribe to the same publication \(that is, publish the same table\). Otherwise, duplicate data or primary key conflicts may occur.
-   If a published table contains data types that do not support B-tree or hash indexes \(such as the geography types\), the table must have a primary key so that UPDATE and DELETE operations can be successfully replicated to the subscription side. Otherwise, the replication will fail, and the message "FATAL: could not identify an equality operator for type xx" will be displayed on the subscription side.

