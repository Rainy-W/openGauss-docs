# gs\_backup<a name="EN-US_TOPIC_0249632295"></a>

## Background<a name="en-us_topic_0237152406_en-us_topic_0059777806_section48401199395"></a>

After openGauss is deployed, problems and exceptions may occur during database running.  **gs\_backup**  is provided by openGauss to back up openGauss, restore important data, and display help and version information.

## Prerequisites<a name="en-us_topic_0237152406_en-us_topic_0059777806_s9649938409774ccdbc6993a90ccb777a"></a>

-   The openGauss database can be connected.
-   There are backup files in the backup directory for each node when the restoration is performed. If the backup file of a node is missing, copy a backup file from other nodes \(for binary files, the node name in the file name needs to be changed\).
-   Log in to the OS as the OS user  **omm**  to run the  **gs\_backup**  command.

## Syntax<a name="en-us_topic_0237152406_en-us_topic_0059777806_sa0c0a7aa3d4042fd81017d22ca1e8cac"></a>

-   Back up the database host.

    ```
    gs_backup -t backup --backup-dir=BACKUPDIR [-h HOSTNAME] [--parameter] [--binary] [--all] [-l LOGFILE]
    ```

-   Restore the database host.

    ```
    gs_backup -t restore --backup-dir=BACKUPDIR [-h HOSTNAME] [--parameter] [--binary] [--all] [-l LOGFILE]
    ```

-   Display help information.

    ```
    gs_backup -? | --help
    ```

-   Display version information.

    ```
    gs_backup -V | --version
    ```


## Parameter Description<a name="en-us_topic_0237152406_en-us_topic_0059777806_s2fa71feeaad041f293de868e52bb5907"></a>

The  **gs\_backup**  tool can use the following types of parameters:

-   Parameters for backing up the database host:
    -   -h

        Specifies the host name for storing the backup files

        Value range: a host name If the host name is not specified, the backup files will be distributed to openGauss.

    -   --backup-dir=BACKUPDIR

        Specifies the backup file path.

    -   --parameter

        Backs up parameter files. If  **--parameter**,  **--binary**, and  **--all**  are not specified, only parameters files are backed up.

    -   --binary

        Backs up binary files.

    -   --all

        Backs up binary files and parameter files.

    -   -l

        Specifies a log file and its storage path.

        Default value:  **$GAUSSLOG/om/gs\_backup-YYYY-MM-DD\_hhmmss.log**.


-   Parameters for restoring the database host:
    -   -h

        Specifies the name of the host to restore.

        Value range: a host name If the host is not specified, the backup files will be distributed to openGauss.

    -   --backup-dir=BACKUPDIR

        Restores the file obtaining path.

    -   --parameter

        Restores parameter files. If  **--parameter**,  **--binary**, and  **--all**  are not specified, only parameters files are restored.

    -   --binary

        Restores binary files.

    -   --all

        Restores binary files and parameter files.

    -   -l

        Specifies a log file and its storage path.

        Default value:  **$GAUSSLOG/om/gs\_backup-YYYY-MM-DD\_hhmmss.log**.


-   Other parameters:
    -   -?, --help

        Displays help information.

    -   -V, --version

        Displays version information.



## Example<a name="en-us_topic_0237152406_en-us_topic_0059777806_sdebe53579dba4bb8a7dad8e21dbcb342"></a>

-   Back up the database host.

    ```
    gs_backup -t backup --backup-dir=/opt/software/gaussdb/backup_dir -h plat1 --parameter
    Backing up openGauss.
    Parsing configuration files.
    Successfully parsed the configuration file.
    Performing remote backup.
    Remote backup succeeded.
    Successfully backed up openGauss.
    ```

-   Execute the  **gs\_backup**  script to restore the database host.

    ```
    gs_backup -t restore --backup-dir=/opt/software/gaussdb/backup_dir -h plat1 --parameter
    Restoring openGauss.
    Parsing the configuration file.
    Successfully parsed configuration files.
    Performing remote restoration.
    Remote restoration succeeded.
    Successfully restored openGauss.
    ```


