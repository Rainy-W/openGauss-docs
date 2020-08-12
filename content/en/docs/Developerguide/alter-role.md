# ALTER ROLE<a name="EN-US_TOPIC_0242370532"></a>

## Function<a name="en-us_topic_0237122068_en-us_topic_0059778744_sa4ec5e4feca4419193486c30e3c50708"></a>

**ALTER ROLE**  modifies role attributes.

## Precautions<a name="en-us_topic_0237122068_en-us_topic_0059778744_sa559bf9874634b91a97ecb349a5b4c5b"></a>

None

## Syntax<a name="en-us_topic_0237122068_en-us_topic_0059778744_sad868fc15480446b8c29a37a152b5fc5"></a>

-   Modify the permissions of a role.

    ```
    ALTER ROLE role_name [ [ WITH ] option [ ... ] ];
    ```

    The  **option**  clause for granting permissions is as follows:

    ```
    {CREATEDB | NOCREATEDB}
        | {CREATEROLE | NOCREATEROLE}
        | {INHERIT | NOINHERIT}
        | {AUDITADMIN | NOAUDITADMIN}
        | {SYSADMIN | NOSYSADMIN}
        | {USEFT | NOUSEFT}
        | {LOGIN | NOLOGIN}
        | {REPLICATION | NOREPLICATION}
        | {INDEPENDENT | NOINDEPENDENT}
        | {VCADMIN | NOVCADMIN}
        | CONNECTION LIMIT connlimit
        | [ ENCRYPTED | UNENCRYPTED ] PASSWORD 'password'
        | [ ENCRYPTED | UNENCRYPTED ] IDENTIFIED BY 'password' [ REPLACE 'old_password' ]
        | [ ENCRYPTED | UNENCRYPTED ] PASSWORD { 'password' | DISABLE }
        | [ ENCRYPTED | UNENCRYPTED ] IDENTIFIED BY { 'password' [ REPLACE 'old_password' ] | DISABLE }
        | VALID BEGIN 'timestamp'
        | VALID UNTIL 'timestamp'
        | RESOURCE POOL 'respool'
        | PERM SPACE 'spacelimit'
        | ACCOUNT { LOCK | UNLOCK }
        | PGUSER
    ```
    
-   Rename a role.

    ```
    ALTER ROLE role_name 
        RENAME TO new_name;
    ```

-   Set parameters for a role.

    ```
    ALTER ROLE role_name [ IN DATABASE database_name ]
        SET configuration_parameter {{ TO | = } { value | DEFAULT } | FROM CURRENT};
    ```

-   Reset parameters for a role.

    ```
    ALTER ROLE role_name
        [ IN DATABASE database_name ] RESET {configuration_parameter|ALL};
    ```


## Parameter Description<a name="en-us_topic_0237122068_en-us_topic_0059778744_s50961af6143d4aafaf8fa02febbbf331"></a>

-   **role\_name**

    Specifies a role name.

    Value range: an existing username

-   **IN DATABASE database\_name**

    Modifies the parameters of a role in a specified database.

-   **SET configuration\_parameter**

    Sets parameters for a role. Session parameters modified by  **ALTER ROLE**  apply to a specified role and take effect in the next session triggered by the role.

    Value range:

    For details about the values of  **configuration\_parameter**  and  **value**, see  [SET](set.md).

    **DEFAULT**: clears the value of  **configuration\_parameter**.  **configuration\_parameter**  will inherit the default value of the new session generated for the role.

    **FROM CURRENT**: uses the value of  **configuration\_parameter**  of the current session.

-   **RESET configuration\_parameter/ALL**

    Clears the value of  **configuration\_parameter**. The statement has the same effect as that of  **SET configuration\_parameter TO DEFAULT**.

    Value range:  **ALL**  indicates that the values of all parameters are cleared.

-   **ACCOUNT LOCK | ACCOUNT UNLOCK**
    -   **ACCOUNT LOCK**: locks an account to forbid login to databases.
    -   **ACCOUNT UNLOCK**: unlocks an account to allow login to databases.

-   **PGUSER**

    In the current version, the  **PGUSER**  attribute of a role cannot be modified.


For details about other parameters, see  [Parameter Description](create-role.md#en-us_topic_0237122112_en-us_topic_0059778189_s5a43ec5742a742089e2c302063de7fe4)  in  **CREATE ROLE**.

## Example<a name="en-us_topic_0237122068_en-us_topic_0059778744_s961f01774f174a5aa4e6f59dea50381a"></a>

See  [Example:](create-role.md#en-us_topic_0237122112_en-us_topic_0059778189_s0dea2f90b8474387aff0ab3f366a611e)  in  **CREATE ROLE**.

## Helpful Links<a name="en-us_topic_0237122068_en-us_topic_0059778744_sb24012e0cec94bc3ba5c2c0e8997d052"></a>

[CREATE ROLE](create-role.md),  [DROP ROLE](drop-role.md), and  [SET](set.md)

