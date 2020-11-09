# DROP INDEX<a name="EN-US_TOPIC_0242370604"></a>

## Function<a name="en-us_topic_0237122140_en-us_topic_0059779018_s6e7bed7d44604f749e4ea7043f81b07b"></a>

**DROP INDEX**  deletes an index.

## Precautions<a name="en-us_topic_0237122140_en-us_topic_0059779018_saafc32e8c71d4cb7b7d30678c9e4658d"></a>

Only the owner of an index or a system administrator has the  **DROP INDEX**  permission.

## Syntax<a name="en-us_topic_0237122140_en-us_topic_0059779018_s79208f25fe214e06b6c7f661c030f3d1"></a>

```
DROP INDEX [ CONCURRENTLY ] [ IF EXISTS ] 
    index_name [, ...] [ CASCADE | RESTRICT ];
```

## Parameter Description<a name="en-us_topic_0237122140_en-us_topic_0059779018_s99e6f6efb9f3448f9de8894607958cd3"></a>

-   **CONCURRENTLY**

    Deletes an index without locking it. A normal  **DROP INDEX**  acquires exclusive lock on the table on which the index depends, blocking other accesses until the index drop can be completed. With this option, the statement does not lock the table during index deletion.

    This parameter allows only one index name and does not support  **CASCADE**.

    The  **DROP INDEX**  statement can be run within a transaction, but  **DROP INDEX CONCURRENTLY**  cannot.

-   **IF EXISTS**

    Reports a notice instead of an error if the specified index does not exist.

-   **index\_name**

    Specifies the index name to be deleted.

    Value range: an existing index

-   **CASCADE | RESTRICT**
    -   **CASCADE**: automatically deletes the objects that depend on the index.
    -   **RESTRICT**: refuses to delete the index if any objects depend on it. This is the default action.


## Examples<a name="en-us_topic_0237122140_en-us_topic_0059779018_s95dd4a9a45334e81be4841d86d7a47f1"></a>

See  [Examples](create-index.md#en-us_topic_0237122106_en-us_topic_0059777455_s985289833081489e9d77c485755bd362)  in  **CREATE INDEX**.

## Helpful Links<a name="en-us_topic_0237122140_en-us_topic_0059779018_s299c55b981d1489986df6a6cf27b73d1"></a>

[ALTER INDEX](alter-index.md)  and  [CREATE INDEX](create-index.md)

