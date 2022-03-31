# Resetting Key Parameters During SQL Tuning<a name="EN-US_TOPIC_0289900358"></a>

This section introduces key parameters of the primary database node that affect optimization of SQL statements in openGauss. For details about the parameter configurations, see  [Configuring Running Parameters](configuring-running-parameters.md).

**Table  1**  Parameters of the primary database node

<a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_table6114302"></a>
<table><thead align="left"><tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row21522166"><th class="cellrowborder" valign="top" width="26.5%" id="mcps1.2.3.1.1"><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p65573909"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p65573909"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p65573909"></a>Parameter/Reference Value</p>
</th>
<th class="cellrowborder" valign="top" width="73.5%" id="mcps1.2.3.1.2"><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p9886408"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p9886408"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p9886408"></a>Description</p>
</th>
</tr>
</thead>
<tbody><tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row59628243"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p65158399"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p65158399"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p65158399"></a>enable_nestloop=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p43339000"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p43339000"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p43339000"></a>Specifies how the optimizer uses <strong id="b126812138114"><a name="b126812138114"></a><a name="b126812138114"></a>Nest Loop Join</strong>. If this parameter is set to <strong id="b422513212110"><a name="b422513212110"></a><a name="b422513212110"></a>on</strong>, the optimizer preferentially uses <strong id="b1923062117111"><a name="b1923062117111"></a><a name="b1923062117111"></a>Nest Loop Join</strong>. If it is set to <strong id="b132312021181112"><a name="b132312021181112"></a><a name="b132312021181112"></a>off</strong>, the optimizer preferentially uses other methods, if any.</p>
<div class="note" id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_note1238574948"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_note1238574948"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_note1238574948"></a><span class="notetitle"> NOTE: </span><div class="notebody"><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p19810311241"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p19810311241"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p19810311241"></a>If you only want to temporarily change the value of this parameter during the current database connection (that is, the current session), execute the following SQL statement:</p>
<a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_screen181041115417"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_screen181041115417"></a><pre class="screen" codetype="Sql" id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_screen181041115417">SET enable_nestloop to off;</pre>
</div></div>
<p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p33568521162216"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p33568521162216"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p33568521162216"></a>By default, this parameter is set to <strong id="b19986249181113"><a name="b19986249181113"></a><a name="b19986249181113"></a>on</strong>. Change the value as required. Generally, nested loop join has the poorest performance among the three <strong id="b42241357181113"><a name="b42241357181113"></a><a name="b42241357181113"></a>JOIN</strong> methods (nested loop join, merge join, and hash join). You are advised to set this parameter to <strong id="b62311579110"><a name="b62311579110"></a><a name="b62311579110"></a>off</strong>.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row24129853"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p8361080"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p8361080"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p8361080"></a>enable_bitmapscan=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p6158855"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p6158855"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p6158855"></a>Specifies whether the optimizer uses bitmap scanning. If the value is <strong id="b2091162112126"><a name="b2091162112126"></a><a name="b2091162112126"></a>on</strong>, bitmap scanning is used. If the value is <strong id="b498102116126"><a name="b498102116126"></a><a name="b498102116126"></a>off</strong>, it is not used.</p>
<div class="note" id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_note1657011214411"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_note1657011214411"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_note1657011214411"></a><span class="notetitle"> NOTE: </span><div class="notebody"><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p747814301147"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p747814301147"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p747814301147"></a>If you only want to temporarily change the value of this parameter during the current database connection (that is, the current session), execute the following SQL statement:</p>
<a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_screen124788309416"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_screen124788309416"></a><pre class="screen" codetype="Sql" id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_screen124788309416">SET enable_bitmapscan to off;</pre>
</div></div>
<p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p36534824162516"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p36534824162516"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p36534824162516"></a>The bitmap scanning applies only in the query condition where <strong id="b1729183412123"><a name="b1729183412123"></a><a name="b1729183412123"></a>a &gt; 1 and b &gt; 1</strong> and indexes are created on columns <strong id="b973783419122"><a name="b973783419122"></a><a name="b973783419122"></a>a</strong> and <strong id="b274043412123"><a name="b274043412123"></a><a name="b274043412123"></a>b</strong>. During performance tuning, if the query performance is poor and bitmapscan operators are in the execution plan, set this parameter to <strong id="b763414781315"><a name="b763414781315"></a><a name="b763414781315"></a>off</strong> and check whether the performance is improved.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row3177297143544"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p66890776143554"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p66890776143554"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p66890776143554"></a>enable_hashagg=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p34548229143544"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p34548229143544"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p34548229143544"></a>Specifies whether to enable the optimizer's use of Hash-aggregation plan types.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row21449639145156"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p4800916314528"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p4800916314528"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p4800916314528"></a>enable_hashjoin=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p3794196145156"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p3794196145156"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p3794196145156"></a>Specifies whether to enable the optimizer's use of Hash-join plan types.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row31678976115536"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p15860301115536"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p15860301115536"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p15860301115536"></a>enable_mergejoin=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p31236364115637"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p31236364115637"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p31236364115637"></a>Specifies whether to enable the optimizer's use of Hash-merge plan types.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row65339861145225"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p41108231145313"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p41108231145313"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p41108231145313"></a>enable_indexscan=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p52574139145225"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p52574139145225"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p52574139145225"></a>Specifies whether to enable the optimizer's use of index-scan plan types.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row25784757145225"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p4524365214542"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p4524365214542"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p4524365214542"></a>enable_indexonlyscan=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p6606196145225"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p6606196145225"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p6606196145225"></a>Specifies whether to enable the optimizer's use of index-only-scan plan types.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row50364799145216"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p18607282145410"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p18607282145410"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p18607282145410"></a>enable_seqscan=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p66511650145216"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p66511650145216"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p66511650145216"></a>Specifies whether the optimizer uses bitmap scanning. It is impossible to suppress sequential scans entirely, but setting this variable to <strong id="b1779952613149"><a name="b1779952613149"></a><a name="b1779952613149"></a>off</strong> encourages the optimizer to choose other methods if available.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_row36952817145219"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p5455969145417"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p5455969145417"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p5455969145417"></a>enable_sort=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p50220297145219"><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p50220297145219"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_en-us_topic_0073253807_en-us_topic_0062520027_p50220297145219"></a>Specifies the optimizer sorts. It is impossible to fully suppress explicit sorts, but setting this variable to <strong id="b204698497147"><a name="b204698497147"></a><a name="b204698497147"></a>off</strong> allows the optimizer to preferentially choose other methods if available.</p>
</td>
</tr>
<tr id="en-us_topic_0283136922_en-us_topic_0237121530_row91254119407"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_p5125511194014"><a name="en-us_topic_0283136922_en-us_topic_0237121530_p5125511194014"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_p5125511194014"></a>rewrite_rule</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136922_en-us_topic_0237121530_p3125411124017"><a name="en-us_topic_0283136922_en-us_topic_0237121530_p3125411124017"></a><a name="en-us_topic_0283136922_en-us_topic_0237121530_p3125411124017"></a>Specifies whether the optimizer enables the <strong id="b11177335152"><a name="b11177335152"></a><a name="b11177335152"></a>LAZY_AGG</strong> and <strong id="b1118763171517"><a name="b1118763171517"></a><a name="b1118763171517"></a>MAGIC_SET</strong> rewriting rules.</p>
</td>
</tr>
<tr id="row15768191461612"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="p076951417163"><a name="p076951417163"></a><a name="p076951417163"></a>sql_beta_feature</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="p1676941418160"><a name="p1676941418160"></a><a name="p1676941418160"></a>Specifies whether the optimizer enables the <strong id="b18358047185717"><a name="b18358047185717"></a><a name="b18358047185717"></a>SEL_SEMI_POISSON</strong>, <strong id="b071826205812"><a name="b071826205812"></a><a name="b071826205812"></a>SEL_EXPR_INSTR</strong>, <strong id="b0452102017588"><a name="b0452102017588"></a><a name="b0452102017588"></a>PARAM_PATH_GEN</strong>, <strong id="b1959817248583"><a name="b1959817248583"></a><a name="b1959817248583"></a>RAND_COST_OPT</strong>, <strong id="b1230282935818"><a name="b1230282935818"></a><a name="b1230282935818"></a>PARAM_PATH_OPT</strong>, <strong id="b46973619583"><a name="b46973619583"></a><a name="b46973619583"></a>PAGE_EST_OPT</strong>, <strong id="b315441113619"><a name="b315441113619"></a><a name="b315441113619"></a>CANONICAL_PATHKEY</strong>, and <strong id="b16147356163719"><a name="b16147356163719"></a><a name="b16147356163719"></a>PARTITION_OPFUSION</strong> beta features.</p>
</td>
</tr>
</tbody>
</table>
