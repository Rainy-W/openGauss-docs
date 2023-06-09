# DBE\_PLDEVELOPER.gs\_errors<a name="EN-US_TOPIC_0000001214726465"></a>

Records errors that occur during PLPGSQL object \(stored procedure, function, package, and package body\) compilation. For details, see the following column description.

After the  **plsql\_show\_all\_error**  parameter is enabled, if an error occurs during compilation, the error is skipped and the compilation continues, and the error information is recorded in  **gs\_errors**. If the  **plsql\_show\_all\_error**  parameter is disabled, related information is not inserted into this table.

**Table  1**  DBE\_PLDEVELOPER.gs\_errors columns

<a name="table1011513101687"></a>
<table><tbody><tr id="row201685101086"><td class="cellrowborder" valign="top" width="17.67176717671767%"><p id="p7168210483"><a name="p7168210483"></a><a name="p7168210483"></a><strong id="b3706105854218"><a name="b3706105854218"></a><a name="b3706105854218"></a>Name</strong></p>
</td>
<td class="cellrowborder" valign="top" width="22.562256225622562%"><p id="p1816817101585"><a name="p1816817101585"></a><a name="p1816817101585"></a><strong id="b106103598421"><a name="b106103598421"></a><a name="b106103598421"></a>Type</strong></p>
</td>
<td class="cellrowborder" valign="top" width="59.765976597659765%"><p id="p111687101286"><a name="p111687101286"></a><a name="p111687101286"></a><strong id="b18171102434"><a name="b18171102434"></a><a name="b18171102434"></a>Description</strong></p>
</td>
</tr>
<tr id="row81692010682"><td class="cellrowborder" valign="top" width="17.67176717671767%"><p id="p151851333151813"><a name="p151851333151813"></a><a name="p151851333151813"></a>id</p>
</td>
<td class="cellrowborder" valign="top" width="22.562256225622562%"><p id="p3182153331820"><a name="p3182153331820"></a><a name="p3182153331820"></a>oid</p>
</td>
<td class="cellrowborder" valign="top" width="59.765976597659765%"><p id="p1712119664518"><a name="p1712119664518"></a><a name="p1712119664518"></a>Object ID.</p>
</td>
</tr>
<tr id="row413211712177"><td class="cellrowborder" valign="top" width="17.67176717671767%"><p id="p1117973381818"><a name="p1117973381818"></a><a name="p1117973381818"></a>owner</p>
</td>
<td class="cellrowborder" valign="top" width="22.562256225622562%"><p id="p71771233131813"><a name="p71771233131813"></a><a name="p71771233131813"></a>bigint</p>
</td>
<td class="cellrowborder" valign="top" width="59.765976597659765%"><p id="p14175538114514"><a name="p14175538114514"></a><a name="p14175538114514"></a>ID of the user who creates the object.</p>
</td>
</tr>
<tr id="row201063118176"><td class="cellrowborder" valign="top" width="17.67176717671767%"><p id="p171743335182"><a name="p171743335182"></a><a name="p171743335182"></a>nspid</p>
</td>
<td class="cellrowborder" valign="top" width="22.562256225622562%"><p id="p71723339188"><a name="p71723339188"></a><a name="p71723339188"></a>oid</p>
</td>
<td class="cellrowborder" valign="top" width="59.765976597659765%"><p id="p58517208219"><a name="p58517208219"></a><a name="p58517208219"></a>Schema ID of an object.</p>
</td>
</tr>
<tr id="row3696121410172"><td class="cellrowborder" valign="top" width="17.67176717671767%"><p id="p9169173311813"><a name="p9169173311813"></a><a name="p9169173311813"></a>name</p>
</td>
<td class="cellrowborder" valign="top" width="22.562256225622562%"><p id="p1616633315187"><a name="p1616633315187"></a><a name="p1616633315187"></a>name</p>
</td>
<td class="cellrowborder" valign="top" width="59.765976597659765%"><p id="p6165533191819"><a name="p6165533191819"></a><a name="p6165533191819"></a>Object name.</p>
</td>
</tr>
<tr id="row0654102510108"><td class="cellrowborder" valign="top" width="17.67176717671767%"><p id="p616313320185"><a name="p616313320185"></a><a name="p616313320185"></a>type</p>
</td>
<td class="cellrowborder" valign="top" width="22.562256225622562%"><p id="p2161133361814"><a name="p2161133361814"></a><a name="p2161133361814"></a>text</p>
</td>
<td class="cellrowborder" valign="top" width="59.765976597659765%"><p id="p174611947474"><a name="p174611947474"></a><a name="p174611947474"></a>Object type (<strong id="b2024916818433"><a name="b2024916818433"></a><a name="b2024916818433"></a>procedure</strong>/<strong id="b1625018810433"><a name="b1625018810433"></a><a name="b1625018810433"></a>function</strong>/<strong id="b82501788431"><a name="b82501788431"></a><a name="b82501788431"></a>package</strong>/<strong id="b925016810438"><a name="b925016810438"></a><a name="b925016810438"></a>package body</strong>).</p>
</td>
</tr>
<tr id="row113297295101"><td class="cellrowborder" valign="top" width="17.67176717671767%"><p id="p161581133141813"><a name="p161581133141813"></a><a name="p161581133141813"></a>line</p>
</td>
<td class="cellrowborder" valign="top" width="22.562256225622562%"><p id="p1658273473911"><a name="p1658273473911"></a><a name="p1658273473911"></a>integer</p>
</td>
<td class="cellrowborder" valign="top" width="59.765976597659765%"><p id="p11687168142613"><a name="p11687168142613"></a><a name="p11687168142613"></a>Line number.</p>
</td>
</tr>
<tr id="row1914143861019"><td class="cellrowborder" valign="top" width="17.67176717671767%"><p id="p13151163321817"><a name="p13151163321817"></a><a name="p13151163321817"></a>src</p>
</td>
<td class="cellrowborder" valign="top" width="22.562256225622562%"><p id="p10972104693918"><a name="p10972104693918"></a><a name="p10972104693918"></a>text</p>
</td>
<td class="cellrowborder" valign="top" width="59.765976597659765%"><p id="p171483338181"><a name="p171483338181"></a><a name="p171483338181"></a>Error message.</p>
</td>
</tr>
</tbody>
</table>

