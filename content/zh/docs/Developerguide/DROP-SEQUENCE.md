# DROP SEQUENCE<a name="ZH-CN_TOPIC_0242370613"></a>

## 功能描述<a name="zh-cn_topic_0237122149_zh-cn_topic_0059778402_section892464917343"></a>

从当前数据库里删除序列。

## 注意事项<a name="zh-cn_topic_0237122149_zh-cn_topic_0059778402_section3924194973416"></a>

只有序列的所有者或者系统管理员才能删除。

## 语法格式<a name="zh-cn_topic_0237122149_zh-cn_topic_0059778402_section292414499345"></a>

```
DROP SEQUENCE [ IF EXISTS ] {[schema.]sequence_name} [ , ... ] [ CASCADE | RESTRICT ];
```

## 参数说明<a name="zh-cn_topic_0237122149_zh-cn_topic_0059778402_section1692544913344"></a>

-   **IF EXISTS**

    如果指定的序列不存在，则发出一个notice而不是抛出一个错误。

-   **name**

    序列名称。

-   **CASCADE**

    级联删除依赖序列的对象。

-   **RESTRICT**

    如果存在任何依赖的对象，则拒绝删除序列。此项是缺省值。


## 示例<a name="zh-cn_topic_0237122149_zh-cn_topic_0059778402_section13928174913345"></a>

```
--创建一个名为serial的递增序列，从101开始。
postgres=# CREATE SEQUENCE serial START 101;

--删除序列。
postgres=# DROP SEQUENCE serial;
```

## 相关链接<a name="zh-cn_topic_0237122149_zh-cn_topic_0059778402_section365162034413"></a>

[ALTER SEQUENCE](ALTER-SEQUENCE.md)，  [DROP SEQUENCE](DROP-SEQUENCE.md)

