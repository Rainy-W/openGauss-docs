# SELECT<a name="ZH-CN_TOPIC_0289900232"></a>

## 功能描述<a name="zh-cn_topic_0283136463_zh-cn_topic_0237122184_zh-cn_topic_0059777449_s65596fb5f1d44a428e41dd508d2044a7"></a>

SELECT用于从表或视图中取出数据。

SELECT语句就像叠加在数据库表上的过滤器，利用SQL关键字从数据表中过滤出用户需要的数据。

## 注意事项<a name="zh-cn_topic_0283136463_zh-cn_topic_0237122184_zh-cn_topic_0059777449_s42c37979749545719ac9114594f45d93"></a>

-   对比原openGauss的SELECT语法，新增了WHERE子句下的sounds like语法。

## 语法格式<a name="zh-cn_topic_0283136463_zh-cn_topic_0237122184_zh-cn_topic_0059777449_sb7329222602d46fe944bf6c300931dd2"></a>

-   查询数据

```
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [/*+ plan_hint */] [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
{ * | {expression [ [ AS ] output_name ]} [, ...] }
[ FROM from_item [, ...] ]
[ WHERE condition ]
[ [ START WITH condition ] CONNECT BY [NOCYCLE] condition [ ORDER SIBLINGS BY expression ] ]
[ GROUP BY grouping_element [, ...] ]
[ HAVING condition [, ...] ]
[ WINDOW {window_name AS ( window_definition )} [, ...] ]
[ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
[ ORDER BY {expression [ [ ASC | DESC | USING operator ] | nlssort_expression_clause ] [ NULLS { FIRST | LAST } ]} [, ...] ]
[ LIMIT { [offset,] count | ALL } ]
[ OFFSET start [ ROW | ROWS ] ]
[ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
[ {FOR { UPDATE | NO KEY UPDATE | SHARE | KEY SHARE } [ OF table_name [, ...] ] [ NOWAIT ]} [...] ];
```

-   其中group子句为：

    ```
    ( )
    | expression
    | ( expression [, ...] )
    | rollup_clause
    | CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    | GROUPING SETS ( grouping_element [, ...] )
    ```

    rollup_clause子句为：

    ```
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    | { expression | ( expression [, ...] ) } WITH ROLLUP
    ```


## 参数说明<a name="zh-cn_topic_0283136463_zh-cn_topic_0237122184_zh-cn_topic_0059777449_sa812f65b8e8c4c638ec7840697222ddc"></a>

-   **WHERE子句**
    1. sounds like是condition的一种语法，用法如：column_name sounds like '字符'; 相当于soundex(column_name) = soundex('字符')的对比结果，是一个boolean的值。用于通过soundex处理来查询满足条件的数据。

![](public_sys-resources/icon-note.gif) **说明：** 
涉及的其它参数说明可见[SELECT](SELECT.md)。

## 示例<a name="zh-cn_topic_0283136463_zh-cn_topic_0237122184_zh-cn_topic_0059777449_sc1b5e63c90c946b89430696c38fc86c0"></a>

--SOUNDS LIKE子句示例：同音字段查询

```
openGauss=# CREATE TABLE TEST(id int, name varchar);
openGauss=# INSERT INTO TEST VALUES(1, 'too');
openGauss=# SELECT * FROM TEST WHERE name SOUNDS LIKE 'two';
 id | name
----+------
  1 | too
(1 row)
```

```
--SELECT GROUP BY子句中使用ROLLUP。
openGauss=# CREATE TABLESPACE t_tbspace ADD DATAFILE 'my_tablespace' ENGINE = test_engine;
CREATE TABLESPACE
openGauss=# CREATE TABLE t_with_rollup(id int, name varchar(20), area varchar(50), count int);
CREATE TABLE
openGauss=# INSERT INTO t_with_rollup values(1, 'a', 'A', 10);
INSERT 0 1
openGauss=# INSERT INTO t_with_rollup values(2, 'b', 'B', 15);
INSERT 0 1
openGauss=# INSERT INTO t_with_rollup values(2, 'b', 'B', 20);
INSERT 0 1
openGauss=# INSERT INTO t_with_rollup values(3, 'c', 'C', 50);
INSERT 0 1
openGauss=# INSERT INTO t_with_rollup values(3, 'c', 'C', 15);
INSERT 0 1
openGauss=# SELECT name, sum(count) FROM t_with_rollup GROUP BY ROLLUP(name);
 name | sum
------+-----
 a    |  10
 b    |  35
 c    |  65
      | 110
(4 rows)

openGauss=# SELECT name, sum(count) FROM t_with_rollup GROUP BY (name) WITH ROLLUP;
 name | sum
------+-----
 a    |  10
 b    |  35
 c    |  65
      | 110
(4 rows)
```

## 相关链接<a name="section156744489391"></a>

[SELECT](SELECT.md)