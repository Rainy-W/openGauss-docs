# SET<a name="EN-US_TOPIC_0242370650"></a>

## Function<a name="en-us_topic_0237122186_en-us_topic_0059779029_s8a5c6264f78f49e3aa93f388d68cd3e6"></a>

**SET**  modifies a run-time parameter.

## Precautions<a name="en-us_topic_0237122186_en-us_topic_0059779029_s8cb7444b58764d99913a4cc61f397f9f"></a>

Most run-time parameters can be modified by executing  **SET**. Some parameters cannot be modified after a server or session starts.

## Syntax<a name="en-us_topic_0237122186_en-us_topic_0059779029_s29888afda1844d6f9fc677f1b59b5b7d"></a>

-   Set the system time zone.

    ```
    SET [ SESSION | LOCAL ] TIME ZONE { timezone | LOCAL | DEFAULT };
    ```

-   Set the schema of the table.

    ```
    SET [ SESSION | LOCAL ] 
        {CURRENT_SCHEMA { TO | = } { schema | DEFAULT }
        | SCHEMA 'schema'};
    ```

-   Set client encoding.

    ```
    SET [ SESSION | LOCAL ] NAMES encoding_name;
    ```

-   Set XML parsing mode.

    ```
    SET [ SESSION | LOCAL ] XML OPTION { DOCUMENT | CONTENT };
    ```

-   Set other run-time parameters.

    ```
    SET [ LOCAL | SESSION ]
        { {config_parameter { { TO | = } { value | DEFAULT } 
                            | FROM CURRENT }}};
    ```


## Parameter Description<a name="en-us_topic_0237122186_en-us_topic_0059779029_s39823c7ebd854a9f9c761b3a32b1c3c3"></a>

-   **SESSION**

    Specifies that the specified parameters take effect for the current session. This is the default value if neither  **SESSION**  nor  **LOCAL**  appears.

    If  **SET**  or  **SET SESSION**  is executed within a transaction that is later aborted, the effects of the  **SET**  statement disappear when the transaction is rolled back. Once the surrounding transaction is committed, the effects will persist until the end of the session, unless overridden by another  **SET**.

-   **LOCAL**

    Specifies that the specified parameters take effect for the current transaction. After  **COMMIT**  or  **ROLLBACK**, the session-level setting takes effect again.

    The effects of  **SET LOCAL**  last only till the end of the current transaction, whether committed or not. A special case is  **SET**  followed by  **SET LOCAL**  within a single transaction: the  **SET LOCAL**  value will be seen until the end of the transaction, but afterward \(if the transaction is committed\) the  **SET**  value will take effect.

-   **TIME ZONE timezone**

    Specifies the local time zone for the current session.

    Value range: a valid local time zone. The corresponding run-time parameter is  **TimeZone**. The default value is  **PRC**.

-   **CURRENT\_SCHEMA**

    **schema**

    Specifies the current schema.

    Value range: an existing schema name

-   **SCHEMA schema**

    Specifies the current schema. Here the schema is a string.

    Example: set schema 'public';

-   **NAMES encoding\_name**

    Specifies the client character encoding. This statement is equivalent to  **set client\_encoding to encoding\_name**.

    Value range: a valid character encoding name. The run-time parameter corresponding to this option is  **client\_encoding**. The default encoding is  **SQL\_ASCII**.

-   **XML OPTION option**

    Specifies the XML parsing mode.

    Value range:  **CONTENT**  \(default\) and  **DOCUMENT**

-   **config\_parameter**

    Specifies the name of a configurable run-time parameter. You can use  **SHOW ALL**  to view available run-time parameters.

-   **value**

    Specifies the new value of  **config\_parameter**. This parameter can be specified as string constants, identifiers, numbers, or comma-separated lists of these.  **DEFAULT**  can be written to indicate resetting the parameter to its default value.


## Examples<a name="en-us_topic_0237122186_en-us_topic_0059779029_s51d29fa208274032a4e5308b57638421"></a>

```
-- Set the search path of a schema.
postgres=# SET search_path TO tpcds, public;

-- Set the date style to the traditional POSTGRES style (date placed before month).
postgres=# SET datestyle TO postgres,dmy;
```

## Helpful Links<a name="en-us_topic_0237122186_en-us_topic_0059779029_sb71b84f08d92434d9974424733f4b326"></a>

[RESET](reset.md)  and  [SHOW](show.md)

