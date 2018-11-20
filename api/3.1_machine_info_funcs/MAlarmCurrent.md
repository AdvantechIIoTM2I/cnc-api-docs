# 3.1.6 MAlarmCurrent

## Information

* List the ongoing Alarms of each device within query time range
* Support one / multiple devices


## Format

* ### Request

  ```
  fns.MAlarmCurrent("path", "device_id", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "device_id"
    - 'device_id' can be empty string if you want to query all devices under the specified 'path'
  

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | DevID | String | Device ID | MC-29 |
  | AlarmCode | String | Alarm Code | "100" |
  | AlarmMsg | String | The alarm message of alarm code list (English). | "100 PARAMETER WRITE ENABLE" |
  | AlarmMsgTC | String | The alarm message of alarm code (Traditional Chinese). | "100 可寫入參數" |
  | Ts | Datetime | Timestamp of the data | 1539679347445 |
  
* ### Example  
    1. Query latest records within query time range
        - Query   
        ``` sql
        select * from fns.MEventList("$Group/$Factory/$Category", "",  "10", "$from", "$to") 
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Table
        - Panel Screenshot      
            ![](/images/3.1.6-MAlarmCurrent.jpg)

        - Return Value Example    
            ``` json
            [
                {
                    "columns": [
                        {
                            "sqltype": "str", 
                            "text": "DevID", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "str", 
                            "text": "AlarmCode", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "str", 
                            "text": "AlarmMsg", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "str", 
                            "text": "AlarmMsgTC", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "datetime", 
                            "text": "Ts", 
                            "type": "time"
                        }
                    ], 
                    "rows": [
                        [
                            "MC-33", 
                            "071", 
                            "071 DATA NOT FOUND", 
                            "071 \u627e\u4e0d\u5230\u5c0b\u627e\u7684\u8cc7\u6599", 
                            1542609229503
                        ]
                    ], 
                    "type": "table"
                }
            ]
            ```