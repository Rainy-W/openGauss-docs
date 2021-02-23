# Optimizer Method Configuration<a name="EN-US_TOPIC_0289900000"></a>

These configuration parameters provide a crude method of influencing the query plans chosen by the query optimizer. If the default plan chosen by the optimizer for a particular query is not optimal, a temporary solution is to use one of these configuration parameters to force the optimizer to choose a different plan. Better ways include adjusting the optimizer cost constants, manually running  **ANALYZE**, increasing the value of the  **default\_statistics\_target**  configuration parameter, and increasing the amount of the statistics collected in specific columns using  **ALTER TABLE SET STATISTICS**.

## enable\_bitmapscan<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s6ff0e1cd09c948469a5e8663cafc209f"></a>

**Parameter description**: Controls the query optimizer's use of bitmap-scan plan types.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of bitmap-scan plan types is enabled.
-   **off**  indicates that the query optimizer's use of bitmap-scan plan types is disabled.

**Default value**:  **on**

## force\_bitmapand<a name="en-us_topic_0283136675_en-us_topic_0237124716_section390014483481"></a>

**Parameter description**: Controls the query optimizer's use of BitmapAnd plan types.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of BitmapAnd plan types is enabled.
-   **off**  indicates that the query optimizer's use of BitmapAnd plan types is disabled.

**Default value**:  **off**

## enable\_hashagg<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s6589532cef104139a10a9b585c97c56b"></a>

**Parameter description**: Controls the query optimizer's use of Hash aggregation plan types.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of Hash aggregation plan types is enabled.
-   **off**  indicates that the query optimizer's use of Hash aggregation plan types is disabled.

**Default value**:  **on**

## enable\_hashjoin<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s566de83fd081416099e1453b10816d77"></a>

**Parameter description**: Controls the query optimizer's use of Hash-join plan types.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of Hash-join plan types is enabled.
-   **off**  indicates that the query optimizer's use of Hash-join plan types is disabled.

**Default value**:  **on**

## enable\_indexscan<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s6f45bb20aded4ed5814fb37ff3849afc"></a>

**Parameter description**: Controls the query optimizer's use of index-scan plan types.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of index-scan plan types is enabled.
-   **off**  indicates that the query optimizer's use of index-scan plan types is disabled.

**Default value**:  **on**

## enable\_indexonlyscan<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_se9bdf3f7db06400482c7c978e00fcc58"></a>

**Parameter description**: Controls the query optimizer's use of index-only-scan plan types.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of index-only-scan plan types is enabled.
-   **off**  indicates that the query optimizer's use of index-only-scan plan types is disabled.

**Default value**:  **on**

## enable\_material<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s9c4bdbba1ad645b497b7d5a2e4cbfd5a"></a>

**Parameter description**: Controls the query optimizer's use of materialization. It is impossible to suppress materialization entirely, but setting this variable to  **off**  prevents the optimizer from inserting materialized nodes.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of materialization is enabled.
-   **off**  indicates that the query optimizer's use of materialization is disabled.

**Default value**:  **on**

## enable\_mergejoin<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_sfc257a8da5f94bbfbe8396598e5fd0e4"></a>

**Parameter description**: Controls the query optimizer's use of merge-join plan types.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of merge-join plan types is enabled.
-   **off**  indicates that the query optimizer's use of merge-join plan types is disabled.

**Default value**:  **off**

## enable\_nestloop<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s5f30625b2fa94498b3b44df41c96970a"></a>

**Parameter description**: Controls the query optimizer's use of nested-loop join plan types to fully scan internal tables. It is impossible to suppress nested-loop joins entirely, but setting this variable to  **off**  encourages the optimizer to choose other methods if available.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of nested-loop join plan types is enabled.
-   **off**  indicates that the query optimizer's use of nested-loop join plan types is disabled.

**Default value**:  **off**

## enable\_index\_nestloop<a name="en-us_topic_0283136675_en-us_topic_0237124716_section1584803291014"></a>

**Parameter description**: Controls the query optimizer's use of the nested-loop join plan types to scan the parameterized indexes of internal tables.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of nested-loop join plan types is enabled.
-   **off**  indicates that the query optimizer's use of nested-loop join plan types is disabled.

**Default value**:  **on**

## enable\_seqscan<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_sd4833f4c14424278a6d0a81ae1195666"></a>

**Parameter description**: Controls the query optimizer's use of sequential scan plan types. It is impossible to suppress sequential scans entirely, but setting this variable to  **off**  encourages the optimizer to choose other methods if available.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of sequential scan plan types is enabled.
-   **off**  indicates that the query optimizer's use of sequential scan plan types is disabled.

**Default value**:  **on**

## enable\_sort<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_sb7f3e95793bc4b4d98518a77ffba4e4a"></a>

**Parameter description**: Controls the query optimizer's use of sort methods. It is impossible to suppress explicit sorts entirely, but setting this variable to  **off**  encourages the optimizer to choose other methods if available.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of sort methods is enabled.
-   **off**  indicates that the query optimizer's use of sort methods is disabled.

**Default value**:  **on**

## enable\_tidscan<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s87c617fc3c47455195a4815d45510482"></a>

**Parameter description**: Controls the query optimizer's use of Tuple ID \(TID\) scan plan types.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the query optimizer's use of TID scan plan types is enabled.
-   **off**  indicates that the query optimizer's use of TID scan plan types is disabled.

**Default value**:  **on**

## enable\_kill\_query<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s2deb52bc33e24b0d9e626eb6b79f80dc"></a>

**Parameter description**: In CASCADE mode, when a user is deleted, all the objects belonging to the user are deleted. This parameter specifies whether the queries of the objects belonging to the user can be unlocked when the user is deleted.

This parameter is a SUSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the unlocking is allowed.
-   **off**  indicates that the unlocking is not allowed.

**Default value**:  **off**

## enforce\_a\_behavior<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_sf2c1a90cdefd484ea8d0ac530476ade1"></a>

**Parameter description**: Controls the rule matching modes of regular expressions.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the O matching rule is used.
-   **off**  indicates that the POSIX matching rule is used.

**Default value**:  **on**

## max\_recursive\_times<a name="en-us_topic_0283136675_en-us_topic_0237124716_section333410396346"></a>

**Parameter description**: Specifies the maximum number of  **WITH RECURSIVE**  iterations.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: an integer ranging from 0 to  _INT\_MAX_

**Default value**:  **200**

## enable\_vector\_engine<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s0d040b72fd304d8ab8f063ffd98226a7"></a>

**Parameter description**: Controls the query optimizer's use of vectorized executor.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates the query optimizer's use of vectorized executor is enabled.
-   **off**  indicates the query optimizer's use of vectorized executor is disabled.

**Default value**:  **on**

## enable\_change\_hjcost<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_s2c3550150fa4494e82080e7c96d93732"></a>

**Parameter description**: Specifies whether the optimizer excludes internal table running costs when selecting the Hash Join cost path. If it is set to  **on**, tables with a few records and high running costs are more possible to be selected.

This parameter is a SUSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the internal table running costs will be excluded.
-   **off**  indicates that the internal table running costs will not be excluded.

**Default value**:  **off**

## enable\_absolute\_tablespace<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_section2170938217248"></a>

**Parameter description**: Controls whether the tablespace can use an absolute path.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that an absolute path can be used.
-   **off**  indicates that an absolute path cannot be used.

**Default value**:  **on**

## enable\_valuepartition\_pruning<a name="en-us_topic_0283136675_en-us_topic_0237124716_en-us_topic_0059778346_section25701680101350"></a>

**Parameter description**: Specifies whether the DFS partitioned table is dynamically or statically optimized.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that the DFS partitioned table is dynamically or statically optimized.
-   **off**  indicates that the DFS partitioned table is not dynamically or statically optimized.

**Default value**:  **on**

## expected\_computing\_nodegroup<a name="en-us_topic_0283136675_en-us_topic_0237124716_section746841514523"></a>

**Parameter description**: Specifies a computing Node Group or the way to choose such a group. The Node Group mechanism is now for internal use only. You do not need to set it.

During join or aggregation operations, a Node Group can be selected in four modes. In each mode, the specified candidate computing Node Groups are listed for the optimizer to select the most appropriate one for the current operator.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: a string

-   **optimal**: The list of candidate computing Node Groups consists of the Node Groups where the operator's operation objects are located and the Node Group that combines all the Node Groups on which the current user has the COMPUTE permission.
-   **query**: The list of candidate computing Node Groups consists of the Node Groups where the operator's operation objects are located and the Node Group that combines all the Node Groups where base tables involved in the query are located.
-   _Node group name_  \(when  **[enable\_nodegroup\_debug](#en-us_topic_0283136675_en-us_topic_0237124716_section1426622145210)**  is set to  **off**\): The list of candidate computing Node Groups consists of the Node Group where the operator's operation objects are located and the specified Node Group.
-   _Node Group name_  \(when  **[enable\_nodegroup\_debug](#en-us_topic_0283136675_en-us_topic_0237124716_section1426622145210)**  is set to  **on**\): A specific Node Group is used as the computing Node Group.

**Default value**:  **query**

## enable\_nodegroup\_debug<a name="en-us_topic_0283136675_en-us_topic_0237124716_section1426622145210"></a>

**Parameter description**: Specifies whether the optimizer assigns computing workloads to a specific Node Group when multiple Node Groups exist in an environment. The Node Group mechanism is now for internal use only. You do not need to set it.

This parameter takes effect only when  **[expected\_computing\_nodegroup](#en-us_topic_0283136675_en-us_topic_0237124716_section746841514523)**  is set to a specific Node Group.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: Boolean

-   **on**  indicates that computing workloads are assigned to the Node Group specified by  **expected\_computing\_nodegroup**.
-   **off**  indicates no Node Group is specified to compute.

**Default value**:  **off**

## qrw\_inlist2join\_optmode<a name="en-us_topic_0283136675_en-us_topic_0237124716_section207996212178"></a>

**Parameter description**: Specifies whether to enable inlist-to-join \(inlist2join\) query rewriting.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: a string

-   **disable**  indicates that the inlist2join query rewriting is disabled.
-   **cost\_base**  indicates that the cost-based inlist2join query rewriting is enabled.
-   **rule\_base**  indicates that the forcible rule-based inlist2join query rewriting is enabled.
-   A positive integer indicates the threshold of inlist2join query rewriting. If the number of elements in the list is greater than the threshold, the rewriting is performed.

**Default value**:  **cost\_base**

## skew\_option<a name="en-us_topic_0283136675_en-us_topic_0237124716_section1211182712176"></a>

**Parameter description**: Specifies whether an optimization policy is used.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: a string

-   **off**  indicates that the policy is disabled.
-   **normal**  indicates that a radical policy is used. All possible skews are optimized.
-   **lazy**  indicates that a conservative policy is used. Uncertain skews are ignored.

**Default value**:  **normal**

## default\_limit\_rows<a name="section5328711171611"></a>

**Parameter description**: Specifies the default estimated number of limit rows for generating genericplan. If this parameter is set to a positive value, the positive value is used as the estimated number of limit rows. If this parameter is set to a negative value, the negative value is converted to a percentage and used as default estimated value, that is, -5 indicates 5%.

This parameter is a USERSET parameter. Set it based on instructions provided in  [Table 1](en-us_topic_0283137176.md#en-us_topic_0237121562_en-us_topic_0059777490_t91a6f212010f4503b24d7943aed6d846).

**Value range**: a floating point number ranging from –100 to DBL\_MAX

**Default value**:  **–10**

