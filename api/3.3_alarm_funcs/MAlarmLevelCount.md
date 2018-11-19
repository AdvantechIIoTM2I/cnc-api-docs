# 3.3.5 MAlarmLevelCount

## Information

* Return Devices’ Alarm code occurrence of level.
* Support one or multiple devices

## Format

* ### Request

  ```
  fns.MAlarmLevelCount("path", "device_id",  "level", "$from", "$to")
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
  | Level | string | Alarm code level | "0" |
  | Occurrence | int | The alarm code occurrence count in time range. | 20 |
 
* ### Example  
    1. Query Alarm occurrence of Alarm Level "0" within time range
        - Query   
        ``` 
        select Occurrence from fns.MAlarmLevelCount("$Group/$Factory/$Category", "", "0",  "$from", "$to")
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Radar Chart
        - Panel Screenshot      
            ![](/images/3.3.5-MAlarmLevelCount-SingleStat.jpg)

        - Return Value Example    
            ```
            [
                {
                    "columns": [
                        {
                            "sqltype": "int", 
                            "text": "Occurrence", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            11
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```