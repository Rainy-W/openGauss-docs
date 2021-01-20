# System Architecture<a name="EN-US_TOPIC_0241663016"></a>

openGauss is a standalone database where data is stored on a single physical node and data access tasks are pushed to service nodes. In this way, high concurrency of servers enables quick data processing. In addition, data can be copied to the standby server through log replication, ensuring high reliability and scalability.

## Software Architecture<a name="en-us_topic_0237080634_en-us_topic_0231764167_section1940043819751"></a>

openGauss is a standalone database and can be deployed in primary/standby mode.

openGauss shows the logical components of  [Figure 1](#en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_fig5205420191411).

**Figure  1**  openGauss logical components<a name="en-us_topic_0237080634_en-us_topic_0231764167_fig5205420191411"></a>  
![](figures/opengauss-logical-components.png "opengauss-logical-components")

**Table  1**  Architecture description

<a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_table5479978919151"></a>

<table><thead align="left"><tr id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_row4411284819151"><th class="cellrowborder" valign="top" width="14.469999999999999%" id="mcps1.2.3.1.1"><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p404366191511"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p404366191511"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p404366191511"></a>Name</p>
</th>
<th class="cellrowborder" valign="top" width="85.53%" id="mcps1.2.3.1.2"><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p7387596191511"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p7387596191511"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p7387596191511"></a>Description</p>
</th>
</tr>
</thead>
<tbody><tr id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_row3200216592122"><td class="cellrowborder" valign="top" width="14.469999999999999%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p1877290192147"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p1877290192147"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p1877290192147"></a>OM</p>
</td>
<td class="cellrowborder" valign="top" width="85.53%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p4420997892147"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p4420997892147"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p4420997892147"></a>Operation Manager (OM) It provides management interfaces and tools for routine maintenance and configuration management of the database.</p>
</td>
</tr>
<tr id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_row6476976919151"><td class="cellrowborder" valign="top" width="14.469999999999999%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p11262944162914"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p11262944162914"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p11262944162914"></a>Client driver</p>
</td>
<td class="cellrowborder" valign="top" width="85.53%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p23234897162914"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p23234897162914"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p23234897162914"></a>Client driver receives access requests from the application layer and returns execution results. It communicates with <span id="text1113502285312"><a name="text1113502285312"></a><a name="text1113502285312"></a>openGauss</span> instances, sends application SQL commands, and receives <span id="text51351822125311"><a name="text51351822125311"></a><a name="text51351822125311"></a>openGauss</span> execution results.</p>
</td>
</tr>
<tr id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_row5813821019151"><td class="cellrowborder" valign="top" width="14.469999999999999%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p29314576162914"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p29314576162914"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p29314576162914"></a><span id="text6736142565318"><a name="text6736142565318"></a><a name="text6736142565318"></a>openGauss</span> (primary/standby)</p>
</td>
<td class="cellrowborder" valign="top" width="85.53%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p1933624014508"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p1933624014508"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p1933624014508"></a><span id="text12102162717535"><a name="text12102162717535"></a><a name="text12102162717535"></a>openGauss</span> primary/standby DN stores service data, executes data query tasks, and returns execution results.</p>
<p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p56577630162914"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p56577630162914"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p56577630162914"></a><span id="text4319172855317"><a name="text4319172855317"></a><a name="text4319172855317"></a>openGauss</span> supports one primary and multiple standbys. You are advised to deploy them on different physical nodes.</p>
</td>
</tr>
<tr id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_row4354812919183"><td class="cellrowborder" valign="top" width="14.469999999999999%" headers="mcps1.2.3.1.1 "><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p553181019183"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p553181019183"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p553181019183"></a>Storage</p>
</td>
<td class="cellrowborder" valign="top" width="85.53%" headers="mcps1.2.3.1.2 "><p id="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p64149272191943"><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p64149272191943"></a><a name="en-us_topic_0283136530_en-us_topic_0237080634_en-us_topic_0231764167_p64149272191943"></a>Functions as the server's local storage resources to store data permanently.</p>
</td>
</tr>
</tbody>
</table>

