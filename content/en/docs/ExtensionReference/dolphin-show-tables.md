# SHOW TABLES<a name="ZH-CN_TOPIC_0289900448"></a>

## Function<a name="en-us_topic_0283137542_en-us_topic_0237122167_en-us_topic_0059778902_s86b6c9741c7741d3976c5e358e8d5486"></a>

Views the list of tables in the current database or schema.

## Precautions<a name="en-us_topic_0283137542_en-us_topic_0237122167_en-us_topic_0059778902_sdd2da7fe44624eb99ee77013ff96c6bd"></a>

- If db\_name is not specified, the list of tables in the current database (or schema) is queried.

## Syntax<a name="en-us_topic_0283137542_en-us_topic_0237122167_en-us_topic_0059778902_se242be9719f44731b261539dbd42d7b9"></a>

```
SHOW [FULL] TABLES
   [{FROM | IN} db_name]
   [LIKE 'pattern' | WHERE expr]
```

## Parameter Description<a name="en-us_topic_0283137542_en-us_topic_0237122167_en-us_topic_0059778902_s06dfa4f09bfd4e0d9826a80e6a91b0a6"></a>

- **db_name**

   Specifies the database name (or schema). This parameter is optional. If it is not specified, the current database or schema is queried.

- **LIKE 'pattern'**

   The pattern matches the first column (column name: 'Tables_in_dbname [`pattern`]') in the displayed result.

## Examples<a name="en-us_topic_0283137542_en-us_topic_0237122167_en-us_topic_0059778902_sfff14489321642278317cf06cd89810d"></a>

```
--Create a simple table:
openGauss=# CREATE SCHEMA tst_schema;
openGauss=# SET SEARCH_PATH TO tst_schema;

openGauss=# CREATE TABLE tst_t1
openGauss-# (
openGauss(# id int primary key,
openGauss(# name varchar(20) NOT NULL,
openGauss(# addr text COLLATE "de_DE",
openGauss(# phone text COLLATE "es_ES",
openGauss(# addr_code text
openGauss(# );
openGauss=# CREATE VIEW tst_v1 AS SELECT * FROM tst_t1;
openGauss=# CREATE TABLE t_t2(id int);

--View the list of tables in the database (or schema).
openGauss=# show tables;
 Tables_in_tst_schema 
----------------------
 tst_t1
 tst_v1
 t_t2

openGauss=# show full tables;
 Tables_in_tst_schema | Table_type 
----------------------+------------
 tst_t1               | BASE TABLE
 tst_v1               | VIEW
 t_t2                 | BASE TABLE

openGauss=# show full tables in tst_schema;
 Tables_in_tst_schema | Table_type 
----------------------+------------
 tst_t1               | BASE TABLE
 tst_v1               | VIEW
 t_t2                 | BASE TABLE
 
--Fuzzy match and filtering
openGauss=# show full tables like '%tst%';
 Tables_in_tst_schema (%tst%) | Table_type 
------------------------------+------------
 tst_t1                       | BASE TABLE
 tst_v1                       | VIEW

openGauss=# show full tables where Table_type='VIEW';
 Tables_in_tst_schema | Table_type 
----------------------+------------
 tst_v1               | VIEW
 
```
