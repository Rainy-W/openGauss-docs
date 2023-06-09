# 启停openGauss<a name="ZH-CN_TOPIC_0289897005"></a>

## 启动openGauss<a name="zh-cn_topic_0283140572_zh-cn_topic_0237088789_zh-cn_topic_0059777680_se84dd72782a34e9b8b1fb962d2842afa"></a>

1.  以操作系统用户omm登录数据库主节点。
2.  使用以下命令启动openGauss。

    ```
    gs_ctl start -D /opt/data
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >如果提示找不到gs\_ctl，请检查是否source过环境变量文件（默认是\~/.bashrc），若不想source环境变量文件也可以手动切换到安装路径下执行该命令。


## 停止openGauss<a name="zh-cn_topic_0283140572_zh-cn_topic_0237088789_section785041010214"></a>

1.  以操作系统用户omm登录数据库主节点。
2.  使用以下命令停止openGauss。

    ```
    gs_ctl stop -D /opt/data
    ```

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >启停节点操作请参见《工具与命令参考》中“系统内部调用的工具 \> gs\_ctl”章节。


## 示例<a name="zh-cn_topic_0283140572_zh-cn_topic_0237088789_zh-cn_topic_0059777680_s8c57591e1a444d5ea91a783a1a2b74c5"></a>

启动openGauss：

```
gs_ctl start -D /opt/data
[2022-01-08 09:11:24.666][4179575][][gs_ctl]: waiting for server to start...
.0 LOG:  [Alarm Module]can not read GAUSS_WARNING_TYPE env.

0 LOG:  [Alarm Module]Host Name: pekphispra59074

0 LOG:  [Alarm Module]Host IP: 192.168.6.247

0 LOG:  [Alarm Module]Get ENV GS_CLUSTER_NAME failed!

0 LOG:  [Alarm Module]Invalid data in AlarmItem file! Read alarm English name failed! line: 55

0 WARNING:  failed to open feature control file, please check whether it exists: FileName=gaussdb.version, Errno=2, Errmessage=No such file or directory.
0 WARNING:  failed to parse feature control file: gaussdb.version.
0 WARNING:  Failed to load the product control file, so gaussdb cannot distinguish product version.
.....The core dump path is an invalid directory
2022-01-08 09:11:30.381 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  when starting as multi_standby mode, we couldn't support data replicaton.
2022-01-08 09:11:30.381 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  [Alarm Module]can not read GAUSS_WARNING_TYPE env.

2022-01-08 09:11:30.381 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  [Alarm Module]Host Name: pekphispra59074

2022-01-08 09:11:30.454 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  [Alarm Module]Host IP: 192.168.6.247

2022-01-08 09:11:30.454 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  [Alarm Module]Get ENV GS_CLUSTER_NAME failed!

2022-01-08 09:11:30.455 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  [Alarm Module]Invalid data in AlarmItem file! Read alarm English name failed! line: 55

2022-01-08 09:11:30.459 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  loaded library "security_plugin"
2022-01-08 09:11:30.459 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] WARNING:  could not create any HA TCP/IP sockets
2022-01-08 09:11:30.459 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] WARNING:  could not create any HA TCP/IP sockets
2022-01-08 09:11:30.461 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] WARNING:  No explicit IP is configured for listen_addresses GUC.
2022-01-08 09:11:30.461 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  InitNuma numaNodeNum: 1 numa_distribute_mode: none inheritThreadPool: 0.
2022-01-08 09:11:30.462 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  reserved memory for backend threads is: 220 MB
2022-01-08 09:11:30.462 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  reserved memory for WAL buffers is: 128 MB
2022-01-08 09:11:30.462 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  Set max backend reserve memory is: 348 MB, max dynamic memory is: 11038 MB
2022-01-08 09:11:30.462 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  shared memory 389 Mbytes, memory context 11386 Mbytes, max process memory 12288 Mbytes
2022-01-08 09:11:30.526 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [CACHE] LOG:  set data cache  size(402653184)
2022-01-08 09:11:30.576 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [CACHE] LOG:  set metadata cache  size(134217728)
2022-01-08 09:11:30.612 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [SEGMENT_PAGE] LOG:  Segment-page constants: DF_MAP_SIZE: 8156, DF_MAP_BIT_CNT: 65248, DF_MAP_GROUP_EXTENTS: 4175872, IPBLOCK_SIZE: 8168, EXTENTS_PER_IPBLOCK: 1021, IPBLOCK_GROUP_SIZE: 4090, BMT_HEADER_LEVEL0_TOTAL_PAGES: 8323072, BktMapEntryNumberPerBlock: 2038, BktMapBlockNumber: 25, BktBitMaxMapCnt: 512
2022-01-08 09:11:30.641 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  gaussdb: fsync file "/opt/data/gaussdb.state.temp" success
2022-01-08 09:11:30.641 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  create gaussdb state file success: db state(STARTING_STATE), server mode(Normal)
2022-01-08 09:11:30.723 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  max_safe_fds = 979, usable_fds = 1000, already_open = 11
The core dump path is an invalid directory
2022-01-08 09:11:30.727 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  the configure file /opt/install/etc/gscgroup_xwj.cfg doesn't exist or the size of configure file has changed. Please create it by root user!
2022-01-08 09:11:30.727 [unknown] [unknown] localhost 281472877080592 0[0:0#0]  0 [BACKEND] LOG:  Failed to parse cgroup config file.
.
[2022-01-08 09:11:31.764][4179575][][gs_ctl]:  done
[2022-01-08 09:11:31.764][4179575][][gs_ctl]: server started (/opt/data)

```

停止openGauss：

```
gs_ctl stop -D /opt/data
[2022-01-08 09:21:01.284][4183642][][gs_ctl]: gs_ctl stopped ,datadir is /opt/data
waiting for server to shut down......... done
server stopped
```

## 错误排查<a name="zh-cn_topic_0283140572_zh-cn_topic_0237088789_zh-cn_topic_0059777680_se86cdadb17ce4b5fbec281adaf1ccc92"></a>

如果启动openGauss或者停止openGauss服务失败，请根据日志文件中的日志信息排查错误，参见[日志参考](日志参考.md)。

