# Obtaining Help Information<a name="EN-US_TOPIC_0303986186"></a>

Before starting the tuning program, run the following command to obtain help information:

```
Source code mode: python main.py --help
```

The command output is as follows:

```
usage:
    python main.py start [--role {{agent,collector,monitor}}] # start local service.
    python main.py stop [--role {{agent,collector,monitor}}] # stop local service.
    python main.py start [--user USER] [--host HOST] [--project-path PROJECT_PATH] [--role {{agent,collector,monitor}}]
    # start the remote service.
    python main.py stop [--user USER] [--host HOST] [--project-path PROJECT_PATH] [--role {{agent,collector,
    monitor}}] # stop the remote service.
    python main.py deploy [--user USER] [--host HOST] [--project-path PROJECT_PATH] # deploy project in remote host.
    python main.py diagnosis [--query] [--start_time] [--finish_time] # rca for slow SQL.
    python main.py show_metrics # display all monitored metrics(can only be executed on 'detector' machine).
    python main.py forecast [--metric-name METRIC_NAME] [--period] [--freq]
     [--forecast-method {{auto_arima, fbprophet}}] [--save-path SAVE_PATH] # forecast future trend of
     metric(can only be executed on 'detector' machine).

Anomaly-detection: a time series forecast and anomaly detection tool.

positional arguments:
  {start,stop,deploy,show_metrics,forecast,diagnosis}

optional arguments:
  -h, --help            show this help message and exit
  --user USER           User of remote server.
  --host HOST           IP of remote server.
  --project-path PROJECT_PATH
                        Project location in remote server.
  --role {agent,collector,monitor}
                        Run as 'agent', 'collector', 'monitor'. Notes: ensure
                        the normal operation of the openGauss in agent.
  --metric-name METRIC_NAME
                        Metric name to be predicted, if this parameter is not provided, all metric in database will be    predicted.         .
.
  --query QUERY         target sql for RCA.
                      
  --start_time START_TIME
                        start time of query
  --finish_time FINISH_TIME
                        finish time of query
  --period PERIOD       Forecast periods of metric, it should be integernotes:
                        the specific value should be determined to the
                        training data. If this parameter is not provided, the
                        default value '100S' will be used.
  --freq FREQ           forecast gap, time unit: S: Second, M: Minute, H:
                        Hour, D: Day, W: Week.
  --forecast-method FORECAST_METHOD
                        Forecast method, default method is 'auto_arima',if
                        want to use 'fbprophet', you should install fbprophet
                        first.
  --save-path SAVE_PATH
                        Save the results to this path using csv format, if
                        this parameter is not provided, the result will not be
                        saved.
  -v, --version         show program's version number and exit

epilog:
     the 'a-detection.conf' and 'metric_task.conf' will be read when the program is running,
     the location of them is:
     a-detection.conf: /openGauss-server/src/gausskernel/dbmind/tools/anomaly_detection/a-detection.conf.
     metric_config: /openGauss-server/src/gausskernel/dbmind/tools/anomaly_detection/task/metric_task.conf.
```

