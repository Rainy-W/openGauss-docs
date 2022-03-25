# Quick Setup<a name="EN-US_TOPIC_0000001261641897"></a>

Set the following configuration items in the  **postgresql.conf**  file:

```
wal_level = logical
```

For a basic setup, retain the default values for the other required settings.

You need to adjust the  **pg\_hba.conf**  file to allow replication \(the value depends on the actual network configuration and the user used for connection\).

```
host     all     repuser     0.0.0.0/0     sha256
```

In the publisher database:

```
CREATE PUBLICATION mypub FOR TABLE users, departments;
```

In the subscriber database:

```
CREATE SUBSCRIPTION mysub CONNECTION 'dbname=foo host=bar user=repuser' PUBLICATION mypub;
```

The above statement starts the replication process, replicating incremental changes to those tables.

