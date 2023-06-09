# Scan Operation Hints<a name="EN-US_TOPIC_0289900472"></a>

## Function<a name="en-us_topic_0283137382_en-us_topic_0237121537_section290819468377"></a>

These hints specify a scan operation, which can be  **tablescan**,  **indexscan**, or  **indexonlyscan**.

## Syntax<a name="en-us_topic_0283137382_en-us_topic_0237121537_section17380317104213"></a>

```
[no] tablescan|indexscan|indexonlyscan(table [index])
```

## Parameter Description<a name="en-us_topic_0283137382_en-us_topic_0237121537_section35087980143822"></a>

-   **no**  indicates that the specified hint will not be used for scanning.

-   **table **specifies the table to be scanned. You can specify only one table. Use a table alias \(if any\) instead of a table name.
-   **index **indicates the index for  **indexscan**  or  **indexonlyscan**. You can specify only one index.

>![](public_sys-resources/icon-note.gif) **NOTE:** 
>**indexscan**  and  **indexonlyscan**  hints can be used only when the specified index belongs to the table.
>Scan operation hints can be used for row-store tables, column-store tables, HDFS tables, OBS tables, and subquery tables. HDFS internal tables include base tables and delta tables. The delta tables are invisible to users. Therefore, scan operation hints are used only for base tables.

## Example<a name="en-us_topic_0283137382_en-us_topic_0237121537_section1127715590585"></a>

To specify an index-based hint for a scan, create an index named  **i**  on the  **i\_item\_sk**  column of the  **item**  table.

```
create index i on item(i_item_sk);
```

Hint the query plan in  [Examples](plan-hint-optimization.md#en-us_topic_0283137554_en-us_topic_0237121532_section671421102912)  as follows:

```
explain
select /*+ indexscan(item i) */ i_product_name product_name ...
```

**item**  is scanned based on an index. The optimized plan is as follows:

![](figures/en-us_image_0283137339.png)

