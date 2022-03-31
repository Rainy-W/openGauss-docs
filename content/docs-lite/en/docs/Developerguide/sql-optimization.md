# SQL Optimization<a name="EN-US_TOPIC_0289900921"></a>

The aim of SQL optimization is to maximize the utilization of resources, including CPU, memory, and disk I/O. All optimization methods are intended for resource utilization. To maximize resource utilization is to run SQL statements as efficiently as possible to achieve the highest performance at a lower cost. For example, when performing a typical point query, you can use a Seq Scan and a filter \(that is, read every tuple and point query conditions for match\). You can also use an Index Scan, which can be implemented at a lower cost but achieve the same effect.

You can determine a proper openGauss deployment solution and table definition based on hardware resources and service characteristics. This is the basis of meeting performance requirements. The following performance tuning sections assume that you have finished installation based on a proper openGauss solution in the software installation guide and performed database design based on the guide for database design and development.

-   **[Query Execution Process](query-execution-process.md)**  

-   **[Introduction to the SQL Execution Plan](introduction-to-the-sql-execution-plan.md)**  

-   **[Tuning Process](tuning-process.md)**  

-   **[Updating Statistics](updating-statistics.md)**  

-   **[Reviewing and Modifying a Table Definition](reviewing-and-modifying-a-table-definition.md)**  

-   **[Typical SQL Optimization Methods](typical-sql-optimization-methods.md)**  

-   **[Experience in Rewriting SQL Statements](experience-in-rewriting-sql-statements.md)**  

-   **[Resetting Key Parameters During SQL Tuning](resetting-key-parameters-during-sql-tuning.md)**  

-   **[Hint-based Tuning](hint-based-tuning.md)**  

-   **[Using the Vectorized Executor for Tuning](using-the-vectorized-executor-for-tuning.md)**  


