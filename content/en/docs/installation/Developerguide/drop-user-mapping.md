# DROP USER MAPPING<a name="EN-US_TOPIC_0272283424"></a>

## Function<a name="section152751851406"></a>

**DROP USER MAPPING**  drops a user mapping for a foreign server.

## Syntax<a name="section4460205915011"></a>

```
DROP USER MAPPING [ IF EXISTS ] FOR { user_name | USER | CURRENT_USER | PUBLIC } SERVER server_name;
```

## Parameter Description<a name="section115661681112"></a>

-   **IF EXISTS**

    Reports a notice instead of an error if the user mapping does not exist.

-   **user\_name**

    Specifies user name of the mapping.

    CURRENT\_USER and USER match the name of the current user. PUBLIC is used to match all current and future user names in the system.

-   **server\_name**

    Specifies name of the server to which the user is mapped.


## Helpful Links<a name="section17590015119"></a>

[ALTER USER MAPPING](alter-user-mapping.md)  and  [CREATE USER MAPPING](create-user-mapping.md)

