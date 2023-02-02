# Data Ingestion Speed<a name="EN-US_TOPIC_0260488109"></a>

This test simulates realtime data streams arriving from massive IoT, cloud or mobile devices that need to be quickly ingested into the database on a massive scale.

-   The test involved
    -   10 million rows were sent by 500 threads, 2000 rounds, 10 records \(rows\) in each insert command, each record was 200 bytes.
    -   The client and database were on different machines.  Database server – x86 2-socket, 72 cores.

-   Performance Results
    -   **Throughput – 10,000 **Records/Core or  **2**  MB/Core.
    -   **Latency – 2.8ms per a 10 records**  bulk insert \(includes client-server networking\)


>![](public_sys-resources/icon-note.gif) **NOTE:**   
>We are projecting that multiple additional, and even significant, performance improvements will be made by MOT for this scenario.  

