# Query<a name="EN-US_TOPIC_0289900490"></a>

## instr\_unique\_sql\_count<a name="en-us_topic_0283137149_en-us_topic_0237124756_section983311682019"></a>

**Parameter description**: Specifies the maximum number of Unique SQL records to be collected. The value  **0**  indicates that the function of collecting Unique SQL information is disabled.

If the value is changed from a larger one to a smaller one, Unique SQL statistics will be reset and re-collected. There is no impact if the value is changed from a smaller one to a larger one.

When the number of Unique SQL records generated in the system is greater than the value of  **instr\_unique\_sql\_count**, the extra Unique SQL records are not collected.

This parameter is a SIGHUP parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: an integer ranging from 0 to  _INT\_MAX_

**Default value**:  **100**

## instr\_unique\_sql\_track\_type<a name="en-us_topic_0283137149_en-us_topic_0237124756_section88591117185212"></a>

**Parameter description**: Specifies which SQL statements are recorded in Unique SQL.

This parameter is an INTERNAL parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: enumerated values

-   **top**: Only top-level SQL statements are recorded.

**Default value**:  **top**

## enable\_instr\_rt\_percentile<a name="en-us_topic_0283137149_en-us_topic_0237124756_section137313294592"></a>

**Parameter description**: Specifies whether to enable the function of calculating the response time of 80% and 95% SQL statements in the system.

This parameter is a SIGHUP parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the function of calculating the response time of 80% and 95% SQL statements is enabled.
-   **off**  indicates that the function of calculating the response time of 80% and 95% SQL statements is disabled.

**Default value**:  **on**

## percentile<a name="en-us_topic_0283137149_en-us_topic_0237124756_section193531235231"></a>

**Parameter description**: Specifies the percentage of SQL statements whose response time is to be calculated by the background calculation thread.

This parameter is an INTERNAL parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: a string

**Default value**:  **80,95**

## instr\_rt\_percentile\_interval<a name="en-us_topic_0283137149_en-us_topic_0237124756_section1658494717518"></a>

**Parameter description**: Specifies the interval at which the background calculation thread calculates the SQL response time.

This parameter is a SIGHUP parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: an integer ranging from 0 to 3600. The unit is s.

**Default value**:  **10s**

## enable\_instr\_cpu\_timer<a name="en-us_topic_0283137149_en-us_topic_0237124756_section1261620172577"></a>

**Parameter description**: Specifies whether to capture the CPU time consumed during SQL statement execution.

This parameter is a SIGHUP parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates the CPU time consumed during SQL statement execution is captured.
-   **off**  indicates the CPU time consumed during SQL statement execution is not captured.

**Default value**:  **on**

## enable\_stmt\_track<a name="section148515311729"></a>

**Parameter description**: Specifies whether to enable the full/slow SQL statement feature.

This parameter is a SIGHUP parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0289899927.md#en-us_topic_0283137176_en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   on: Full/Slow SQL capture is enabled.
-   off: Full /Slow SQL capture is disabled.

**Default value**:  **on**

## track\_stmt\_session\_slot<a name="section1768054315510"></a>

**Parameter description**: Specifies the maximum number of full/slow SQL statements that can be cached in a session. If the number of full/slow SQL statements exceeds this value, new statements will not be traced until the flush thread flushes the cached statements to the disk to reserve idle space.

This parameter is a SIGHUP parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0289899927.md#en-us_topic_0283137176_en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: an integer ranging from 0 to 2147483647

**Default value**:  **1000**

## track\_stmt\_details\_size<a name="section584919463"></a>

**Parameter description**: Specifies the maximum size \(in bytes\) of execution events that can be collected by a single statement.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0289899927.md#en-us_topic_0283137176_en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: an integer ranging from 0 to 100000000

**Default value**:  **4096**

## track\_stmt\_retention\_time<a name="section16119247614"></a>

**Parameter description**: Specifies the retention period of full/slow SQL statement records. This parameter is a combination of parameters. This parameter is read every 60 seconds and records exceeding the retention period are deleted.

This parameter is a SIGHUP parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0289899927.md#en-us_topic_0283137176_en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: a string

This parameter consists of two parts in the format of 'full sql retention time, slow sql retention time'.

**full sql retention time**  indicates the retention time of full SQL statements. The value ranges from 0 to 86400.

**slow sql retention time**  indicates the retention time of slow SQL statements. The value ranges from 0 to 604800.

**Default value**:  **3600,604800**

## track\_stmt\_stat\_level<a name="section194516368610"></a>

**Parameter description**: Controls the level of statement execution tracing.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0289899927.md#en-us_topic_0283137176_en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846). The value is case-insensitive.

**Value range**: a string

This parameter consists of two parts in the format of 'full sql stat level, slow sql stat level'.

The first part indicates the tracing level of full SQL statements. The value can be  **OFF**,  **L0**,  **L1**, or  **L2**.

The second part indicates the tracing level of slow SQL statements. The value can be  **OFF**,  **L0**,  **L1**, or  **L2**.

**Default value**:  **OFF,L0**

