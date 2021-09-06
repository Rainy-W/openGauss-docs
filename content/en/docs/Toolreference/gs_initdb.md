# gs\_initdb<a name="EN-US_TOPIC_0249632240"></a>

## Overview<a name="section7777368159"></a>

**Background**

When a database is initialized using  **gs\_initdb**, a database directory is created, a system catalog is generated, and a default database and a template database are created.

**System catalog**

A large number of system catalogs and views are generated when a database is initialized, many of which allow access from any database user.

>![](public_sys-resources/icon-note.gif) **NOTE:**   
>Permissions on  **pg\_user\_status**  and  **pg\_auth\_history**  system catalogs are granted only to initialized users and  **sysadmin**  users.  

**Generated database**

-   template1: a template database. When you create a database, all content in the template1 database is copied. The settings of template1 are determined by the parameters of  **gs\_initdb**.
-   template0: Is the initial backup database provided by openGauss. template0 can be used to generate an empty database if necessary.
-   postgres: a default database provided for users, tools, and third-party applications.

## Usage Guide<a name="section209951723181812"></a>

**Background**

During installation, you are advised to use the  **-D**  parameter to call  **gs\_initdb**  to initialize a database. If a database needs to be initialized to rectify a fault, run  **gs\_initdb**.

-   Although  **gs\_initdb**  attempts to create the corresponding data directory, it may not have the permission to do so, because in most cases, the parent directory is owned by user  **root**. To create a data directory, create an empty data directory as user  **root**  first and deliver the ownership of this directory to the database user using  **chown**.
-   **gs\_initdb**  is used to set the template1 database and the setting becomes the default setting of other databases.
-   **gs\_initdb**  initializes the default locale and character set encoding of a database. The character set encoding, character encoding sequence \(LC\_COLLATE\), and character set class \(LC\_CTYPE, such as uppercase letters, lowercase letters, and digits\) can be separately set for databases when you create them.

**syntax**

```
gs_initdb [OPTION]... [DATADIR]
```

**Procedure**

1.  Log in as the OS user  **omm**  to the primary database node.
2.  Plan the database directory.

    a. Switch to user  **root**.

      ```
      su - root
      ```

    b. Enter the username and password as prompted.

3.  Go to the  **/opt/gaussdb**  directory and create the  **data1**  directory.

    ```
    cd /opt/gaussdb
    mkdir data1
    ```

    a. Allocate the ownership of the  **data1**  directory to the database user omm. dbgrp is the user group that the omm belongs to.

    ```
    chown omm:dbgrp data1
    ```

    b. Exit user  **root**.

    ```
    exit
    ```

4.  Run the  **gs\_initdb**  command to initialize the database.

    ```
    gs_initdb -D /opt/gaussdb/data1 -w "Gauss@123" --nodename='data1'
    ```



## Command Reference<a name="section01341136122018"></a>

For details about common parameters and uncommon parameters supported by  **gs\_initdb**, see  [Table 1](#en-us_topic_0237152414_en-us_topic_0059778168_t7527cd2e8e304b64bec55dcd38b701bb)  and  [Table 2](#en-us_topic_0237152414_en-us_topic_0059778168_t2f464cb1775044808eceb29e25d6d37f).

**Table  1**  Common parameters

<a name="en-us_topic_0237152414_en-us_topic_0059778168_t7527cd2e8e304b64bec55dcd38b701bb"></a>

<table><thead align="left"><tr id="en-us_topic_0237152414_en-us_topic_0059778168_rb04ed4dbb2024e91814fe29c62058a1e"><th class="cellrowborder" valign="top" width="23.76%" id="mcps1.2.4.1.1"><p id="en-us_topic_0237152414_en-us_topic_0059778168_abb1d0e137f344644873d231722922745"><a name="en-us_topic_0237152414_en-us_topic_0059778168_abb1d0e137f344644873d231722922745"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_abb1d0e137f344644873d231722922745"></a>Parameter</p>
</th>
<th class="cellrowborder" valign="top" width="32.6%" id="mcps1.2.4.1.2"><p id="en-us_topic_0237152414_en-us_topic_0059778168_a2a756e3c53094c5ea62729be1496108e"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a2a756e3c53094c5ea62729be1496108e"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a2a756e3c53094c5ea62729be1496108e"></a>Description</p>
</th>
<th class="cellrowborder" valign="top" width="43.64%" id="mcps1.2.4.1.3"><p id="en-us_topic_0237152414_en-us_topic_0059778168_ab80eddf3dfec41808d7b2abeeb2768f7"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab80eddf3dfec41808d7b2abeeb2768f7"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab80eddf3dfec41808d7b2abeeb2768f7"></a>Value Range</p>
</th>
</tr>
</thead>
<tbody><tr id="en-us_topic_0237152414_en-us_topic_0059778168_rd179fba4db404defa826417a64d12321"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a3cb75dc19ee843408dc2738c6fbdacf5"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a3cb75dc19ee843408dc2738c6fbdacf5"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a3cb75dc19ee843408dc2738c6fbdacf5"></a>-A, --auth=METHOD</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a860229dc5c08407d8732a736dd68009a"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a860229dc5c08407d8732a736dd68009a"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a860229dc5c08407d8732a736dd68009a"></a>Specifies the authentication method for local users used in <strong id="b115602186359"><a name="b115602186359"></a><a name="b115602186359"></a>pg_hba.conf</strong> (host and local rows).</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_a54020ab85c9b4a19b224c6ebb322f0fd"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a54020ab85c9b4a19b224c6ebb322f0fd"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a54020ab85c9b4a19b224c6ebb322f0fd"></a>Do not use <strong id="b16518182112357"><a name="b16518182112357"></a><a name="b16518182112357"></a>trust</strong>, which is the default value, unless you trust all local users on your system.</p>
<p id="p17236103166"><a name="p17236103166"></a><a name="p17236103166"></a></p>
<div class="notice" id="note20723141012164"><a name="note20723141012164"></a><a name="note20723141012164"></a><span class="noticetitle"> NOTICE: </span><div class="noticebody"><p id="p172361051616"><a name="p172361051616"></a><a name="p172361051616"></a>If the value is <strong id="b13597624133514"><a name="b13597624133514"></a><a name="b13597624133514"></a>md5</strong>, manually change the value of <strong id="b1660214248356"><a name="b1660214248356"></a><a name="b1660214248356"></a>password_encryption_type</strong> in the <strong id="b14602182410357"><a name="b14602182410357"></a><a name="b14602182410357"></a>postgresql.conf.sample</strong> file to <strong id="b96031924113518"><a name="b96031924113518"></a><a name="b96031924113518"></a>0</strong> and comment out the parameter for the change to take effect. <strong id="b4844183103516"><a name="b4844183103516"></a><a name="b4844183103516"></a>gs_initdb</strong> must be used in conjunction with <strong id="b1184912314351"><a name="b1184912314351"></a><a name="b1184912314351"></a>-W</strong>.</p>
</div></div>
<p id="p128419701615"><a name="p128419701615"></a><a name="p128419701615"></a></p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a63ab922337dd4d04aeeccf564ba3d5c9"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a63ab922337dd4d04aeeccf564ba3d5c9"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a63ab922337dd4d04aeeccf564ba3d5c9"></a>Values of <strong id="b1989583419355"><a name="b1989583419355"></a><a name="b1989583419355"></a>METHOD</strong>:</p>
<a name="en-us_topic_0237152414_en-us_topic_0059778168_uc88578ae236a4c23901b34032feecabd"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_uc88578ae236a4c23901b34032feecabd"></a><ul id="en-us_topic_0237152414_en-us_topic_0059778168_uc88578ae236a4c23901b34032feecabd"><li>trust</li><li>reject</li><li><strong id="b417544019355"><a name="b417544019355"></a><a name="b417544019355"></a>md5</strong> (an insecure algorithm, used for compatibility with earlier versions)</li><li>sha256</li><li>sm3</li></ul>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_ad4b8bf2ccd58490788bcf20d798a6b8d"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ad4b8bf2ccd58490788bcf20d798a6b8d"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ad4b8bf2ccd58490788bcf20d798a6b8d"></a>Default value: <strong id="b1816124312353"><a name="b1816124312353"></a><a name="b1816124312353"></a>trust</strong></p>
</td>
</tr>
<tr id="en-us_topic_0237152414_en-us_topic_0059778168_rf73b734c009149788c82b8aa398ac4af"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_af47c563f101c4cea8910db7f73abd15a"><a name="en-us_topic_0237152414_en-us_topic_0059778168_af47c563f101c4cea8910db7f73abd15a"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_af47c563f101c4cea8910db7f73abd15a"></a>--auth-host=METHOD</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ab7ee914f7d5b4ee2ae3788836f4a9ba2"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab7ee914f7d5b4ee2ae3788836f4a9ba2"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab7ee914f7d5b4ee2ae3788836f4a9ba2"></a>Specifies the authentication method for local users over TCP/IP used in <strong id="b990724512356"><a name="b990724512356"></a><a name="b990724512356"></a>pg_hba.conf</strong> (host rows).</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_ac3bf14491ea44e3787b2ea25eaac0aa5"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ac3bf14491ea44e3787b2ea25eaac0aa5"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ac3bf14491ea44e3787b2ea25eaac0aa5"></a>The value specified in the <strong id="b175354843519"><a name="b175354843519"></a><a name="b175354843519"></a>-A</strong> parameter is overwritten when this parameter is specified.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_adf75e663ccd74766a057c833066b5ecc"><a name="en-us_topic_0237152414_en-us_topic_0059778168_adf75e663ccd74766a057c833066b5ecc"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_adf75e663ccd74766a057c833066b5ecc"></a>Values of <strong id="b13146538351"><a name="b13146538351"></a><a name="b13146538351"></a>METHOD</strong>:</p>
<a name="en-us_topic_0237152414_en-us_topic_0059778168_ua0bc882ad25b4c30889bd8beb2df1684"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ua0bc882ad25b4c30889bd8beb2df1684"></a><ul id="en-us_topic_0237152414_en-us_topic_0059778168_ua0bc882ad25b4c30889bd8beb2df1684"><li>trust</li><li>reject</li><li><strong id="b014475463511"><a name="b014475463511"></a><a name="b014475463511"></a>md5</strong> (an insecure algorithm, used for compatibility with earlier versions)</li><li>sha256</li><li>sm3</li></ul>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_abd57e40a917448c2b7edd44975429a92"><a name="en-us_topic_0237152414_en-us_topic_0059778168_abd57e40a917448c2b7edd44975429a92"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_abd57e40a917448c2b7edd44975429a92"></a>Default value: <strong id="b151018544355"><a name="b151018544355"></a><a name="b151018544355"></a>trust</strong></p>
</td>
</tr>
<tr id="en-us_topic_0237152414_en-us_topic_0059778168_r68a0e327cb7d4bc996dc484686062273"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a40e2990b520b4b2f8e7844de42a774b6"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a40e2990b520b4b2f8e7844de42a774b6"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a40e2990b520b4b2f8e7844de42a774b6"></a>--auth-local=METHOD</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_af4e8d27f91c04a82b20477d9cf1c7437"><a name="en-us_topic_0237152414_en-us_topic_0059778168_af4e8d27f91c04a82b20477d9cf1c7437"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_af4e8d27f91c04a82b20477d9cf1c7437"></a>Specifies the authentication method for local users using Unix-domain socket connections used in <strong id="b610395573515"><a name="b610395573515"></a><a name="b610395573515"></a>pg_hba.conf</strong> (local rows).</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_a51a82f8aca384c1cb239459acc286af3"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a51a82f8aca384c1cb239459acc286af3"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a51a82f8aca384c1cb239459acc286af3"></a>The value specified in the <strong id="b5482076363"><a name="b5482076363"></a><a name="b5482076363"></a>-A</strong> parameter is overwritten when this parameter is specified.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a66742067d6074ae1b1e4f9dcf9c991ef"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a66742067d6074ae1b1e4f9dcf9c991ef"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a66742067d6074ae1b1e4f9dcf9c991ef"></a>Values of <strong id="b168720815369"><a name="b168720815369"></a><a name="b168720815369"></a>METHOD</strong>:</p>
<a name="en-us_topic_0237152414_en-us_topic_0059778168_ua8f41201ecce4a38838612396d037513"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ua8f41201ecce4a38838612396d037513"></a><ul id="en-us_topic_0237152414_en-us_topic_0059778168_ua8f41201ecce4a38838612396d037513"><li>trust</li><li>reject</li><li><strong id="b5889148193619"><a name="b5889148193619"></a><a name="b5889148193619"></a>md5</strong> (an insecure algorithm, used for compatibility with earlier versions)</li><li>sha256</li><li>sm3</li></ul>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p338903114578"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p338903114578"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p338903114578"></a>Default value: <strong id="b67616923615"><a name="b67616923615"></a><a name="b67616923615"></a>trust</strong></p>
</td>
</tr>
<tr id="en-us_topic_0237152414_en-us_topic_0059778168_r47ed009556a04eaf93f25efafa434b48"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ad674234b3ed54669ae4422ab93b53b7f"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ad674234b3ed54669ae4422ab93b53b7f"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ad674234b3ed54669ae4422ab93b53b7f"></a>[-D, --pgdata=]DATADIR</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a05e68f440cd848f5b234c12269b9a336"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a05e68f440cd848f5b234c12269b9a336"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a05e68f440cd848f5b234c12269b9a336"></a>Specifies the data directory.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_aaa96bc60571e4c03a72d420b5c231b04"><a name="en-us_topic_0237152414_en-us_topic_0059778168_aaa96bc60571e4c03a72d420b5c231b04"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_aaa96bc60571e4c03a72d420b5c231b04"></a>Set <strong id="b1346218113368"><a name="b1346218113368"></a><a name="b1346218113368"></a>DATADIR</strong> as required.</p>
</td>
</tr>
<tr id="row7206193362114"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p163219612615"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p163219612615"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p163219612615"></a>--nodename=NODENAME</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_afa4fd3ea63b44774b96814d9e7d5c33a"><a name="en-us_topic_0237152414_en-us_topic_0059778168_afa4fd3ea63b44774b96814d9e7d5c33a"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_afa4fd3ea63b44774b96814d9e7d5c33a"></a>Specifies the name of an initialized node.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="p39322419302"><a name="p39322419302"></a><a name="p39322419302"></a>The naming rules for nodes are as follows:</p>
<a name="ul0976124733118"></a><a name="ul0976124733118"></a><ul id="ul0976124733118"><li>The node name can only be lowercase letters (a-z), underscores (_), number signs (#), digits (0-9), and dollar signs ($).</li><li>The node name must start with a lowercase letter (a-z), or underscore (_).</li><li>The nodename cannot be an empty string, and cannot exceed 64 characters.</li></ul>
</td>
</tr>
<tr id="row1020519334218"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_abe6235a1ec1a41bdbe8b52c706ea8d94"><a name="en-us_topic_0237152414_en-us_topic_0059778168_abe6235a1ec1a41bdbe8b52c706ea8d94"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_abe6235a1ec1a41bdbe8b52c706ea8d94"></a>-E, --encoding=ENCODING</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p825108314042"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p825108314042"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p825108314042"></a>Specifies the encoding format for a new database.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_ul47919015168"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_ul47919015168"></a><ul id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_ul47919015168"><li>If this parameter is specified, the <strong id="b8771142235015"><a name="b8771142235015"></a><a name="b8771142235015"></a>--locale</strong> option must be added to specify the locale that supports the encoding format. If the <strong id="b2827305502"><a name="b2827305502"></a><a name="b2827305502"></a>--locale</strong> option is not added, the system default locale is used. If the encoding format in the system default locale is inconsistent with the encoding format specified in this parameter, the database initialization failed.</li><li>If this parameter is not specified, the encoding format of the system default locale is used. The system default locale and encoding format can be checked using the <strong id="b213054185017"><a name="b213054185017"></a><a name="b213054185017"></a>locale</strong> command as follows:<pre class="screen" id="en-us_topic_0237152414_en-us_topic_0059778168_s240f6735fde74db2a6ca95d0a9624015"><a name="en-us_topic_0237152414_en-us_topic_0059778168_s240f6735fde74db2a6ca95d0a9624015"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_s240f6735fde74db2a6ca95d0a9624015"></a><span id="en-us_topic_0237152414_text493110181653"><a name="en-us_topic_0237152414_text493110181653"></a><a name="en-us_topic_0237152414_text493110181653"></a>omm</span>@linux:~&gt; locale|grep LC_CTYPE
LC_CTYPE="en_US.UTF-8"
</pre>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_a631effe7371d428ea86042a709f14ecc"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a631effe7371d428ea86042a709f14ecc"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a631effe7371d428ea86042a709f14ecc"></a><strong id="b11910164515018"><a name="b11910164515018"></a><a name="b11910164515018"></a>UTF-8</strong> indicates the encoding format of the system default locale.</p>
</li></ul>
</td>
</tr>
<tr id="row1220518333214"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a4116cde05e05427daf2a46774bb81de8"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a4116cde05e05427daf2a46774bb81de8"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a4116cde05e05427daf2a46774bb81de8"></a>--locale=LOCALE</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ae62cadd0b34546d8bcc2c36dfb24ec10"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ae62cadd0b34546d8bcc2c36dfb24ec10"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ae62cadd0b34546d8bcc2c36dfb24ec10"></a>Specifies the default locale for the new database. You can run the <strong id="b32367245577"><a name="b32367245577"></a><a name="b32367245577"></a>locale -a</strong> command to view available locales, for example, zh_CN.gbk. If you do not want to specify a locale, set the parameter to <strong id="b078015995715"><a name="b078015995715"></a><a name="b078015995715"></a>C</strong>.</p>
<div class="notice" id="en-us_topic_0237152414_en-us_topic_0059778168_n68804385e7ce4f0ba5d88a03ae2e4c73"><a name="en-us_topic_0237152414_en-us_topic_0059778168_n68804385e7ce4f0ba5d88a03ae2e4c73"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_n68804385e7ce4f0ba5d88a03ae2e4c73"></a><span class="noticetitle"> NOTICE: </span><div class="noticebody"><p id="en-us_topic_0237152414_en-us_topic_0059778168_acccca55cfee647d581bdb9936e40bf31"><a name="en-us_topic_0237152414_en-us_topic_0059778168_acccca55cfee647d581bdb9936e40bf31"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_acccca55cfee647d581bdb9936e40bf31"></a>If the encoding format of the database is set, the encoding format of the user specified area must be consistent with the encoding format set by the user. Otherwise, database initialization fails.</p>
</div></div>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a803a9ebdf89c45f0a6b46a76846a93e0"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a803a9ebdf89c45f0a6b46a76846a93e0"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a803a9ebdf89c45f0a6b46a76846a93e0"></a>For example, to set the database encoding format to GBK, perform the following steps:</p>
<a name="en-us_topic_0237152414_en-us_topic_0059778168_o14641ef5676b4f6e8cf5555515076472"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_o14641ef5676b4f6e8cf5555515076472"></a><ol id="en-us_topic_0237152414_en-us_topic_0059778168_o14641ef5676b4f6e8cf5555515076472"><li>Run the <strong id="b187621010135910"><a name="b187621010135910"></a><a name="b187621010135910"></a>locale -a |grep gbk</strong> command to check the locale that supports GBK encoding:<pre class="screen" id="en-us_topic_0237152414_en-us_topic_0059778168_sde05eecf42394d6fafbef19c47e15d0d"><a name="en-us_topic_0237152414_en-us_topic_0059778168_sde05eecf42394d6fafbef19c47e15d0d"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_sde05eecf42394d6fafbef19c47e15d0d"></a><span id="en-us_topic_0237152414_text1781618203519"><a name="en-us_topic_0237152414_text1781618203519"></a><a name="en-us_topic_0237152414_text1781618203519"></a>omm</span>@linux:~&gt;  locale -a|grep gbk
zh_CN.gbk
zh_SG.gbk
</pre>
</li><li>Add the <strong id="b1922282075920"><a name="b1922282075920"></a><a name="b1922282075920"></a>--locale=zh_CN.gbk</strong> option when the database is initialized.</li></ol>
</td>
</tr>
<tr id="row020433382114"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="p19550114234517"><a name="p19550114234517"></a><a name="p19550114234517"></a>--dbcompatibility=DBCOMPATIBILITY</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="p1642510590523"><a name="p1642510590523"></a><a name="p1642510590523"></a>Specifies the type of the compatible database.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="p83741414135318"><a name="p83741414135318"></a><a name="p83741414135318"></a>Value range: A, B, C, and PG, indicating <strong id="b235119335593"><a name="b235119335593"></a><a name="b235119335593"></a>O</strong>, <strong id="b6357433175912"><a name="b6357433175912"></a><a name="b6357433175912"></a>MY</strong>, <strong id="b6357433175912"><a name="b6357433175912"></a><a name="b6357433175912"></a>TD</strong>, and <strong id="b535763385914"><a name="b535763385914"></a><a name="b535763385914"></a>POSTGRES</strong> databases, respectively.</p>
</td>
</tr>
<tr id="row142041433132110"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p296280814042"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p296280814042"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p296280814042"></a>--lc-collate=LOCALE</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_aa94596f2af8d4c94990bf5216816300c"><a name="en-us_topic_0237152414_en-us_topic_0059778168_aa94596f2af8d4c94990bf5216816300c"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_aa94596f2af8d4c94990bf5216816300c"></a>--lc-ctype=LOCALE</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_ad3d9c7e24fb049ffbfdb796a0cc703ae"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ad3d9c7e24fb049ffbfdb796a0cc703ae"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ad3d9c7e24fb049ffbfdb796a0cc703ae"></a>--lc-messages=LOCALE</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_ab87e33d09c4448138e1d1827ff0b8b1a"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab87e33d09c4448138e1d1827ff0b8b1a"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab87e33d09c4448138e1d1827ff0b8b1a"></a>--lc-monetary=LOCALE</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_a5d227938183a45f6b37b9d9455b9c5c6"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a5d227938183a45f6b37b9d9455b9c5c6"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a5d227938183a45f6b37b9d9455b9c5c6"></a>--lc-numeric=LOCALE</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_a71d42f00eeb84856adc6aa9acae96847"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a71d42f00eeb84856adc6aa9acae96847"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a71d42f00eeb84856adc6aa9acae96847"></a>--lc-time=LOCALE</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a9da720ea69b64f35adbb2f0240905dba"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a9da720ea69b64f35adbb2f0240905dba"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a9da720ea69b64f35adbb2f0240905dba"></a>Sets the specified locale for a new database.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ae044b8732e2e4ea78011b720dc1c3dda"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ae044b8732e2e4ea78011b720dc1c3dda"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ae044b8732e2e4ea78011b720dc1c3dda"></a>The parameter values must be supported by the OS.</p>
<div class="note" id="en-us_topic_0237152414_en-us_topic_0059778168_nc48697637c684e3fbc74abf832cbcfc5"><a name="en-us_topic_0237152414_en-us_topic_0059778168_nc48697637c684e3fbc74abf832cbcfc5"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_nc48697637c684e3fbc74abf832cbcfc5"></a><span class="notetitle"> NOTE: </span><div class="notebody"><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p783479093635"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p783479093635"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p783479093635"></a>If the <strong id="b184665519594"><a name="b184665519594"></a><a name="b184665519594"></a>--lc-collate</strong> parameter is not specified when the database is installed, the default value of <strong id="b75175513593"><a name="b75175513593"></a><a name="b75175513593"></a>--lc-collate</strong> is <strong id="b125135575914"><a name="b125135575914"></a><a name="b125135575914"></a>C</strong>.</p>
</div></div>
</td>
</tr>
<tr id="row10203113372110"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a61be6a616dbf499ebec62cdef807ee22"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a61be6a616dbf499ebec62cdef807ee22"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a61be6a616dbf499ebec62cdef807ee22"></a>--no-locale</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p93658414042"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p93658414042"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p93658414042"></a>Equivalent to <strong id="b52861223202"><a name="b52861223202"></a><a name="b52861223202"></a>--locale=C</strong>.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a02154014d8804f94b02a28b77103ec89"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a02154014d8804f94b02a28b77103ec89"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a02154014d8804f94b02a28b77103ec89"></a>-</p>
</td>
</tr>
<tr id="row1202113311214"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a1986cbe2b2054e9d949bd7d55ae635a5"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a1986cbe2b2054e9d949bd7d55ae635a5"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a1986cbe2b2054e9d949bd7d55ae635a5"></a>--pwfile=FILE</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p670015314042"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p670015314042"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p670015314042"></a>Reads the password for the database administrator from <strong id="b139809256019"><a name="b139809256019"></a><a name="b139809256019"></a>FILE</strong> during the running of <strong id="b1298017251405"><a name="b1298017251405"></a><a name="b1298017251405"></a>gs_initdb</strong>. The first row of the file is taken as the password.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ac7818172370b415c96f02f3eb914d9a1"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ac7818172370b415c96f02f3eb914d9a1"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ac7818172370b415c96f02f3eb914d9a1"></a>The format of <strong id="b157891537604"><a name="b157891537604"></a><a name="b157891537604"></a>FILE</strong> can be "a relative path+file" or "an absolute path+file". The relative path is relative to the current path.</p>
</td>
</tr>
<tr id="row7631753182119"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a3764e4e4a8a9461f8573f7cf4537514d"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a3764e4e4a8a9461f8573f7cf4537514d"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a3764e4e4a8a9461f8573f7cf4537514d"></a>-T, --text-search-config=CFG</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ade5a330c60df4410a111730ce871e9e5"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ade5a330c60df4410a111730ce871e9e5"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ade5a330c60df4410a111730ce871e9e5"></a>Specifies the default text search mode. The value of this parameter is not verified. After the configuration is successful, a log is recorded to notify you of the value of this parameter.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a23eba128a8c849039535c5d156384b1d"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a23eba128a8c849039535c5d156384b1d"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a23eba128a8c849039535c5d156384b1d"></a>Values of <strong id="b74111971410"><a name="b74111971410"></a><a name="b74111971410"></a>text-search-config</strong>:</p>
<a name="en-us_topic_0237152414_en-us_topic_0059778168_u32787aec68b74a82a8046c16faeab614"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_u32787aec68b74a82a8046c16faeab614"></a><ul id="en-us_topic_0237152414_en-us_topic_0059778168_u32787aec68b74a82a8046c16faeab614"><li><strong id="b16806410417"><a name="b16806410417"></a><a name="b16806410417"></a>english</strong>: full-document search</li><li><strong id="b1812711620116"><a name="b1812711620116"></a><a name="b1812711620116"></a>simple</strong>: common text search</li></ul>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_a4e71d94acb6d439a8776a3c7f493b753"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a4e71d94acb6d439a8776a3c7f493b753"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a4e71d94acb6d439a8776a3c7f493b753"></a>Default value: <strong id="b4649518916"><a name="b4649518916"></a><a name="b4649518916"></a>simple</strong></p>
</td>
</tr>
<tr id="row163014537211"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a863106d2c4154ecfb12f4bf35d8b6d31"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a863106d2c4154ecfb12f4bf35d8b6d31"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a863106d2c4154ecfb12f4bf35d8b6d31"></a>-U, --username=NAME</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a0fa722e5a044454fb85f37064f7daed8"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a0fa722e5a044454fb85f37064f7daed8"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a0fa722e5a044454fb85f37064f7daed8"></a>Selects the username of the database administrator.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ab72d990d68c049388be0cb39b489de4c"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab72d990d68c049388be0cb39b489de4c"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab72d990d68c049388be0cb39b489de4c"></a>Value range: normal database users</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_a371879078a194a3c97ac3b9f7e1901f1"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a371879078a194a3c97ac3b9f7e1901f1"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a371879078a194a3c97ac3b9f7e1901f1"></a>Default value: OS user who runs <strong id="b5793133714111"><a name="b5793133714111"></a><a name="b5793133714111"></a>gs_initdb</strong></p>
</td>
</tr>
<tr id="row10630653182111"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a9330b3666ebc49779fda7208430ef86e"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a9330b3666ebc49779fda7208430ef86e"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a9330b3666ebc49779fda7208430ef86e"></a>-W, --pwprompt</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a07c8842a8b014b60a7ee59bd5c00e083"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a07c8842a8b014b60a7ee59bd5c00e083"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a07c8842a8b014b60a7ee59bd5c00e083"></a>Prompts users to enter the password for the database administrator during the running of <strong id="b1798674516114"><a name="b1798674516114"></a><a name="b1798674516114"></a>gs_initdb</strong>.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a8bc2e6e444c94ee28ccf7fc7ef579234"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a8bc2e6e444c94ee28ccf7fc7ef579234"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a8bc2e6e444c94ee28ccf7fc7ef579234"></a>-</p>
</td>
</tr>
<tr id="row16309536215"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a531d28a82e5b42fda7427067e7a269e1"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a531d28a82e5b42fda7427067e7a269e1"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a531d28a82e5b42fda7427067e7a269e1"></a>-w, --pwpasswd=PASSWD</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a9036f008e6b2417ab4fd693d1afd5281"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a9036f008e6b2417ab4fd693d1afd5281"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a9036f008e6b2417ab4fd693d1afd5281"></a>Specifies the password of the database administrator by running commands during the running of <strong id="b268418491418"><a name="b268418491418"></a><a name="b268418491418"></a>gs_initdb</strong> instead of interactive input.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a166374baf1b9417fa4d889f2b9e7b3ff"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a166374baf1b9417fa4d889f2b9e7b3ff"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a166374baf1b9417fa4d889f2b9e7b3ff"></a>The password must meet the following complexity requirements:</p>
<a name="en-us_topic_0237152414_en-us_topic_0059778168_u5cf6c2fab0884e6db33705a8b1517dba"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_u5cf6c2fab0884e6db33705a8b1517dba"></a><ul id="en-us_topic_0237152414_en-us_topic_0059778168_u5cf6c2fab0884e6db33705a8b1517dba"><li>Contain at least eight characters.</li><li>Cannot be the same as the username, the current password (ALTER), or the current password in an inverted sequence.</li><li>Contain at least three of the following: uppercase characters (A to Z), lowercase characters (a to z), digits (0 to 9), and other characters (limited to ~!@#$%^&amp;*()-_=+\|[{}];:,&lt;.&gt;/?).</li></ul>
</td>
</tr>
<tr id="row16291853162117"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_afaf2c98348cc4a5591a2884a984183ce"><a name="en-us_topic_0237152414_en-us_topic_0059778168_afaf2c98348cc4a5591a2884a984183ce"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_afaf2c98348cc4a5591a2884a984183ce"></a>-C, --enpwdfiledir=DIR</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ae6b0a4366ce6473d93856ed2bb2c330d"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ae6b0a4366ce6473d93856ed2bb2c330d"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ae6b0a4366ce6473d93856ed2bb2c330d"></a>Specifies the directory where the password encrypted is located, using the AES128 encryption algorithm during the running of <strong id="b54941438214"><a name="b54941438214"></a><a name="b54941438214"></a>gs_initdb</strong>. <strong id="b107821098212"><a name="b107821098212"></a><a name="b107821098212"></a>gs_initdb</strong> decrypts the password file in this directory and performs the password complexity check on the decrypted password. The password is used as the user's password if the check passes.</p>
<div class="note" id="en-us_topic_0237152414_en-us_topic_0059778168_n96825782fffe451a8e266c4642f5c5ab"><a name="en-us_topic_0237152414_en-us_topic_0059778168_n96825782fffe451a8e266c4642f5c5ab"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_n96825782fffe451a8e266c4642f5c5ab"></a><span class="notetitle"> NOTE: </span><div class="notebody"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ue1d74eb6d6544f5a87095ffe467c3893"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ue1d74eb6d6544f5a87095ffe467c3893"></a><ul id="en-us_topic_0237152414_en-us_topic_0059778168_ue1d74eb6d6544f5a87095ffe467c3893"><li>The decrypted password file must use <strong id="b7278113821"><a name="b7278113821"></a><a name="b7278113821"></a>gs_guc</strong> to generate <strong id="b328321319219"><a name="b328321319219"></a><a name="b328321319219"></a>gs_guc encrypt -K Gauss@123 -D Dir</strong>.</li><li>If multiple <strong id="b94901616429"><a name="b94901616429"></a><a name="b94901616429"></a>-w</strong> and <strong id="b1149551616210"><a name="b1149551616210"></a><a name="b1149551616210"></a>-C</strong> parameters are specified, <strong id="b204951016423"><a name="b204951016423"></a><a name="b204951016423"></a>gs_initdb</strong> regards the last <strong id="b749515162026"><a name="b749515162026"></a><a name="b749515162026"></a>-w</strong> or <strong id="b174951016527"><a name="b174951016527"></a><a name="b174951016527"></a>-C</strong> parameter as the user's requirement (entering a plain-text password or a password encrypted using AES128).</li></ul>
</div></div>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p669277881694"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p669277881694"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p669277881694"></a>-</p>
</td>
</tr>
<tr id="row4629125315216"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a3a039c42f6cc4b9f950bcb1f0f37fcd6"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a3a039c42f6cc4b9f950bcb1f0f37fcd6"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a3a039c42f6cc4b9f950bcb1f0f37fcd6"></a>-X, --xlogdir=XLOGDIR</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a006d0d95e29748c592fdd4cd2d275db7"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a006d0d95e29748c592fdd4cd2d275db7"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a006d0d95e29748c592fdd4cd2d275db7"></a>Specifies the directory where the transaction logs are stored.</p>
<p id="en-us_topic_0237152414_en-us_topic_0059778168_aa7f9aced4b4f49529a06901c7baa05ba"><a name="en-us_topic_0237152414_en-us_topic_0059778168_aa7f9aced4b4f49529a06901c7baa05ba"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_aa7f9aced4b4f49529a06901c7baa05ba"></a>The directory must be a directory where an openGauss user has the read and write permissions.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ad84c6e72a8014e17b4fc637e4744fcb0"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ad84c6e72a8014e17b4fc637e4744fcb0"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ad84c6e72a8014e17b4fc637e4744fcb0"></a>The value must be an absolute path.</p>
</td>
</tr>
<tr id="row18628253172119"><td class="cellrowborder" valign="top" width="23.76%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_adb3b9f7b61294101b39eedd21feef973"><a name="en-us_topic_0237152414_en-us_topic_0059778168_adb3b9f7b61294101b39eedd21feef973"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_adb3b9f7b61294101b39eedd21feef973"></a>-S, --security</p>
</td>
<td class="cellrowborder" valign="top" width="32.6%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a941fc47a24bf41ed93d91a2fc8fe28c9"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a941fc47a24bf41ed93d91a2fc8fe28c9"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a941fc47a24bf41ed93d91a2fc8fe28c9"></a>Initializes a database in a secure mode.</p>
</td>
<td class="cellrowborder" valign="top" width="43.64%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a6ef9874c80974ce3953e2aa1db0a0efb"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a6ef9874c80974ce3953e2aa1db0a0efb"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a6ef9874c80974ce3953e2aa1db0a0efb"></a>After the database is initialized using <strong id="b0429332422"><a name="b0429332422"></a><a name="b0429332422"></a>-S</strong>, the created database user permissions are restricted, and the <strong id="b12435183210217"><a name="b12435183210217"></a><a name="b12435183210217"></a>public schema</strong> permission cannot be used any more by default.</p>
</td>
</tr>
</tbody>
</table>




**Table  2**  Uncommon parameters

<a name="en-us_topic_0237152414_en-us_topic_0059778168_t2f464cb1775044808eceb29e25d6d37f"></a>
<table><thead align="left"><tr id="en-us_topic_0237152414_en-us_topic_0059778168_rcdce44e401504e7fbc3d46375a8bdfcf"><th class="cellrowborder" valign="top" width="15.939999999999998%" id="mcps1.2.4.1.1"><p id="en-us_topic_0237152414_en-us_topic_0059778168_a56f44abb258a4286be24bb7b628afece"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a56f44abb258a4286be24bb7b628afece"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a56f44abb258a4286be24bb7b628afece"></a>Parameter</p>
</th>
<th class="cellrowborder" valign="top" width="60.940000000000005%" id="mcps1.2.4.1.2"><p id="en-us_topic_0237152414_en-us_topic_0059778168_a08ee6c1b36b24ef98584c3fa2926fe19"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a08ee6c1b36b24ef98584c3fa2926fe19"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a08ee6c1b36b24ef98584c3fa2926fe19"></a>Description</p>
</th>
<th class="cellrowborder" valign="top" width="23.119999999999997%" id="mcps1.2.4.1.3"><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p510352201451"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p510352201451"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p510352201451"></a>Value Range</p>
</th>
</tr>
</thead>
<tbody><tr id="en-us_topic_0237152414_en-us_topic_0059778168_r20e8aa016e00498e8cdd78cb91ae1259"><td class="cellrowborder" valign="top" width="15.939999999999998%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a08696e88c5504abeb747084aa8a014e5"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a08696e88c5504abeb747084aa8a014e5"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a08696e88c5504abeb747084aa8a014e5"></a>-d, --debug</p>
</td>
<td class="cellrowborder" valign="top" width="60.940000000000005%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a20acb965470a4011b6a112fba8fdd554"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a20acb965470a4011b6a112fba8fdd554"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a20acb965470a4011b6a112fba8fdd554"></a>Prints debugging output from the bootstrap backend. The bootstrap backend is used by <strong id="b8923154011218"><a name="b8923154011218"></a><a name="b8923154011218"></a>gs_initdb</strong> to create system catalogs.</p>
</td>
<td class="cellrowborder" valign="top" width="23.119999999999997%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_aab224892323541ebb37429a325f72ae3"><a name="en-us_topic_0237152414_en-us_topic_0059778168_aab224892323541ebb37429a325f72ae3"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_aab224892323541ebb37429a325f72ae3"></a>-</p>
</td>
</tr>
<tr id="en-us_topic_0237152414_en-us_topic_0059778168_rb3cc8dfb4ef147789b26c7bedc388ff1"><td class="cellrowborder" valign="top" width="15.939999999999998%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p754280414042"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p754280414042"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p754280414042"></a>-L DIRECTORY</p>
</td>
<td class="cellrowborder" valign="top" width="60.940000000000005%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p698742114042"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p698742114042"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p698742114042"></a>Specifies the input file path where the database is initialized using <strong id="b23452423217"><a name="b23452423217"></a><a name="b23452423217"></a>gs_initdb</strong>. This is unnecessary. You will be told if you need to specify their location explicitly. This parameter is used to create a database with specified configuration information. You are advised to copy all subdirectories and files related to startup in the <strong id="b1754713514219"><a name="b1754713514219"></a><a name="b1754713514219"></a>share/postgresql</strong> directory to avoid impact of other factors.</p>
</td>
<td class="cellrowborder" valign="top" width="23.119999999999997%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a1a814991f59347708f713aed46a2de69"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a1a814991f59347708f713aed46a2de69"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a1a814991f59347708f713aed46a2de69"></a>Path of input files required by the initialized database.</p>
</td>
</tr>
<tr id="en-us_topic_0237152414_en-us_topic_0059778168_r9fd94d4eea5a4fffbe84f595c06ce3e9"><td class="cellrowborder" valign="top" width="15.939999999999998%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_af0f24cb7bf5b4f1fa1ba5f81fdf53fa2"><a name="en-us_topic_0237152414_en-us_topic_0059778168_af0f24cb7bf5b4f1fa1ba5f81fdf53fa2"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_af0f24cb7bf5b4f1fa1ba5f81fdf53fa2"></a>-n, --noclean</p>
</td>
<td class="cellrowborder" valign="top" width="60.940000000000005%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a6e425272494742d5a19f77d99bf796b2"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a6e425272494742d5a19f77d99bf796b2"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a6e425272494742d5a19f77d99bf796b2"></a>If this parameter is not specified and <strong id="b18268568220"><a name="b18268568220"></a><a name="b18268568220"></a>gs_initdb</strong> determines that an error prevents it from creating a database, it removes any files it might have created before discovering that it cannot finish the job. This option inhibits tidying-up and is useful for debugging.</p>
</td>
<td class="cellrowborder" valign="top" width="23.119999999999997%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a6812e35ed982480493c851dadf1d4e2e"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a6812e35ed982480493c851dadf1d4e2e"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a6812e35ed982480493c851dadf1d4e2e"></a>-</p>
</td>
</tr>
<tr id="en-us_topic_0237152414_en-us_topic_0059778168_ra211d54b4ac3434eb653905797bace22"><td class="cellrowborder" valign="top" width="15.939999999999998%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_ab4b1d602d8e64fa7935cc69bdefd63dc"><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab4b1d602d8e64fa7935cc69bdefd63dc"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_ab4b1d602d8e64fa7935cc69bdefd63dc"></a>-s, --show</p>
</td>
<td class="cellrowborder" valign="top" width="60.940000000000005%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a5011243f8d344adc983426a76fe5c054"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a5011243f8d344adc983426a76fe5c054"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a5011243f8d344adc983426a76fe5c054"></a>Displays internal settings.</p>
</td>
<td class="cellrowborder" valign="top" width="23.119999999999997%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_adb419280469547c786f06333a1d3f20a"><a name="en-us_topic_0237152414_en-us_topic_0059778168_adb419280469547c786f06333a1d3f20a"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_adb419280469547c786f06333a1d3f20a"></a>-</p>
</td>
</tr>
<tr id="en-us_topic_0237152414_en-us_topic_0059778168_re847d900ac2c4d18b1a81472b956cc0d"><td class="cellrowborder" valign="top" width="15.939999999999998%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p938216814042"><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p938216814042"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_en-us_topic_0058968084_p938216814042"></a>-V, --version</p>
</td>
<td class="cellrowborder" valign="top" width="60.940000000000005%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a9f3d5f19499c4294915ffd31b51d521a"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a9f3d5f19499c4294915ffd31b51d521a"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a9f3d5f19499c4294915ffd31b51d521a"></a>Prints the <strong id="b196296451632"><a name="b196296451632"></a><a name="b196296451632"></a>gs_initdb</strong> version and exits.</p>
</td>
<td class="cellrowborder" valign="top" width="23.119999999999997%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_a447b6665afb94838805a0fb78226994a"><a name="en-us_topic_0237152414_en-us_topic_0059778168_a447b6665afb94838805a0fb78226994a"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_a447b6665afb94838805a0fb78226994a"></a>-</p>
</td>
</tr>
<tr id="en-us_topic_0237152414_en-us_topic_0059778168_r61b79064dcd94ee5af8f108de8b4b284"><td class="cellrowborder" valign="top" width="15.939999999999998%" headers="mcps1.2.4.1.1 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_af7a8724ee2da49998933039cbd96bf6d"><a name="en-us_topic_0237152414_en-us_topic_0059778168_af7a8724ee2da49998933039cbd96bf6d"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_af7a8724ee2da49998933039cbd96bf6d"></a>-?, --help</p>
</td>
<td class="cellrowborder" valign="top" width="60.940000000000005%" headers="mcps1.2.4.1.2 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_afe016a5c969f40588960864b14bef101"><a name="en-us_topic_0237152414_en-us_topic_0059778168_afe016a5c969f40588960864b14bef101"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_afe016a5c969f40588960864b14bef101"></a>Displays help about <strong id="b134691471316"><a name="b134691471316"></a><a name="b134691471316"></a>gs_initdb</strong> command line parameters and exits.</p>
</td>
<td class="cellrowborder" valign="top" width="23.119999999999997%" headers="mcps1.2.4.1.3 "><p id="en-us_topic_0237152414_en-us_topic_0059778168_acd137c3708c44ec7b5aa19addfc1b627"><a name="en-us_topic_0237152414_en-us_topic_0059778168_acd137c3708c44ec7b5aa19addfc1b627"></a><a name="en-us_topic_0237152414_en-us_topic_0059778168_acd137c3708c44ec7b5aa19addfc1b627"></a>-</p>
</td>
</tr>
</tbody>
</table>

