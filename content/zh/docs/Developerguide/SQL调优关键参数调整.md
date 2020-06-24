# SQL调优关键参数调整<a name="ZH-CN_TOPIC_0245374565"></a>

本节将介绍影响openGauss SQL调优性能的关键数据库主节点配置参数，配置方法参见[配置运行参数](配置运行参数.md)。

**表 1**  数据库主节点配置参数

<a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_table6114302"></a>
<table><thead align="left"><tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row21522166"><th class="cellrowborder" valign="top" width="26.5%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p65573909"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p65573909"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p65573909"></a>参数/参考值</p>
</th>
<th class="cellrowborder" valign="top" width="73.5%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p9886408"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p9886408"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p9886408"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row59628243"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p65158399"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p65158399"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p65158399"></a>enable_nestloop=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p43339000"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p43339000"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p43339000"></a>控制查询优化器对嵌套循环连接（Nest Loop Join）类型的使用。当设置为“on”后，优化器优先使用Nest Loop Join；当设置为“off”后，优化器在存在其他方法时将优先选择其他方法。</p>
<div class="note" id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_note1238574948"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_note1238574948"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_note1238574948"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p19810311241"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p19810311241"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p19810311241"></a>如果只需要在当前数据库连接（即当前Session）中临时更改该参数值，则只需要在SQL语句中执行如下命令：</p>
<a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_screen181041115417"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_screen181041115417"></a><pre class="screen" codetype="Sql" id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_screen181041115417">SET enable_nestloop to off;</pre>
</div></div>
<p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p33568521162216"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p33568521162216"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p33568521162216"></a>此参数默认设置为“on”，但实际调优中应根据情况选择是否关闭。一般情况下，在三种join方式（Nested Loop、Merge Join和Hash Join）里，Nested Loop性能较差，实际调优中可以选择关闭。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row24129853"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p8361080"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p8361080"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p8361080"></a>enable_bitmapscan=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p6158855"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p6158855"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p6158855"></a>控制查询优化器对位图扫描规划类型的使用。设置为“on”，表示使用；设置为“off”，表示不使用。</p>
<div class="note" id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_note1657011214411"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_note1657011214411"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_note1657011214411"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p747814301147"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p747814301147"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p747814301147"></a>如果只需要在当前数据库连接（即当前Session）中临时更改该参数值，则只需要在SQL语句中执行命令如下命令：</p>
<a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_screen124788309416"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_screen124788309416"></a><pre class="screen" codetype="Sql" id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_screen124788309416">SET enable_bitmapscan to off;</pre>
</div></div>
<p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p36534824162516"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p36534824162516"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p36534824162516"></a>bitmapscan扫描方式适用于“where a &gt; 1 and b &gt; 1”且a列和b列都有索引这种查询条件，但有时其性能不如indexscan。因此，现场调优如发现查询性能较差且计划中有bitmapscan算子，可以关闭bitmapscan，看性能是否有提升。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row3177297143544"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p66890776143554"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p66890776143554"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p66890776143554"></a>enable_hashagg=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p34548229143544"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p34548229143544"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p34548229143544"></a>控制优化器对Hash聚集规划类型的使用。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row21449639145156"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p4800916314528"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p4800916314528"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p4800916314528"></a>enable_hashjoin=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p3794196145156"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p3794196145156"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p3794196145156"></a>控制优化器对Hash连接规划类型的使用。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row31678976115536"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p15860301115536"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p15860301115536"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p15860301115536"></a>enable_mergejoin=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p31236364115637"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p31236364115637"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p31236364115637"></a>控制优化器对融合连接规划类型的使用。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row65339861145225"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p41108231145313"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p41108231145313"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p41108231145313"></a>enable_indexscan=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p52574139145225"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p52574139145225"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p52574139145225"></a>控制优化器对索引扫描规划类型的使用。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row25784757145225"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p4524365214542"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p4524365214542"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p4524365214542"></a>enable_indexonlyscan=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p6606196145225"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p6606196145225"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p6606196145225"></a>控制优化器对仅索引扫描规划类型的使用。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row50364799145216"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p18607282145410"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p18607282145410"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p18607282145410"></a>enable_seqscan=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p66511650145216"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p66511650145216"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p66511650145216"></a>控制优化器对顺序扫描规划类型的使用。完全消除顺序扫描是不可能的，但是关闭这个变量会让优化器在存在其他方法的时候优先选择其他方法。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_row36952817145219"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p5455969145417"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p5455969145417"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p5455969145417"></a>enable_sort=on</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p50220297145219"><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p50220297145219"></a><a name="zh-cn_topic_0237121530_zh-cn_topic_0073253807_zh-cn_topic_0062520027_p50220297145219"></a>控制优化器使用的排序步骤。该设置不可能完全消除明确的排序，但是关闭这个变量可以让优化器在存在其他方法的时候优先选择其他方法。</p>
</td>
</tr>
<tr id="zh-cn_topic_0237121530_row91254119407"><td class="cellrowborder" valign="top" width="26.5%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0237121530_p5125511194014"><a name="zh-cn_topic_0237121530_p5125511194014"></a><a name="zh-cn_topic_0237121530_p5125511194014"></a>rewrite_rule</p>
</td>
<td class="cellrowborder" valign="top" width="73.5%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0237121530_p3125411124017"><a name="zh-cn_topic_0237121530_p3125411124017"></a><a name="zh-cn_topic_0237121530_p3125411124017"></a>控制优化器是否启用LAZY_AGG和MAGIC_SET重写规则。</p>
</td>
</tr>
</tbody>
</table>

