# DROP TABLE<a name="EN-US_TOPIC_0242370616"></a>

## Function<a name="en-us_topic_0237122152_en-us_topic_0059778107_s74e2e8764aa64af1b093f8f68069bce6"></a>

**DROP TABLE**  deletes a table.

## Precautions<a name="en-us_topic_0237122152_en-us_topic_0059778107_sdcf8f26a27a64e52b7099ca3ce0256b6"></a>

**DROP TABLE**  forcibly deletes the specified table and the indexes depending on the table. After the table is deleted, the functions and stored procedures that need to use this table cannot be executed. Deleting a partitioned table also deletes all partitions in the table.

## Syntax<a name="en-us_topic_0237122152_en-us_topic_0059778107_s6fa866d73d5c4158836c9fdd0ad5b3ac"></a>

```
DROP TABLE [ IF EXISTS ] 
    { [schema.]table_name } [, ...] [ CASCADE | RESTRICT ];
```

## Parameter Description<a name="en-us_topic_0237122152_en-us_topic_0059778107_sa6ea557919e84c0db8ed5cbb227fa983"></a>

-   **IF EXISTS**

    Reports a notice instead of an error if the specified table does not exist.

-   **schema**

    Specifies the schema name.

-   **table\_name**

    Specifies the name of the table to be deleted.

-   **CASCADE | RESTRICT**
    -   **CASCADE**: automatically deletes the objects \(such as views\) that depend on the table.
    -   **RESTRICT**: refuses to delete the table if any objects depend on it. This is the default action.


## Examples<a name="en-us_topic_0237122152_en-us_topic_0059778107_s1af12a7c6e4e456f9fc72da9c90358ff"></a>

See  [Example:](create-table.md#en-us_topic_0237122117_en-us_topic_0059778169_s86758dcf05d442d2a9ebd272e76ed1b8)  in  **CREATE TABLE**.

## Helpful Links<a name="en-us_topic_0237122152_en-us_topic_0059778107_s08580f38742d47efa6a955c9385d6ae2"></a>

[ALTER TABLE](alter-table.md)  and  [CREATE TABLE](create-table.md)

