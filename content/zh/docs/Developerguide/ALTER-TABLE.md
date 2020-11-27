# ALTER TABLE<a name="ZH-CN_TOPIC_0289899912"></a>

## 功能描述<a name="zh-cn_topic_0283137126_zh-cn_topic_0237122076_zh-cn_topic_0059779051_s2baab5c876044795a12b5949f22d2144"></a>

修改表，包括修改表的定义、重命名表、重命名表中指定的列、重命名表的约束、设置表的所属模式、添加/更新多个列、打开/关闭行访问控制开关。

## 注意事项<a name="zh-cn_topic_0283137126_zh-cn_topic_0237122076_zh-cn_topic_0059779051_s8ea536d5b8ff459e9e3614e35f53bc2a"></a>

-   只有表的所有者或者被授予了表ALTER权限的用户有权限执行ALTER TABLE命令，系统管理员默认拥有此权限。但要修改表的所有者或者修改表的模式，当前用户必须是该表的所有者或者系统管理员，且该用户是新所有者角色的成员。
-   不能修改分区表的tablespace，但可以修改分区的tablespace。
-   不支持修改存储参数ORIENTATION。
-   SET SCHEMA操作不支持修改为系统内部模式，当前仅支持用户模式之间的修改。
-   列存表只支持PARTIAL CLUSTER KEY表级约束，不支持主外键等表级约束。
-   列存表只支持添加字段ADD COLUMN、修改字段的数据类型ALTER TYPE、设置单个字段的收集目标SET STATISTICS、支持更改表名称、支持更改表空间，支持删除字段DROP COLUMN。对于添加的字段和修改的字段类型要求是列存支持的[数据类型](zh-cn_topic_0289900421.md)。ALTER TYPE的USING选项只支持常量表达式和涉及本字段的表达式，暂不支持涉及其他字段的表达式。
-   列存表支持的字段约束包括NULL、NOT NULL和DEFAULT常量值；对字段约束的修改当前只支持对DEFAULT值的修改（SET DEFAULT）和删除（DROP DEFAULT），暂不支持对非空约束NULL/NOT NULL的修改。

-   不支持增加自增列，或者增加DEFAULT值中包含nextval\(\)表达式的列。
-   不支持对外表、临时表开启行访问控制开关。
-   通过约束名删除PRIMARY KEY约束时，不会删除NOT NULL约束，如果有需要，请手动删除NOT NULL约束。
-   使用JDBC时，支持通过PrepareStatement对DEFAUTL值进行参数化设置。

## 语法格式<a name="zh-cn_topic_0283137126_zh-cn_topic_0237122076_zh-cn_topic_0059779051_s58bdce220c9f4292ba9af919b04ad25c"></a>

-   修改表的定义。

    ```
    ALTER TABLE [ IF EXISTS ] { table_name [*] | ONLY table_name | ONLY ( table_name ) }
        action [, ... ];
    ```

    其中具体表操作action可以是以下子句之一：

    ```
    column_clause
        | ADD table_constraint [ NOT VALID ]
        | ADD table_constraint_using_index
        | VALIDATE CONSTRAINT constraint_name
        | DROP CONSTRAINT [ IF EXISTS ]  constraint_name [ RESTRICT | CASCADE ]
        | CLUSTER ON index_name
        | SET WITHOUT CLUSTER
        | SET ( {storage_parameter = value} [, ... ] )
        | RESET ( storage_parameter [, ... ] )
        | OWNER TO new_owner
        | SET TABLESPACE new_tablespace
        | SET {COMPRESS|NOCOMPRESS}
        | TO { GROUP groupname | NODE ( nodename [, ... ] ) }
        | ADD NODE ( nodename [, ... ] )
        | DELETE NODE ( nodename [, ... ] )
        | DISABLE TRIGGER [ trigger_name | ALL | USER ]
        | ENABLE TRIGGER [ trigger_name | ALL | USER ]
        | ENABLE REPLICA TRIGGER trigger_name
        | ENABLE ALWAYS TRIGGER trigger_name
        | DISABLE ROW LEVEL SECURITY
        | ENABLE ROW LEVEL SECURITY
        | FORCE ROW LEVEL SECURITY
        | NO FORCE ROW LEVEL SECURITY
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   **ADD table\_constraint \[ NOT VALID \]**
    >    给表增加一个新的约束。
    >-   **ADD table\_constraint\_using\_index**
    >    根据已有唯一索引为表增加主键约束或唯一约束。
    >-   **VALIDATE CONSTRAINT constraint\_name**
    >    验证一个使用NOT VALID选项创建的检查类约束，通过扫描全表来保证所有记录都符合约束条件。如果约束已标记为有效时，什么操作也不会发生。
    >-   **DROP CONSTRAINT \[ IF EXISTS \]  constraint\_name \[ RESTRICT | CASCADE \]**
    >    删除一个表上的约束。
    >-   **CLUSTER ON index\_name**
    >    为将来的CLUSTER（聚簇）操作选择默认索引。实际上并没有重新盘簇化处理该表。
    >-   **SET WITHOUT CLUSTER**
    >    从表中删除最新使用的CLUSTER索引。这样会影响将来那些没有声明索引的CLUSTER（聚簇）操作。
    >-   **SET \( \{storage\_parameter = value\} \[, ... \] \)**
    >    修改表的一个或多个存储参数。
    >-   **RESET \( storage\_parameter \[, ... \] \)**
    >    重置表的一个或多个存储参数。与SET一样，根据参数的不同可能需要重写表才能获得想要的效果。
    >-   **OWNER TO new\_owner**
    >    将表、序列、视图的属主改变成指定的用户。
    >-   **SET TABLESPACE new\_tablespace**
    >    这种形式将表空间修改为指定的表空间并将相关的数据文件移动到新的表空间。但是表上的所有索引都不会被移动，索引可以通过ALTER INDEX语法的SET TABLESPACE选项来修改索引的表空间。
    >-   **SET \{COMPRESS|NOCOMPRESS\}**
    >    修改表的压缩特性。表压缩特性的改变只会影响后续批量插入的数据的存储方式，对已有数据的存储毫无影响。也就是说，表压缩特性的修改会导致该表中同时存在着已压缩和未压缩的数据。
    >-   **TO \{ GROUP groupname | NODE \( nodename \[, ... \] \) \}**
    >    此语法仅在扩展模式（GUC参数support\_extended\_features为on时）下可用。该模式谨慎打开，主要供内部扩容工具使用，一般用户不应使用该模式。
    >-   **ADD NODE \( nodename \[, ... \] \)**
    >    此语法主要供内部扩容工具使用，一般用户不建议使用。
    >-   **DELETE NODE \( nodename \[, ... \] \)**
    >    此语法主要供内部缩容工具使用，一般用户不建议使用。
    >-   **DISABLE TRIGGER \[ trigger\_name | ALL | USER \]**
    >    禁用trigger\_name所表示的单个触发器，或禁用所有触发器，或仅禁用用户触发器（此选项不包括内部生成的约束触发器，例如，可延迟唯一性和排除约束的约束触发器）。
    >    应谨慎使用此功能，因为如果不执行触发器，则无法保证原先期望的约束的完整性。
    >-   **| ENABLE TRIGGER \[ trigger\_name | ALL | USER \]**
    >    启用trigger\_name所表示的单个触发器，或启用所有触发器，或仅启用用户触发器。
    >-   **| ENABLE REPLICA TRIGGER trigger\_name**
    >    触发器触发机制受配置变量[session\_replication\_role](zh-cn_topic_0289900775.md#zh-cn_topic_0283136752_zh-cn_topic_0237124732_zh-cn_topic_0059779117_sffbd1c48d86b4c3fa3287167a7810216)的影响，当复制角色为“origin”（默认值）或“local”时，将触发简单启用的触发器。
    >    配置为ENABLE REPLICA的触发器仅在会话处于“replica”模式时触发。
    >-   **| ENABLE ALWAYS TRIGGER trigger\_name**
    >    无论当前复制模式如何，配置为ENABLE ALWAYS的触发器都将触发。
    >-   **| DISABLE/ENABLE ROW LEVEL SECURITY**
    >    开启或关闭表的行访问控制开关。
    >    当开启行访问控制开关时，如果未在该数据表定义相关行访问控制策略，数据表的行级访问将不受影响；如果关闭表的行访问控制开关，即使定义了行访问控制策略，数据表的行访问也不受影响。详细信息参见[CREATE ROW LEVEL SECURITY POLICY](zh-cn_topic_0289901001.md)章节。
    >-   **| NO FORCE/FORCE ROW LEVEL SECURITY**
    >    强制开启或关闭表的行访问控制开关。
    >    默认情况，表所有者不受行访问控制特性影响，但当强制开启表的行访问控制开关时，表的所有者（不包含系统管理员用户）会受影响。系统管理员可以绕过所有的行访问控制策略，不受影响。

    -   其中列相关的操作column\_clause可以是以下子句之一：

        ```
        ADD [ COLUMN ] column_name data_type [ compress_mode ] [ COLLATE collation ] [ column_constraint [ ... ] ]    
        | MODIFY column_name data_type    
        | MODIFY column_name [ CONSTRAINT constraint_name ] NOT NULL [ ENABLE ]
        | MODIFY column_name [ CONSTRAINT constraint_name ] NULL
        | DROP [ COLUMN ] [ IF EXISTS ] column_name [ RESTRICT | CASCADE ]    
        | ALTER [ COLUMN ] column_name [ SET DATA ] TYPE data_type [ COLLATE collation ] [ USING expression ]    
        | ALTER [ COLUMN ] column_name { SET DEFAULT expression | DROP DEFAULT }    
        | ALTER [ COLUMN ] column_name { SET | DROP } NOT NULL    
        | ALTER [ COLUMN ] column_name SET STATISTICS [PERCENT] integer    
        | ADD STATISTICS (( column_1_name, column_2_name [, ...] ))    
        | DELETE STATISTICS (( column_1_name, column_2_name [, ...] ))    
        | ALTER [ COLUMN ] column_name SET ( {attribute_option = value} [, ... ] )    
        | ALTER [ COLUMN ] column_name RESET ( attribute_option [, ... ] )    
        | ALTER [ COLUMN ] column_name SET STORAGE { PLAIN | EXTERNAL | EXTENDED | MAIN }
        ```

        >![](public_sys-resources/icon-note.gif) **说明：** 
        >-   **ADD \[ COLUMN \] column\_name data\_type \[ compress\_mode \] \[ COLLATE collation \] \[ column\_constraint \[ ... \] \]**
        >    向表中增加一个新的字段。用ADD COLUMN增加一个字段，所有表中现有行都初始化为该字段的缺省值（如果没有声明DEFAULT子句，值为NULL）。
        >-   **ADD \( \{ column\_name data\_type \[ compress\_mode \] \} \[, ...\] \)**
        >    向表中增加多列。
        >-   **MODIFY \( \{ column\_name data\_type | column\_name \[ CONSTRAINT constraint\_name \] NOT NULL \[ ENABLE \] | column\_name \[ CONSTRAINT constraint\_name \] NULL \} \[, ...\] \)**
        >    修改表已存在字段的数据类型。
        >-   **DROP \[ COLUMN \] \[ IF EXISTS \] column\_name \[ RESTRICT | CASCADE \]**
        >    从表中删除一个字段，和这个字段相关的索引和表约束也会被自动删除。如果任何表之外的对象依赖于这个字段，必须声明CASCADE ，比如视图。
        >    DROP COLUMN命令并不是物理上把字段删除，而只是简单地把它标记为对SQL操作不可见。随后对该表的插入和更新将在该字段存储一个NULL。因此，删除一个字段是很快的，但是它不会立即释放表在磁盘上的空间，因为被删除了的字段占据的空间还没有回收。这些空间将在执行VACUUM时而得到回收。
        >-   **ALTER \[ COLUMN \] column\_name \[ SET DATA \] TYPE data\_type \[ COLLATE collation \] \[ USING expression \]**
        >    改变表字段的数据类型。该字段涉及的索引和简单的表约束将被自动地转换为使用新的字段类型，方法是重新分析最初提供的表达式。
        >    ALTER TYPE要求重写整个表的特性有时候是一个优点，因为重写的过程消除了表中没用的空间。比如，要想立刻回收被一个已经删除的字段占据的空间，最快的方法是
        >    ```
        >    ALTER TABLE table ALTER COLUMN anycol TYPE anytype;
        >    ```
        >    这里的anycol是任何在表中还存在的字段，而anytype是和该字段的原类型一样的类型。这样的结果是在表上没有任何可见的语意的变化，但是这个命令强迫重写，这样就删除了不再使用的数据。
        >-   **ALTER \[ COLUMN \] column\_name \{ SET DEFAULT expression | DROP DEFAULT \}**
        >    为一个字段设置或者删除缺省值。请注意缺省值只应用于随后的INSERT命令，它们不会修改表中已经存在的行。也可以为视图创建缺省，这个时候它们是在视图的ON INSERT规则应用之前插入到INSERT句中的。
        >-   **ALTER \[ COLUMN \] column\_name \{ SET | DROP \} NOT NULL**
        >    修改一个字段是否允许NULL值或者拒绝NULL值。如果表在字段中包含非NULL，则只能使用SET NOT NULL。
        >-   **ALTER \[ COLUMN \] column\_name SET STATISTICS \[PERCENT\] integer**
        >    为随后的ANALYZE操作设置针对每个字段的统计收集目标。目标的范围可以在0到10000之内设置。设置为-1时表示重新恢复到使用系统缺省的统计目标。
        >-   **\{ADD | DELETE\} STATISTICS \(\(column\_1\_name, column\_2\_name \[, ...\]\)\)**
        >    用于添加和删除多列统计信息声明（不实际进行多列统计信息收集），以便在后续进行全表或全库analyze时进行多列统计信息收集。每组多列统计信息最多支持32列。不支持添加/删除多列统计信息声明的表：系统表、外表。
        >-   **ALTER \[ COLUMN \] column\_name SET \( \{attribute\_option = value\} \[, ... \] \)**
        >    **ALTER \[ COLUMN \] column\_name RESET \( attribute\_option \[, ... \] \)**
        >    设置/重置属性选项。
        >    目前，属性选项只定义了n\_distinct和n\_distinct\_inherited。n\_distinct影响表本身的统计值，而n\_distinct\_inherited影响表及其继承子表的统计。目前，只支持SET/RESET n\_distinct参数，禁止SET/RESET n\_distinct\_inherited参数。
        >-   **ALTER \[ COLUMN \] column\_name SET STORAGE \{ PLAIN | EXTERNAL | EXTENDED | MAIN \}**
        >    为一个字段设置存储模式。这个设置控制这个字段是内联保存还是保存在一个附属的表里，以及数据是否要压缩。仅支持对行存表的设置；对列存表没有意义，执行时报错。SET STORAGE本身并不改变表上的任何东西，只是设置将来的表操作时，建议使用的策略。

        -   其中列约束column\_constraint为：

            ```
            [ CONSTRAINT constraint_name ]
                { NOT NULL |
                  NULL |
                  CHECK ( expression ) |
                  DEFAULT default_expr  |
                  UNIQUE index_parameters |
                  PRIMARY KEY index_parameters }
                [ DEFERRABLE | NOT DEFERRABLE | INITIALLY DEFERRED | INITIALLY IMMEDIATE ]
            ```

        -   其中列的压缩可选项compress\_mode为：

            ```
            [ DELTA | PREFIX | DICTIONARY | NUMSTR | NOCOMPRESS ]
            ```


    -   其中根据已有唯一索引为表增加主键约束或唯一约束table\_constraint\_using\_index为：

        ```
        [ CONSTRAINT constraint_name ]
            { UNIQUE | PRIMARY KEY } USING INDEX index_name
            [ DEFERRABLE | NOT DEFERRABLE | INITIALLY DEFERRED | INITIALLY IMMEDIATE ]
        ```

    -   其中表约束table\_constraint为：

        ```
        [ CONSTRAINT constraint_name ]
            { CHECK ( expression ) |
              UNIQUE ( column_name [, ... ] ) index_parameters |
              PRIMARY KEY ( column_name [, ... ] ) index_parameters |
              PARTIAL CLUSTER KEY ( column_name [, ... ] }
            [ DEFERRABLE | NOT DEFERRABLE | INITIALLY DEFERRED | INITIALLY IMMEDIATE ]
        ```

        其中索引参数index\_parameters为：

        ```
        [ WITH ( {storage_parameter = value} [, ... ] ) ]
            [ USING INDEX TABLESPACE tablespace_name ]
        ```



-   重命名表。对名称的修改不会影响所存储的数据。

    ```
    ALTER TABLE [ IF EXISTS ] table_name 
        RENAME TO new_table_name;
    ```

-   重命名表中指定的列。

    ```
    ALTER TABLE [ IF EXISTS ] { table_name [*] | ONLY table_name | ONLY ( table_name )}
        RENAME [ COLUMN ] column_name TO new_column_name;
    ```

-   重命名表的约束。

    ```
    ALTER TABLE [ IF EXISTS ] { table_name [*] | ONLY table_name | ONLY ( table_name ) }
        RENAME CONSTRAINT constraint_name TO new_constraint_name;
    ```

-   设置表的所属模式。

    ```
    ALTER TABLE [ IF EXISTS ] table_name 
        SET SCHEMA new_schema;
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   这种形式把表移动到另外一个模式。相关的索引、约束都跟着移动。目前序列不支持改变schema。 若该表拥有序列，需要将序列删除，重建，或者取消拥有关系， 才能将表schema更改成功。
    >-   要修改一个表的模式，用户必须在新模式上拥有CREATE权限。要把该表添加为一个父表的新子表，用户必须同时又是父表的所有者。要修改所有者，用户还必须是新的所有角色的直接或间接成员，并且该成员必须在此表的模式上有CREATE权限。这些限制规定了该用户不能做出了重建和删除表之外的事情。不过，系统管理员可以以任何方式修改任意表的所有权限。
    >-   除了RENAME和SET SCHEMA之外所有动作都可以捆绑在一个经过多次修改的列表中并行使用。比如，可以在一个命令里增加几个字段或修改几个字段的类型。对于大表，此种操作带来的效率提升更明显，原因在于只需要对该大表做一次处理。
    >-   增加一个CHECK或NOT NULL约束将会扫描该表，以保证现有的行符合约束要求。
    >-   用一个非空缺省值增加一个字段或者改变一个字段的现有类型会重写整个表。对于大表来说，这个操作可能会花很长时间，并且它还临时需要两倍的磁盘空间。

-   添加多个列。

    ```
    ALTER TABLE [ IF EXISTS ] table_name
        ADD ( { column_name data_type [ compress_mode ] [ COLLATE collation ] [ column_constraint [ ... ] ]} [, ...] );
    ```

-   更新多个列。

    ```
    ALTER TABLE [ IF EXISTS ] table_name 
        MODIFY ( { column_name data_type | column_name [ CONSTRAINT constraint_name ] NOT NULL [ ENABLE ] | column_name [ CONSTRAINT constraint_name ] NULL } [, ...] );
    ```


## 参数说明<a name="zh-cn_topic_0283137126_zh-cn_topic_0237122076_zh-cn_topic_0059779051_sf4962205ddf84312a5fd888bc662e5cf"></a>

-   **IF EXISTS**

    如果不存在相同名称的表，不会抛出一个错误，而会发出一个通知，告知表不存在。

-   **table\_name  \[\*\] | ONLY table\_name | ONLY \( table\_name  \)**

    table\_name是需要修改的表名。

    若声明了ONLY选项，则只有那个表被更改。若未声明ONLY，该表及其所有子表都将会被更改。另外，可以在表名称后面显示地增加\*选项来指定包括子表，即表示所有后代表都被扫描，这是默认行为。

-   **constraint\_name**

    要删除的现有约束的名称。

-   **index\_name**

    索引名称。

-   **storage\_parameter**

    表的存储参数的名称。

-   **new\_owner**

    表新拥有者的名称。

-   **new\_tablespace**

    表所属新的表空间名称。

-   **column\_name**，**column\_1\_name， column\_2\_name**

    现存的或新字段的名称。

-   **data\_type**

    新字段的类型，或者现存字段的新类型。

-   **compress\_mode**

    表字段的压缩可选项，当前仅对行存表有效。该子句指定该字段优先使用的压缩算法。

-   **collation**

    字段排序规则名称。可选字段COLLATE指定了新字段的排序规则，如果省略，排序规则为新字段的默认类型。排序规则可以使用“select \* from pg\_collation”命令从pg\_collation系统表中查询，默认的排序规则为查询结果中以default开始的行。

-   **USING expression**

    USING子句声明如何从旧的字段值里计算新的字段值；如果省略，缺省从旧类型向新类型的赋值转换。如果从旧数据类型到新类型没有隐含或者赋值的转换，则必须提供一个USING子句。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >ALTER TYPE的USING选项实际上可以声明涉及该行旧值的任何表达式，即它可以引用除了正在被转换的字段之外其他的字段。这样，就可以用ALTER TYPE语法做非常普遍性的转换。因为这个灵活性，USING表达式并没有作用于该字段的缺省值（如果有的话），结果可能不是缺省表达式要求的常量表达式。这就意味着如果从旧类型到新类型没有隐含或者赋值转换的话，即使存在USING子句，ALTER TYPE也可能无法把缺省值转换成新的类型。在这种情况下，应该用DROP DEFAULT先删除缺省，执行ALTER TYPE，然后使用SET DEFAULT增加一个合适的新缺省值。类似的考虑也适用于涉及该字段的索引和约束。

-   **NOT NULL | NULL**

    设置列是否允许空值。

-   **integer**

    带符号的整数常值。当使用PERCENT时表示按照表数据的百分比收集统计信息，integer的取值范围为0-100。

-   **attribute\_option**

    属性选项。

-   **PLAIN | EXTERNAL | EXTENDED | MAIN**

    字段存储模式。

    -   PLAIN必需用于定长的数值（比如integer）并且是内联的、不压缩的。
    -   MAIN用于内联、可压缩的数据。
    -   EXTERNAL用于外部保存、不压缩的数据。使用EXTERNAL将令在text和bytea字段上的子字符串操作更快，但付出的代价是增加了存储空间。
    -   EXTENDED用于外部的压缩数据，EXTENDED是大多数支持非PLAIN存储的数据的缺省。

-   **CHECK \( expression \)**

    每次将要插入的新行或者将要被更新的行必须使表达式结果为真才能成功，否则会抛出一个异常并且不会修改数据库。

    声明为字段约束的检查约束应该只引用该字段的数值，而在表约束里出现的表达式可以引用多个字段。

    目前，CHECK表达式不能包含子查询也不能引用除当前行字段之外的变量。

-   **DEFAULT default\_expr**

    给字段指定缺省值。

    缺省表达式的数据类型必须和字段类型匹配。

    缺省表达式将被用于任何未声明该字段数值的插入操作。如果没有指定缺省值则缺省值为NULL 。

-   **UNIQUE index\_parameters**

    **UNIQUE \( column\_name \[, ... \] \) index\_parameters**

    UNIQUE约束表示表里的一个或多个字段的组合必须在全表范围内唯一。

-   **PRIMARY KEY index\_parameters**

    **PRIMARY KEY \( column\_name \[, ... \] \) index\_parameters**

    主键约束表明表中的一个或者一些字段只能包含唯一（不重复）的非NULL值。

-   **DEFERRABLE | NOT DEFERRABLE | INITIALLY DEFERRED | INITIALLY IMMEDIATE**

    设置该约束是否可推迟。

    -   DEFERRABLE：可以推迟到事务结尾使用SET CONSTRAINTS命令检查。
    -   NOT DEFERRABLE：在每条命令之后马上检查。
    -   INITIALLY IMMEDIATE：那么每条语句之后就立即检查它。
    -   INITIALLY DEFERRED：只有在事务结尾才检查它。

-   **WITH \( \{storage\_parameter = value\} \[, ... \] \)**

    为表或索引指定一个可选的存储参数。

-   **tablespace\_name**

    索引所在表空间的名称。

-   **COMPRESS|NOCOMPRESS**
    -   NOCOMPRESS：如果指定关键字NOCOMPRESS则不会修改表的现有压缩特性。
    -   COMPRESS：如果指定COMPRESS关键字，则对该表进行批量插入元组时触发该特性。

-   **new\_table\_name**

    修改后新的表名称。

-   **new\_column\_name**

    表中指定列修改后新的列名称。

-   **new\_constraint\_name**

    修改后表约束的新名称。

-   **new\_schema**

    修改后新的模式名称。

-   **CASCADE**

    级联删除依赖于被依赖字段或者约束的对象（比如引用该字段的视图）。

-   **RESTRICT**

    如果字段或者约束还有任何依赖的对象，则拒绝删除该字段。这是缺省行为。

-   **schema\_name**

    表所在的模式名称。


## 示例<a name="zh-cn_topic_0283137126_zh-cn_topic_0237122076_zh-cn_topic_0059779051_se4f9dc97861c410bb51554bb58bcd76d"></a>

请参考CREATE TABLE的[示例](zh-cn_topic_0289900279.md#zh-cn_topic_0283137629_zh-cn_topic_0237122117_zh-cn_topic_0059778169_s86758dcf05d442d2a9ebd272e76ed1b8)。

## 相关链接<a name="zh-cn_topic_0283137126_zh-cn_topic_0237122076_zh-cn_topic_0059779051_s489a6430be6447c193a4011257dc4994"></a>

[CREATE TABLE](zh-cn_topic_0289900279.md)，[DROP TABLE](DROP-TABLE.md)

