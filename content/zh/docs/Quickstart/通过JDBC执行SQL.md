# 通过JDBC执行SQL<a name="ZH-CN_TOPIC_0241704269"></a>

## JDBC包与驱动类<a name="section135946503153"></a>

-   JDBC包

    在linux服务器端源代码目录下执行build.sh，获得驱动jar包postgresql.jar，包位置在源代码目录下。从发布包中获取, 包名为openGauss-x.x.x-操作系统版本号-64bit-Jdbc.tar.gz。

    驱动包与PostgreSQL保持兼容，其中类名、类结构与PostgreSQL驱动完全一致，曾经运行于PostgreSQL的应用程序可以直接移植到当前系统使用。

-   驱动类

    在创建数据库连接之前，需要加载数据库驱动类“org.postgresql.Driver”。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >由于openGauss在JDBC的使用上与PG的使用方法保持兼容，所以同时在同一进程内使用两个JDBC驱动的时候，可能会类名冲突。


## 加载驱动<a name="section126336264203"></a>

在创建数据库连接之前，需要先加载数据库驱动程序。

加载驱动有两种方法：

-   在代码中创建连接之前任意位置隐含装载：Class.forName\("org.postgresql.Driver"\);
-   在JVM启动时参数传递：java -Djdbc.drivers=org.postgresql.Driver jdbctest

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >上述jdbctest为测试用例程序的名称。


## 连接数据库<a name="section3739105302112"></a>

在创建数据库连接之后，才能使用它来执行SQL语句操作数据。

**函数原型**

JDBC提供了三个方法，用于创建数据库连接。

-   DriverManager.getConnection\(String url\);
-   DriverManager.getConnection\(String url, Properties info\);
-   DriverManager.getConnection\(String url, String user, String password\);

**参数**

**表 1**  数据库连接参数

<a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_tfcd5d7b17d27423d9d3b648da394ac52"></a>
<table><thead align="left"><tr id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_r13c3173c830e468eb39e6aa804dfed59"><th class="cellrowborder" valign="top" width="13%" id="mcps1.2.3.1.1"><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a5501243843d34369bb879eed773000ae"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a5501243843d34369bb879eed773000ae"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a5501243843d34369bb879eed773000ae"></a>参数</p>
</th>
<th class="cellrowborder" valign="top" width="87%" id="mcps1.2.3.1.2"><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a2939f7c5b53e49479763c806734c4f93"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a2939f7c5b53e49479763c806734c4f93"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a2939f7c5b53e49479763c806734c4f93"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_re1e62c9744ec489884f418b7f28dafe3"><td class="cellrowborder" valign="top" width="13%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a89d7b3d8fd624d06b353a9947f7905fe"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a89d7b3d8fd624d06b353a9947f7905fe"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a89d7b3d8fd624d06b353a9947f7905fe"></a>url</p>
</td>
<td class="cellrowborder" valign="top" width="87%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_aa712d56d1c1b48c7818432cfaf686c60"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_aa712d56d1c1b48c7818432cfaf686c60"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_aa712d56d1c1b48c7818432cfaf686c60"></a>postgresql.jar数据库连接描述符。格式如下：</p>
<a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_ud24eb001d2c147738618d53304180b18"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_ud24eb001d2c147738618d53304180b18"></a><ul id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_ud24eb001d2c147738618d53304180b18"><li>jdbc:postgresql:database</li><li>jdbc:postgresql://host/database</li><li>jdbc:postgresql://host:port/database</li><li>jdbc:postgresql://host:port/database?param1=value1&amp;param2=value2</li><li>jdbc:postgresql://host1:port1,host2:port2/database?param1=value1&amp;param2=value2</li></ul>
<div class="note" id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_na32bb62c928d4a4a96b51b226ee5631b"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_na32bb62c928d4a4a96b51b226ee5631b"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_na32bb62c928d4a4a96b51b226ee5631b"></a><span class="notetitle"> 说明： </span><div class="notebody"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_u37354cd4fb1547e3973b70859e9fe729"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_u37354cd4fb1547e3973b70859e9fe729"></a><ul id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_u37354cd4fb1547e3973b70859e9fe729"><li>database为要连接的数据库名称。</li><li>host为数据库服务器名称或IP地址。<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_p461072082618"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_p461072082618"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_p461072082618"></a>连接<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_text1998119910444"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_text1998119910444"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_text1998119910444"></a><span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text202481331142613"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text202481331142613"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text202481331142613"></a><span id="zh-cn_topic_0244720262_text17015171312"><a name="zh-cn_topic_0244720262_text17015171312"></a><a name="zh-cn_topic_0244720262_text17015171312"></a>openGauss</span></span></span>的机器与<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_text17887837132414"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_text17887837132414"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_text17887837132414"></a><span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text12227183612619"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text12227183612619"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text12227183612619"></a><span id="zh-cn_topic_0244720262_text01235217138"><a name="zh-cn_topic_0244720262_text01235217138"></a><a name="zh-cn_topic_0244720262_text01235217138"></a>openGauss</span></span></span>不在同一网段时，host指定的IP地址应为Manager界面上所设的coo.cooListenIp2（应用访问IP）的取值。</p>
<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_p1441610315219"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_p1441610315219"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_p1441610315219"></a>由于安全原因，<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text924214328594"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text924214328594"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text924214328594"></a>数据库主节点</span>禁止<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text42571145173519"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text42571145173519"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text42571145173519"></a>openGauss</span>内部其他节点无认证接入。如果要在<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text106581047153514"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text106581047153514"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text106581047153514"></a>openGauss</span>内部访问<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text6112765112"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text6112765112"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text6112765112"></a>数据库主节点</span>，请将JDBC程序部署在<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text414820885115"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text414820885115"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text414820885115"></a>数据库主节点</span>所在机器，host使用"127.0.0.1"。否则可能会出现“FATAL: Forbid remote connection with trust method!”错误。</p>
<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_p572510297236"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_p572510297236"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_p572510297236"></a>建议业务系统单独部署在<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text512019495351"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text512019495351"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text512019495351"></a>openGauss</span>外部，否则可能会影响数据库运行性能。</p>
<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p15116145917295"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p15116145917295"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p15116145917295"></a>缺省情况下，连接服务器为localhost。</p>
</li><li>port为数据库服务器端口。<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a0f37847b6f9c44ebacd95d8a7d5e1626"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a0f37847b6f9c44ebacd95d8a7d5e1626"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a0f37847b6f9c44ebacd95d8a7d5e1626"></a>缺省情况下，会尝试连接到5431端口的database。</p>
</li><li>param为参数名称，即数据库连接属性。<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p11846133317341"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p11846133317341"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p11846133317341"></a>参数可以配置在URL中，以"?"开始配置，以"="给参数赋值，以"&amp;"作为不同参数的间隔。也可以采用info对象的属性方式进行配置，详细示例会在本节给出。</p>
</li><li>value为参数值，即数据库连接属性值。</li></ul>
</div></div>
</td>
</tr>
<tr id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_ref8dd9fc7790450ca15b4f30b96a0a18"><td class="cellrowborder" valign="top" width="13%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a1c692d258574463c90cbadc432be1c2e"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a1c692d258574463c90cbadc432be1c2e"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a1c692d258574463c90cbadc432be1c2e"></a>info</p>
</td>
<td class="cellrowborder" valign="top" width="87%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_aade6bbcac4be4b7cacc238da5173b93d"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_aade6bbcac4be4b7cacc238da5173b93d"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_aade6bbcac4be4b7cacc238da5173b93d"></a>数据库连接属性。常用的属性如下：</p>
<a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_u8546689def034a5a8257c477a574f39e"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_u8546689def034a5a8257c477a574f39e"></a><ul id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_u8546689def034a5a8257c477a574f39e"><li>PGDBNAME：String类型。表示数据库名称。（URL中无需配置该参数，自动从URL中解析）</li><li>PGHOST：String类型。主机IP地址。详细示例见下。</li><li>PGPORT：Integer类型。主机端口号。详细示例见下。</li><li>user：String类型。表示创建连接的数据库用户。</li><li>password：String类型。表示数据库用户的密码。</li><li>loggerLevel：String类型。目前支持3种级别：OFF、DEBUG、TRACE。设置为OFF关闭日志，设置为DEBUG和TRACE记录的日志信息详细程度不同。</li><li>loggerFile：String类型。Logger输出的文件名。需要显示指定日志文件名，若未指定目录则生成在客户端运行程序目录。</li><li>allowEncodingChanges：Boolean类型。设置该参数值为“true”进行字符集类型更改，配合characterEncoding=CHARSET设置字符集，二者使用"&amp;"分隔。</li><li>currentSchema：String类型。在search-path中指定要设置的schema。</li><li>hostRecheckSeconds：Integer类型。JDBC尝试连接主机后会保存主机状态：连接成功或连接失败。在hostRecheckSeconds时间内保持可信，超过则状态失效。缺省值是10秒。</li><li>ssl：Boolean类型。以SSL方式连接。<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p175682912210"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p175682912210"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p175682912210"></a>ssl=true可支持NonValidatingFactory通道和使用证书的方式：</p>
<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p1075620296222"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p1075620296222"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p1075620296222"></a>1、NonValidatingFactory通道需要配置用户名和密码，同时将SSL设置为true。</p>
<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p9756122919225"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p9756122919225"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_p9756122919225"></a>2、配置客户端证书、密钥、根证书，将SSL设置为true。</p>
</li><li>sslmode：String类型。SSL认证方式。取值范围为：require、verify-ca、verify-full。<a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_ul460013619316"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_ul460013619316"></a><ul id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_ul460013619316"><li>require只尝试SSL连接，如果存在CA文件，则应设置成verify-ca的方式验证。</li><li>verify-ca只尝试SSL连接，并且验证服务器是否具有由可信任的证书机构签发的证书。</li><li>verify-full只尝试SSL连接，并且验证服务器是否具有由可信任的证书机构签发的证书，以及验证服务器主机名是否与证书中的一致。</li></ul>
</li><li>sslcert：String类型。提供证书文件的完整路径。客户端和服务端证书的类型为End Entity。</li><li>sslkey：String类型。提供密钥文件的完整路径。使用时将客户端证书转换为DER格式：<pre class="screen" id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_screen65436268111"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_screen65436268111"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_screen65436268111"></a>openssl pkcs8 -topk8 -outform DER -in client.key -out client.key.pk8 -nocrypt</pre>
</li><li>sslrootcert：String类型。SSL根证书的文件名。根证书的类型为CA。</li><li>sslpassword：String类型。提供给ConsoleCallbackHandler使用。</li><li>sslpasswordcallback：String类型。SSL密码提供者的类名。缺省值：org.postgresql.ssl.jdbc4.LibPQFactory.ConsoleCallbackHandler。</li><li>sslfactory：String类型。提供的值是SSLSocketFactory在建立SSL连接时用的类名。</li><li>sslfactoryarg：String类型。此值是上面提供的sslfactory类的构造函数的可选参数（不推荐使用）。</li><li>sslhostnameverifier：String类型。主机名验证程序的类名。接口实现javax.net.ssl.HostnameVerifier，默认使用org.postgresql.ssl.PGjdbcHostnameVerifier。</li><li>loginTimeout：Integer类型。指建立数据库连接的等待时间。超时时间单位为秒。</li><li>connectTimeout：Integer类型。用于连接服务器操作的超时值。如果连接到服务器花费的时间超过此值，则连接断开。超时时间单位为秒，值为0时表示已禁用，timeout不发生。</li><li>socketTimeout：Integer类型。用于socket读取操作的超时值。如果从服务器读取所花费的时间超过此值，则连接关闭。超时时间单位为秒，值为0时表示已禁用，timeout不发生。</li><li>cancelSignalTimeout：Integer类型。发送取消消息本身可能会阻塞，此属性控制用于取消命令的“connect超时”和“socket超时”。超时时间单位为秒，默认值为10秒。</li><li>tcpKeepAlive：Boolean类型。启用或禁用TCP保活探测功能。默认为false。</li><li>logUnclosedConnections：Boolean类型。客户端可能由于未调用Connection对象的close()方法而泄漏Connection对象。最终这些对象将被垃圾回收，并且调用finalize()方法。如果调用者自己忽略了此操作，该方法将关闭Connection。</li><li>assumeMinServerVersion：String类型。客户端会发送请求进行float精度设置。该参数设置要连接的服务器版本，如assumeMinServerVersion=9.0，可以在建立时减少相关包的发送。</li><li>ApplicationName：String类型。设置正在使用连接的JDBC驱动的名称。通过在数据库主节点上查询pg_stat_activity表可以看到正在连接的客户端信息，JDBC驱动名称显示在application_name列。缺省值为PostgreSQL JDBC Driver。</li><li>connectionExtraInfo：Boolean类型。表示驱动是否上报当前驱动的部署路径、进程属主用户到数据库。<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p126364543506"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p126364543506"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p126364543506"></a>取值范围：true或false，默认值为false。设置connectionExtraInfo为true，JDBC驱动会将当前驱动的部署路径、进程属主用户上报到数据库中，记录在connection_info参数里；同时可以在PG_STAT_ACTIVITY中查询到。</p>
</li><li>autosave：String类型。共有3种："always", "never", "conservative"。如果查询失败，指定驱动程序应该执行的操作。在autosave=always模式下，JDBC驱动程序在每次查询之前设置一个保存点，并在失败时回滚到该保存点。在autosave=never模式（默认）下，无保存点。在autosave=conservative模式下，每次查询都会设置保存点，但是只会在“statement XXX无效”等情况下回滚并重试。</li><li>protocolVersion：Integer类型。连接协议版本号，目前仅支持3。注意：设置该参数时将采用md5加密方式，需要同步修改数据库的加密方式：gs_guc set -N all -I all -c "password_encryption_type=1" ，重启<span id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text11512175513513"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text11512175513513"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_text11512175513513"></a>openGauss</span>生效后需要创建用md5方式加密口令的用户。同时修改pg_hba.conf，将客户端连接方式修改为md5。用新建用户进行登录（不推荐）。</li><li>prepareThreshold：Integer类型。控制parse语句何时发送。默认值是5。第一次parse一个SQL比较慢，后面再parse就会比较快，因为有缓存了。如果一个会话连续多次执行同一个SQL，在达到prepareThreshold次数以上时，JDBC将不再对这个SQL发送parse命令。</li><li>preparedStatementCacheQueries：Integer类型。确定每个连接中缓存的查询数，默认情况下是256。若在prepareStatement()调用中使用超过256个不同的查询，则最近最少使用的查询缓存将被丢弃。0表示禁用缓存。</li><li>preparedStatementCacheSizeMiB：Integer类型。确定每个连接可缓存的最大值（以兆字节为单位），默认情况下是5。若缓存了超过5MB的查询，则最近最少使用的查询缓存将被丢弃。0表示禁用缓存。</li><li>databaseMetadataCacheFields：Integer类型。默认值是65536。指定每个连接可缓存的最大值。“0”表示禁用缓存。</li><li>databaseMetadataCacheFieldsMiB：Integer类型。默认值是5。每个连接可缓存的最大值，单位是MB。“0”表示禁用缓存。</li><li>stringtype：String类型，可选字段为：false, "unspecified", "varchar"。设置通过setString()方法使用的PreparedStatement参数的类型，如果stringtype设置为VARCHAR（默认值），则这些参数将作为varchar参数发送给服务器。若stringtype设置为unspecified，则参数将作为untyped值发送到服务器，服务器将尝试推断适当的类型。</li><li>batchMode：Boolean类型。用于确定是否使用batch模式连接。</li><li>fetchsize：Integer类型。用于设置数据库连接所创建statement的默认fetchsize。</li><li>reWriteBatchedInserts：Boolean类型。批量导入时，该参数设置为on，可将N条插入语句合并为一条：insert into TABLE_NAME values(values1, ..., valuesN), ..., (values1, ..., valuesN);使用该参数时，需设置batchMode=off。</li><li>unknownLength：Integer类型，默认为Integer.MAX_VALUE。某些postgresql类型（例如TEXT）没有明确定义的长度，当通过ResultSetMetaData.getColumnDisplaySize和ResultSetMetaData.getPrecision等函数返回关于这些类型的数据时，此参数指定未知长度类型的长度。</li><li>defaultRowFetchSize：Integer类型。确定一次fetch在ResultSet中读取的行数。限制每次访问数据库时读取的行数可以避免不必要的内存消耗，从而避免OutOfMemoryException。缺省值是0，这意味着ResultSet中将一次获取所有行。没有负数。</li><li>binaryTransfer：Boolean类型。使用二进制格式发送和接收数据，默认值为“false”。</li><li>binaryTransferEnable：String类型。启用二进制传输的类型列表，以逗号分隔。OID编号和名称二选一，例如binaryTransferEnable=Integer4_ARRAY,Integer8_ARRAY。<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p3778145719527"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p3778145719527"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p3778145719527"></a>比如：OID名称为BLOB，编号为88，可以如下配置：</p>
<p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p12336192714527"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p12336192714527"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_p12336192714527"></a>binaryTransferEnable=BLOB 或 binaryTransferEnable=88</p>
</li><li>binaryTransferDisEnable：String类型。禁用二进制传输的类型列表，以逗号分隔。OID编号和名称二选一。覆盖binaryTransferEnable的设置。</li><li>blobMode：String类型。用于设置setBinaryStream方法为不同类型的数据赋值，设置为on时表示为blob类型数据赋值，设置为off时表示为bytea类型数据赋值，默认为on。</li><li>socketFactory：String类型。用于创建与服务器socket连接的类的名称。该类必须实现了接口“javax.net.SocketFactory”，并定义无参或单String参数的构造函数。</li><li>socketFactoryArg：String类型。此值是上面提供的socketFactory类的构造函数的可选参数，不推荐使用。</li><li>receiveBufferSize：Integer类型。该值用于设置连接流上的SO_RCVBUF。</li><li>sendBufferSize：Integer类型。该值用于设置连接流上的SO_SNDBUF。</li><li>preferQueryMode：String类型。共有4种："extended", "extendedForPrepared", "extendedCacheEverything", "simple"。用于指定执行查询的模式，simple模式会excute，不parse和bind；extended模式会bind和excute；extendedForPrepared模式为prepared statement扩展使用；extendedCacheEverything模式会缓存每个statement。</li></ul>
</td>
</tr>
<tr id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_r8005ff51ee3d40e184a8db722d0f18ae"><td class="cellrowborder" valign="top" width="13%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a925328f5c60948c98b489a99cbc20017"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a925328f5c60948c98b489a99cbc20017"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a925328f5c60948c98b489a99cbc20017"></a>user</p>
</td>
<td class="cellrowborder" valign="top" width="87%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a12ebd01bc95b4c2cbaf12561c10053df"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a12ebd01bc95b4c2cbaf12561c10053df"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a12ebd01bc95b4c2cbaf12561c10053df"></a>数据库用户。</p>
</td>
</tr>
<tr id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_rc74336c5bc0640da9b968c8b953ea76d"><td class="cellrowborder" valign="top" width="13%" headers="mcps1.2.3.1.1 "><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_ad02cd653ced04960aec39fa00ed2bb40"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_ad02cd653ced04960aec39fa00ed2bb40"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_ad02cd653ced04960aec39fa00ed2bb40"></a>password</p>
</td>
<td class="cellrowborder" valign="top" width="87%" headers="mcps1.2.3.1.2 "><p id="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a112a5bf510a14f4d95bd069bc1afc01a"><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a112a5bf510a14f4d95bd069bc1afc01a"></a><a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_a112a5bf510a14f4d95bd069bc1afc01a"></a>数据库用户的密码。</p>
</td>
</tr>
</tbody>
</table>

## 示例<a name="zh-cn_topic_0244720262_zh-cn_topic_0237120381_zh-cn_topic_0213179126_zh-cn_topic_0189251768_zh-cn_topic_0059779354_sa87cf707a76c493997989289921f9202"></a>

-   示例1：此示例将演示如何基于openGauss提供的JDBC接口连接数据库。

    ```
    //以下代码将获取数据库连接操作封装为一个接口，可通过给定用户名和密码来连接数据库。
    public static Connection getConnect(String username, String passwd)
        {
            //驱动类。
            String driver = "org.postgresql.Driver";
            //数据库连接描述符。
            String sourceURL = "jdbc:postgresql://10.10.0.13:8000/postgres";
            Connection conn = null;
            
            try
            {
                //加载驱动。
                Class.forName(driver);
            }
            catch( Exception e )
            {
                e.printStackTrace();
                return null;
            }
            
            try
            {
                 //创建连接。
                conn = DriverManager.getConnection(sourceURL, username, passwd);
                System.out.println("Connection succeed!");
            }
            catch(Exception e)
            {
                e.printStackTrace();
                return null;
            }
            
            return conn;
        };
    // 以下代码将使用Properties对象作为参数建立连接
    public static Connection getConnectUseProp(String username, String passwd)
        {
            //驱动类。
            String driver = "org.postgresql.Driver";
            //数据库连接描述符。
            String sourceURL = "jdbc:postgresql://10.10.0.13:8000/postgres?";
            Connection conn = null;
            Properties info = new Properties();
            
            try
            {
                //加载驱动。
                Class.forName(driver);
            }
            catch( Exception e )
            {
                e.printStackTrace();
                return null;
            }
            
            try
            {
                 info.setProperty("user", username);
                 info.setProperty("password", passwd);
                 //创建连接。
                 conn = DriverManager.getConnection(sourceURL, info);
                 System.out.println("Connection succeed!");
            }
            catch(Exception e)
            {
                e.printStackTrace();
                return null;
            }
            
            return conn;
        };
    ```

-   示例2：此示例将演示如何基于openGauss提供的JDBC接口开发应用程序。

    ```
    //DBtest.java
    //演示基于JDBC开发的主要步骤，会涉及创建数据库、创建表、插入数据等。
    
    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.PreparedStatement;
    import java.sql.SQLException;
    import java.sql.Statement;
    import java.sql.CallableStatement;
    
    public class DBTest {
    
      //创建数据库连接。
      public static Connection GetConnection(String username, String passwd) {
        String driver = "org.postgresql.Driver";
        String sourceURL = "jdbc:postgresql://localhost:8000/postgres";
        Connection conn = null;
        try {
          //加载数据库驱动。
          Class.forName(driver).newInstance();
        } catch (Exception e) {
          e.printStackTrace();
          return null;
        }
    
        try {
          //创建数据库连接。
          conn = DriverManager.getConnection(sourceURL, username, passwd);
          System.out.println("Connection succeed!");
        } catch (Exception e) {
          e.printStackTrace();
          return null;
        }
    
        return conn;
      };
    
      //执行普通SQL语句，创建customer_t1表。
      public static void CreateTable(Connection conn) {
        Statement stmt = null;
        try {
          stmt = conn.createStatement();
    
          //执行普通SQL语句。
          int rc = stmt
              .executeUpdate("CREATE TABLE customer_t1(c_customer_sk INTEGER, c_customer_name VARCHAR(32));");
    
          stmt.close();
        } catch (SQLException e) {
          if (stmt != null) {
            try {
              stmt.close();
            } catch (SQLException e1) {
              e1.printStackTrace();
            }
          }
          e.printStackTrace();
        }
      }
    
      //执行预处理语句，批量插入数据。
      public static void BatchInsertData(Connection conn) {
        PreparedStatement pst = null;
    
        try {
          //生成预处理语句。
          pst = conn.prepareStatement("INSERT INTO customer_t1 VALUES (?,?)");
          for (int i = 0; i < 3; i++) {
            //添加参数。
            pst.setInt(1, i);
            pst.setString(2, "data " + i);
            pst.addBatch();
          }
          //执行批处理。
          pst.executeBatch();
          pst.close();
        } catch (SQLException e) {
          if (pst != null) {
            try {
              pst.close();
            } catch (SQLException e1) {
            e1.printStackTrace();
            }
          }
          e.printStackTrace();
        }
      }
    
      //执行预编译语句，更新数据。
      public static void ExecPreparedSQL(Connection conn) {
        PreparedStatement pstmt = null;
        try {
          pstmt = conn
              .prepareStatement("UPDATE customer_t1 SET c_customer_name = ? WHERE c_customer_sk = 1");
          pstmt.setString(1, "new Data");
          int rowcount = pstmt.executeUpdate();
          pstmt.close();
        } catch (SQLException e) {
          if (pstmt != null) {
            try {
              pstmt.close();
            } catch (SQLException e1) {
              e1.printStackTrace();
            }
          }
          e.printStackTrace();
        }
      }
    
    
    //执行存储过程。
      public static void ExecCallableSQL(Connection conn) {
        CallableStatement cstmt = null;
        try {
          
          cstmt=conn.prepareCall("{? = CALL TESTPROC(?,?,?)}");
          cstmt.setInt(2, 50); 
          cstmt.setInt(1, 20);
          cstmt.setInt(3, 90);
          cstmt.registerOutParameter(4, Types.INTEGER);  //注册out类型的参数，类型为整型。
          cstmt.execute();
          int out = cstmt.getInt(4);  //获取out参数
          System.out.println("The CallableStatment TESTPROC returns:"+out);
          cstmt.close();
        } catch (SQLException e) {
          if (cstmt != null) {
            try {
              cstmt.close();
            } catch (SQLException e1) {
              e1.printStackTrace();
            }
          }
          e.printStackTrace();
        }
      }
      
    
      /**
       * 主程序，逐步调用各静态方法。
       * @param args
      */
      public static void main(String[] args) {
        //创建数据库连接。
        Connection conn = GetConnection("tester", "Password1234");
    
        //创建表。
        CreateTable(conn);
    
        //批插数据。
        BatchInsertData(conn);
    
        //执行预编译语句，更新数据。
        ExecPreparedSQL(conn);
    
        //执行存储过程。
        ExecCallableSQL(conn);
    
        //关闭数据库连接。
        try {
          conn.close();
        } catch (SQLException e) {
          e.printStackTrace();
        }
    
      }
    
    }
    ```


