# Materialized View<a name="EN-US_TOPIC_0295970202"></a>

A materialized view is a special physical table, which is relative to a common view. A common view is a virtual table and has many application limitations. Any query on a view is actually converted into a query on an SQL statement, and performance is not actually improved. The materialized view actually stores the results of the statements executed by the SQL statement, and is used to cache the results.

-   **[Complete-refresh Materialized View](full-materialized-view.md)**  

-   **[Fast-refresh Materialized View](incremental-materialized-view.md)**  


