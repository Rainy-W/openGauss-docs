# REINDEX<a name="ZH-CN_TOPIC_0242370638"></a>

## 功能描述<a name="zh-cn_topic_0237122174_zh-cn_topic_0059777511_sf1cc0970ae31445a9e063cf504569e6e"></a>

为表中的数据重建索引。

在以下几种情况下需要使用REINDEX重建索引：

-   索引崩溃，并且不再包含有效的数据。
-   索引变得“臃肿”，包含大量的空页或接近空页。
-   为索引更改了存储参数（例如填充因子），并且希望这个更改完全生效。
-   使用CONCURRENTLY选项创建索引失败，留下了一个“非法”索引。


## 注意事项<a name="zh-cn_topic_0237122174_zh-cn_topic_0059777511_s871de483556241f0a3180925ed04ded3"></a>

REINDEX DATABASE和SYSTEM这种形式的重建索引不能在事务块中执行。

## 语法格式<a name="zh-cn_topic_0237122174_zh-cn_topic_0059777511_s2ba0db3344cd44189859fbd0cefdd97f"></a>

-   重建普通索引。

    ```
    REINDEX { INDEX | [INTERNAL] TABLE | DATABASE | SYSTEM } name [ FORCE ];
    ```


-   重建索引分区。

    ```
    REINDEX  { INDEX|  [INTERNAL] TABLE} name
        PARTITION partition_name [ FORCE  ];
    ```


## 参数说明<a name="zh-cn_topic_0237122174_zh-cn_topic_0059777511_s68dcdc2270944092a61b8e6fb6f09a48"></a>

-   **INDEX**

    重新建立指定的索引。

-   **INTERNAL TABLE**

    重建列存表或Hadoop内表的Desc表的索引，如果表有从属的"TOAST"表，则这个表也会重建索引。

-   **TABLE**

    重新建立指定表的所有索引，如果表有从属的"TOAST"表，则这个表也会重建索引。

-   **DATABASE**

    重建当前数据库里的所有索引。

-   **SYSTEM**

    在当前数据库上重建所有系统表上的索引。不会处理在用户表上的索引。

-   **name**

    需要重建索引的索引、表、数据库的名称。表和索引可以有模式修饰。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >REINDEX DATABASE和SYSTEM只能重建当前数据库的索引，所以name必须和当前数据库名称相同。  

-   **FORCE**

    无效选项，会被忽略。

-   **partition\_name**

    需要重建索引的分区的名称或者索引分区的名称。

    取值范围：

    -   如果前面是REINDEX INDEX，则这里应该指定索引分区的名称；
    -   如果前面是REINDEX TABLE，则这里应该指定分区的名称；
    -   如果前面是REINDEX INTERNAL TABLE，则这里应该指定列存分区表的分区的名称。


>![](public_sys-resources/icon-notice.gif) **须知：**   
>REINDEX DATABASE和SYSTEM这种形式的重建索引不能在事务块中执行。  

## 示例<a name="zh-cn_topic_0237122174_zh-cn_topic_0059777511_saeb969f6c052407e98c22893941c9440"></a>

```
--创建一个行存表tpcds.customer_t1，并在tpcds.customer_t1表上的c_customer_sk字段创建索引。
postgres=# CREATE TABLE tpcds.customer_t1
(
    c_customer_sk             integer               not null,
    c_customer_id             char(16)              not null,
    c_current_cdemo_sk        integer                       ,
    c_current_hdemo_sk        integer                       ,
    c_current_addr_sk         integer                       ,
    c_first_shipto_date_sk    integer                       ,
    c_first_sales_date_sk     integer                       ,
    c_salutation              char(10)                      ,
    c_first_name              char(20)                      ,
    c_last_name               char(30)                      ,
    c_preferred_cust_flag     char(1)                       ,
    c_birth_day               integer                       ,
    c_birth_month             integer                       ,
    c_birth_year              integer                       ,
    c_birth_country           varchar(20)                   ,
    c_login                   char(13)                      ,
    c_email_address           char(50)                      ,
    c_last_review_date        char(10)
)
WITH (orientation = row)

postgres=# CREATE INDEX tpcds_customer_index1 ON tpcds.customer_t1 (c_customer_sk);

postgres=# INSERT INTO tpcds.customer_t1 SELECT * FROM tpcds.customer WHERE c_customer_sk < 10;

--重建一个单独索引。
postgres=# REINDEX INDEX tpcds.tpcds_customer_index1;

--重建表tpcds.customer_t1上的所有索引。
postgres=# REINDEX TABLE tpcds.customer_t1;

--删除tpcds.customer_t1表。
postgres=# DROP TABLE tpcds.customer_t1;
```

## 优化建议<a name="zh-cn_topic_0237122174_zh-cn_topic_0059777511_section21815038152246"></a>

-   INTERNAL TABLE

    此种情况大多用于故障恢复，不建议进行并发操作。

-   DATABASE

    不能在事务中reindex database。

-   SYSTEM

    不能在事务中reindex系统表。


