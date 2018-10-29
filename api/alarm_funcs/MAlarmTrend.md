# 3.3.4 MAlarmTrend

## Information

* Return Devices’ daily alarm count of each alarm level within query time range
* Support one or multiple devices

## Format

* ### Request

  ```
  fns.MAlarmTrend("path", "device_id",  "level", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | level | String | String of alarm code level<br>"0" = Critical level<br>"1" = Warning level | "0" |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "device_id"
    - 'device_id' can be empty string if you want to query all devices under the specified 'path'
  

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | Level | string | alarm code level | "0" |
  | Ts | Datetime | Timestamp of the data | 1539679347445 |
  | AlarmLevelCount | int | Number of alarm  | 20 |

* ### Example  
    1. Query daily alarm count of 2 kinds of alarm levels
        - Query   
            * Use 2 queries for this panel    
            * Note:   
                * Use "select 'xxxx' as metric" to specify the Display Legend Name of these data 
        ```    
        select 'Critical' as metric, AlarmLevelCount, Ts  from fns.MAlarmTrend("$Group/$Factory/$Category", "", "0", "$from", "$to")   
        select 'Warning' as metric, AlarmLevelCount, Ts  from fns.MAlarmTrend("$Group/$Factory/$Category", "", "1", "$from", "$to")   
        ```   

        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Graph
        - Panel Screenshot      
            ![](/images/3.3.4-MAlarmTrend-graph.jpg)

        - Return Value Example    
            ```
            [
                {
                    "datapoints": [
                        [
                            3, 
                            1539792000000
                        ], 
                        [
                            5, 
                            1539878400000
                        ], 
                        [
                            0, 
                            1539964800000
                        ], 
                        [
                            0, 
                            1540051200000
                        ], 
                        [
                            4, 
                            1540137600000
                        ], 
                        [
                            2, 
                            1540224000000
                        ], 
                        [
                            2, 
                            1540310400000
                        ], 
                        [
                            2, 
                            1540396800000
                        ]
                    ], 
                    "target": "Critical"
                }, 
                {
                    "datapoints": [
                        [
                            0, 
                            1539792000000
                        ], 
                        [
                            0, 
                            1539878400000
                        ], 
                        [
                            0, 
                            1539964800000
                        ], 
                        [
                            0, 
                            1540051200000
                        ], 
                        [
                            0, 
                            1540137600000
                        ], 
                        [
                            0, 
                            1540224000000
                        ], 
                        [
                            0, 
                            1540310400000
                        ], 
                        [
                            0, 
                            1540396800000
                        ]
                    ], 
                    "target": "Warning"
                }
            ]


            ```