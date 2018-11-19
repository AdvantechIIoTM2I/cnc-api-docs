# 3.3.6 MAlarmLatest

## Information

* List latest "N" Alarms within query time range
* Support one / multiple devices


## Format

* ### Request

  ```
  fns.MAlarmLatest("path", "device_id",  "num_of_record", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | num_of_record | String | Number of alarm records that you want to display | "10" |
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
    1. Query latest 10 alarm records within query time range
        - Query   
        ``` 
        select * from fns.MAlarmLatest("$Group/$Factory/$Category", "",  "10", "$from", "$to") 
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Table
        - Panel Screenshot      
            ![](/images/3.3.6-MAlarmLatest-Table.jpg)

        - Return Value Example    
            ```
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
                            "FM-04", 
                            "1095", 
                            "NO EXCHANGE TABLE", 
                            "NO EXCHANGE TABLE", 
                            1540516568525
                        ], 
                        [
                            "FM-04", 
                            "1058", 
                            "ATC DOOR NOT CLOSE!", 
                            "ATC DOOR NOT CLOSE!", 
                            1540447202947
                        ], 
                        [
                            "FM-04", 
                            "1058", 
                            "ATC DOOR NOT CLOSE!", 
                            "ATC DOOR NOT CLOSE!", 
                            1540447090714
                        ], 
                        [
                            "FM-04", 
                            "1016", 
                            "SP TOOL (D440) SETTING ERROR!", 
                            "SP TOOL (D440) SETTING ERROR!", 
                            1540342936705
                        ], 
                        [
                            "FM-04", 
                            "1016", 
                            "SP TOOL (D440) SETTING ERROR!", 
                            "SP TOOL (D440) SETTING ERROR!", 
                            1540342140337
                        ], 
                        [
                            "FM-04", 
                            "1020", 
                            "OIL MATIC ! SPINDLE !", 
                            "OIL MATIC ! SPINDLE !", 
                            1540300318297
                        ], 
                        [
                            "FM-04", 
                            "1020", 
                            "OIL MATIC ! SPINDLE !", 
                            "OIL MATIC ! SPINDLE !", 
                            1540299078024
                        ], 
                        [
                            "FM-04", 
                            "1094", 
                            "CTS INVENTER ERROR!", 
                            "CTS INVENTER ERROR!", 
                            1540185398010
                        ], 
                        [
                            "MC-35", 
                            "1065", 
                            "NONE TF COMMAND!", 
                            "NONE TF COMMAND!", 
                            1540168216175
                        ], 
                        [
                            "FM-04", 
                            "1094", 
                            "CTS INVENTER ERROR!", 
                            "CTS INVENTER ERROR!", 
                            1540167942617
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```