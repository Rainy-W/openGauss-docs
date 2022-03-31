# Troubleshooting<a name="EN-US_TOPIC_0289900701"></a>

-   Failure of connection to the database instance: Check whether the database instance is faulty or the security permissions of configuration items in the  **pg\_hba.conf**  file are incorrectly configured.
-   Restart failure: Check the health status of the database instance and ensure that the database instance is running properly.
-   Poor performance of TPC-C jobs: In high-concurrency scenarios such as TPC-C, a large amount of data is modified during pressure tests. Each test is not idempotent, for example, the data volume in the TPC-C database increases, invalid tuples are not cleared using VACUUM FULL, checkpoints are not triggered in the database, and drop cache is not performed. Therefore, it is recommended that the benchmark data that is written with a large amount of data, such as TPC-C, be imported again at intervals \(depending on the number of concurrent tasks and execution duration\). A simple method is to back up the $PGDATA directory.
-   When the TPC-C job is running, the TPC-C driver script reports the error "TypeError: float\(\) argument must be a string or a number, not 'NoneType'" \(**none **cannot be converted to the float type\). This is because the TPC-C pressure test result is not obtained. There are many causes for this problem, manually check whether TPC-C can be successfully executed and whether the returned result can be obtained. If the preceding problem does not occur, you are advised to set the delay time of the  **sleep **command in the command list in the TPC-C driver script to a larger value.
