# 3.3.5 MAlarmInfo

## Information

* Computes device’s availability information, include
    * Availability
    * Run/Down/Idle/Off time
    * OFF count and  Run+Idle+Down total time
* Need to specify the Query time range (from $from to $to)
* Support one / multiple devices

## Format

* ### Request

  ```
  fns.MAvail('path', '<device ID>', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | device ID | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "device ID"
    - 'device ID' can be empty string if you want to query all devices under the specified 'path'
  

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | OffTime | float | Device's total Off time(sec.) within query time range | 100.11 |
  | RunTime | float | Device's total Run time(sec.) within query time range | 60000.11 |
  | IdleTime | float | Device's total Idle time(sec.) within query time range | 10000.11 |  
  | DownTime | float | Device's total Down time(sec.) within query time range | 50.11 |
  | Total | float | RunTime + IdleTime + DownTime (sec.) | 70050.33 |
  | DownCount | int | Number of Down state within query time range | 2 |
  | Availability | float | Device's Availability within query time range | 90.1 |
  

* ### Example  
    1. Query Availability of one device   
        - Query   
        ``` select Availability from fns.MAvail('Advantech/Taipei','{MC-31}', '$from', '$to') ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Singlestat
        - Panel Screenshot      
            ![](/images/3.2.1-MAvail-Availability.jpg)
        - Return Value Example    
            ```
            [
                {
                    "columns": [
                        {
                            "sqltype": "float", 
                            "text": "Availability", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            54.55
                        ]
                    ], 
                    "type": "table"
                }
            ]
            ```

    2. Multiple device's Availability Analysis   
        - Query   
            * Use 4 queries for this panel   
        ``` 
        select 'Run' as metric, RunTime from fns.MAvail("Advantech/Taipei","", "$from", "$to") 
        select 'Idle' as metric, IdleTime from fns.MAvail("Advantech/Taipei","", "$from", "$to")
        select 'Down' as metric, DownTime from fns.MAvail("Advantech/Taipei","", "$from", "$to")
        select 'Off' as metric, OffTime from fns.MAvail("Advantech/Taipei","", "$from", "$to")
        ```
        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Pie Chart
        - Panel Screenshot   
            ![](/images/3.2.1-MAvail-Pie.jpg)
        - Return Value Example    
            ```
            [
                {
                    "datapoints": [
                        [
                            219076.90199999997, 
                            219076.90199999997
                        ]
                    ], 
                    "target": "Run"
                }, 
                {
                    "datapoints": [
                        [
                            106124.7910000001, 
                            106124.7910000001
                        ]
                    ], 
                    "target": "Idle"
                }, 
                {
                    "datapoints": [
                        [
                            10.018, 
                            10.018
                        ]
                    ], 
                    "target": "Down"
                }, 
                {
                    "datapoints": [
                        [
                            252653.89900000003, 
                            252653.89900000003
                        ]
                    ], 
                    "target": "Off"
                }
            ]       
            ```
