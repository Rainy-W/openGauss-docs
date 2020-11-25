# CREATE USER<a name="ZH-CN_TOPIC_0289899951"></a>

## 功能描述<a name="zh-cn_topic_0283136891_zh-cn_topic_0237122125_zh-cn_topic_0059778166_s08b0f056b5f14492970a9037c63fa70c"></a>

创建一个用户。

## 注意事项<a name="zh-cn_topic_0283136891_zh-cn_topic_0237122125_zh-cn_topic_0059778166_sd48f2980b9464b1abca65a4747930552"></a>

-   通过CREATE USER创建的用户，默认具有LOGIN权限；
-   通过CREATE USER创建用户的同时系统会在执行该命令的数据库中，为该用户创建一个同名的SCHEMA；其他数据库中，则不自动创建同名的SCHEMA；用户可使用CREATE SCHEMA命令，分别在其他数据库中，为该用户创建同名SCHEMA。
-   系统管理员在普通用户同名schema下创建的对象，所有者为schema的同名用户（非系统管理员）。

## 语法格式<a name="zh-cn_topic_0283136891_zh-cn_topic_0237122125_zh-cn_topic_0059778166_s93c6eaefe7c447408b7d42ff86e6035f"></a>

```
CREATE USER user_name [ [ WITH ] option [ ... ] ] [ ENCRYPTED | UNENCRYPTED ] { PASSWORD | IDENTIFIED BY } { 'password' [EXPIRED] | DISABLE };
```

其中option子句用于设置权限及属性等信息。

```
{SYSADMIN | NOSYSADMIN}
    | {AUDITADMIN | NOAUDITADMIN}
    | {CREATEDB | NOCREATEDB}
    | {USEFT | NOUSEFT}
    | {CREATEROLE | NOCREATEROLE}
    | {INHERIT | NOINHERIT}
    | {LOGIN | NOLOGIN}
    | {REPLICATION | NOREPLICATION}
    | {INDEPENDENT | NOINDEPENDENT}
    | {VCADMIN | NOVCADMIN}
    | CONNECTION LIMIT connlimit
    | VALID BEGIN 'timestamp'
    | VALID UNTIL 'timestamp'
    | RESOURCE POOL 'respool'
    | PERM SPACE 'spacelimit'
    | TEMP SPACE 'tmpspacelimit'
    | SPILL SPACE 'spillspacelimit'
    | IN ROLE role_name [, ...]
    | IN GROUP role_name [, ...]
    | ROLE role_name [, ...]
    | ADMIN role_name [, ...]
    | USER role_name [, ...]
    | SYSID uid
    | DEFAULT TABLESPACE tablespace_name
    | PROFILE DEFAULT
    | PROFILE profile_name
    | PGUSER
```

## 参数说明<a name="zh-cn_topic_0283136891_zh-cn_topic_0237122125_zh-cn_topic_0059778166_s65dbaae3763942599852d585997c77dd"></a>

-   **user\_name**

    用户名称。

    取值范围：字符串，要符合标识符的命名规范。且最大长度不超过63个字符。

-   **password**

    登录密码。

    密码规则如下：

    -   密码默认不少于8个字符。
    -   不能与用户名及用户名倒序相同。
    -   至少包含大写字母（A-Z），小写字母（a-z），数字（0-9），非字母数字字符（限定为\~!@\#$%^&\*\(\)-\_=+\\|\[\{\}\];:,<.\>/?）四类字符中的三类字符。
    -   创建用户时，应当使用双引号或单引号将用户密码括起来。

    取值范围：字符串。


CREATE USER的其他参数值请参考[CREATE ROLE](CREATE-ROLE.md)。

## 示例<a name="zh-cn_topic_0283136891_zh-cn_topic_0237122125_zh-cn_topic_0059778166_sfbca773f5bcd4799b3ea668b3eb074fa"></a>

```
--创建用户jim，登录密码为Bigdata@123。
postgres=# CREATE USER jim PASSWORD 'Bigdata@123';

--下面语句与上面的等价。
postgres=# CREATE USER kim IDENTIFIED BY 'Bigdata@123';

--如果创建有“创建数据库”权限的用户，则需要加CREATEDB关键字。
postgres=# CREATE USER dim CREATEDB PASSWORD 'Bigdata@123';

--将用户jim的登录密码由Bigdata@123修改为Abcd@123。
postgres=# ALTER USER jim IDENTIFIED BY 'Abcd@123' REPLACE 'Bigdata@123';

--为用户jim追加CREATEROLE权限。
postgres=# ALTER USER jim CREATEROLE;

--将enable_seqscan的值设置为on， 设置成功后，在下一会话中生效。
postgres=# ALTER USER jim SET enable_seqscan TO on;

--重置jim的enable_seqscan参数。
postgres=# ALTER USER jim RESET enable_seqscan;

--锁定jim帐户。
postgres=# ALTER USER jim ACCOUNT LOCK;

--删除用户。
postgres=# DROP USER kim CASCADE;
postgres=# DROP USER jim CASCADE;
postgres=# DROP USER dim CASCADE;
```

## 相关链接<a name="zh-cn_topic_0283136891_zh-cn_topic_0237122125_zh-cn_topic_0059778166_sf40b399700a74bd7b2d37e445d057f6e"></a>

[ALTER USER](ALTER-USER.md)，[CREATE ROLE](CREATE-ROLE.md)，[DROP USER](zh-cn_topic_0289900387.md)

