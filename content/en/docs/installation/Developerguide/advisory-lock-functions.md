# Advisory Lock Functions<a name="EN-US_TOPIC_0242370459"></a>

Advisory lock functions manage advisory locks.

-   pg\_advisory\_lock\(key bigint\)

    Description: Obtains an exclusive session-level advisory lock.

    Return type: void

    Note:  **pg\_advisory\_lock**  locks resources defined by an application. The resources can be identified using a 64-bit or two nonoverlapped 32-bit key values. If another session locks the resources, the function blocks the resources until they can be used. The lock is exclusive. Multiple locking requests are pushed into the stack. Therefore, if the same resource is locked three times, it must be unlocked three times so that it is released to another session.

-   pg\_advisory\_lock\(key1 int, key2 int\)

    Description: Obtains an exclusive session-level advisory lock.

    Return type: void

    Note: Only users with the  **sysadmin**  permission can add session-level exclusive advisory locks to the key-value pair \(65535, 65535\).

-   pg\_advisory\_lock\_shared\(key bigint\)

    Description: Obtains a shared session-level advisory lock.

    Return type: void

-   pg\_advisory\_lock\_shared\(key1 int, key2 int\)

    Description: Obtains a shared session-level advisory lock.

    Return type: void

    Note:  **pg\_advisory\_lock\_shared**  works in the same way as  **pg\_advisory\_lock**, except the lock can be shared with other sessions requesting shared locks. Only would-be exclusive lockers are locked out.

-   pg\_advisory\_unlock\(key bigint\)

    Description: Releases an exclusive session-level advisory lock.

    Return type: Boolean

-   pg\_advisory\_unlock\(key1 int, key2 int\)

    Description: Releases an exclusive session-level advisory lock.

    Return type: Boolean

    Note:  **pg\_advisory\_unlock**  releases the obtained exclusive advisory lock. If the release is successful, the function returns  **true**. If the lock was not held, it will return  **false**. In addition, a SQL warning will be reported by the server.

-   pg\_advisory\_unlock\_shared\(key bigint\)

    Description: Releases a shared session-level advisory lock.

    Return type: Boolean

-   pg\_advisory\_unlock\_shared\(key1 int, key2 int\)

    Description: Releases a shared session-level advisory lock.

    Return type: Boolean

    Note:  **pg\_advisory\_unlock\_shared**  works in the same way as  **pg\_advisory\_unlock**, except it releases a shared session-level advisory lock.

-   pg\_advisory\_unlock\_all\(\)

    Description: Releases all advisory locks owned by the current session.

    Return type: void

    Note:  **pg\_advisory\_unlock\_all**  releases all advisory locks owned by the current session. The function is implicitly invoked when the session ends even if the client is abnormally disconnected.

-   pg\_advisory\_xact\_lock\(key bigint\)

    Description: Obtains an exclusive transaction-level advisory lock.

    Return type: void

-   pg\_advisory\_xact\_lock\(key1 int, key2 int\)

    Description: Obtains an exclusive transaction-level advisory lock.

    Return type: void

    Note:  **pg\_advisory\_xact\_lock**  works in the same way as  **pg\_advisory\_lock**, except the lock is automatically released at the end of the current transaction and cannot be released explicitly. Only users with the  **sysadmin**  permission can add transaction-level exclusive advisory locks to the key-value pair \(65535, 65535\).

-   pg\_advisory\_xact\_lock\_shared\(key bigint\)

    Description: Obtains a shared transaction-level advisory lock.

    Return type: void

-   pg\_advisory\_xact\_lock\_shared\(key1 int, key2 int\)

    Description: Obtains a shared transaction-level advisory lock.

    Return type: void

    Note:  **pg\_advisory\_xact\_lock\_shared**  works in the same way as  **pg\_advisory\_lock\_shared**, except the lock is automatically released at the end of the current transaction and cannot be released explicitly.

-   pg\_try\_advisory\_lock\(key bigint\)

    Description: Obtains an exclusive session-level advisory lock if available.

    Return type: Boolean

    Note:  **pg\_try\_advisory\_lock**  is similar to  **pg\_advisory\_lock**, except  **pg\_try\_advisory\_lock**  does not block the resource until the resource is released.  **pg\_try\_advisory\_lock**  either immediately obtains the lock and returns  **true**  or returns  **false**, which indicates the lock cannot be performed currently.

-   pg\_try\_advisory\_lock\(key1 int, key2 int\)

    Description: Obtains an exclusive session-level advisory lock if available.

    Return type: Boolean

    Note: Only users with the  **sysadmin**  permission can add session-level exclusive advisory locks to the key-value pair \(65535, 65535\).

-   pg\_try\_advisory\_lock\_shared\(key bigint\)

    Description: Obtains a shared session-level advisory lock if available.

    Return type: Boolean

-   pg\_try\_advisory\_lock\_shared\(key1 int, key2 int\)

    Description: Obtains a shared session-level advisory lock if available.

    Return type: Boolean

    Note:  **pg\_try\_advisory\_lock\_shared**  is similar to  **pg\_try\_advisory\_lock**, except  **pg\_try\_advisory\_lock\_shared**  attempts to obtain a shared lock instead of an exclusive lock.

-   pg\_try\_advisory\_xact\_lock\(key bigint\)

    Description: Obtains an exclusive transaction-level advisory lock if available.

    Return type: Boolean

-   pg\_try\_advisory\_xact\_lock\(key1 int, key2 int\)

    Description: Obtains an exclusive transaction-level advisory lock if available.

    Return type: Boolean

    Note:  **pg\_try\_advisory\_xact\_lock**  works in the same way as  **pg\_try\_advisory\_lock**, except the lock, if acquired, is automatically released at the end of the current transaction and cannot be released explicitly. Note: Only users with the  **sysadmin**  permission can add transaction-level exclusive advisory locks to the key-value pair \(65535, 65535\).

-   pg\_try\_advisory\_xact\_lock\_shared\(key bigint\)

    Description: Obtains a shared transaction-level advisory lock if available.

    Return type: Boolean

-   pg\_try\_advisory\_xact\_lock\_shared\(key1 int, key2 int\)

    Description: Obtains a shared transaction-level advisory lock if available.

    Return type: Boolean

    Note:  **pg\_try\_advisory\_xact\_lock\_shared**  works in the same way as  **pg\_try\_advisory\_lock\_shared**, except the lock, if acquired, is automatically released at the end of the current transaction and cannot be released explicitly.

-   lock\_cluster\_ddl\(\)

    Description: Attempts to obtain a session-level exclusive advisory lock for all active primary database nodes in openGauss.

    Return type: Boolean

    Note: Only users with the  **sysadmin**  permission can call this function.

-   unlock\_cluster\_ddl\(\)

    Description: Attempts to add a session-level exclusive advisory lock on the primary database node.

    Return type: Boolean


