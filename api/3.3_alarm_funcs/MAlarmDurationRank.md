# 3.3.3 MAlarmDurationRank


## Information

* Get device’s ranking top number information from alarm duration of each code.
* Support single / multiple devices


## Format

* ### Request

  ```
  fns.MAlarmDurationRank("path", "device_id", "topN", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | topN | String | Top "N" of duration rank | 5 |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "device ID"
    - 'device_id' can be empty string if you want to query all devices under the specified 'path'
  

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | No | Int | Rank number | 1 |
  | AlarmCode | String | Alarm Code | "100" |
  | Duration | float | The alarm code duration count (second) | 8923.11 |  
  | AlarmMsg | String | The alarm message of alarm code list (English). | "100 PARAMETER WRITE ENABLE" |
  | AlarmMsgTC | String | The alarm message of alarm code (Traditional Chinese). | "100 可寫入參數" |
  

* ### Example  
    1. List Top 10 Alarm code by Duration   
        - Query   
        ``` select * from fns.MAlarmDurationRank("$Group/$Factory", "", "10", "$from", "$to") ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Table
        - Panel Screenshot      
            ![](/images/3.3.3-MAlarmDurationRank-table.jpg)
        - Return Value Example    
            ```
            [
                {
                    "columns": [
                        {
                            "sqltype": "int", 
                            "text": "No", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "str", 
                            "text": "Code", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "Duration", 
                            "type": "number"
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
                        }
                    ], 
                    "rows": [
                        [
                            1, 
                            "383", 
                            8923.11, 
                            "383 n AXIS : PULSE MISS (EXT)", 
                            "383 n\u8ef8:\u76f8\u4f4d\u5931\u8aa4(EXT)"
                        ], 
                        [
                            2, 
                            "1081", 
                            372.27799999999996, 
                            "", 
                            ""
                        ], 
                        [
                            3, 
                            "300", 
                            100.112, 
                            "300 APC ALARM:nth-AXIS ORIGIN RETURN", 
                            "300 \u7b2cn\u8ef8\u539f\u9ede\u5fa9\u6b78"
                        ], 
                        [
                            4, 
                            "000", 
                            80.09299999999999, 
                            "000 PLEASE TURN OFF POWER !", 
                            "000 \u8acb\u95dc\u96fb\u518d\u958b"
                        ], 
                        [
                            5, 
                            "385", 
                            80.092, 
                            "385 n AXIS : SERIAL DATA ERROR (EXT)", 
                            "385 n\u8ef8:\u4e32\u5217\u8cc7\u6599\u8aa4\u5dee(EXT)"
                        ], 
                        [
                            6, 
                            "091", 
                            20.026, 
                            "091 REFERENCE RETURN INCOMPLETE", 
                            "091"
                        ], 
                        [
                            7, 
                            "1065", 
                            10.014, 
                            "NONE TF COMMAND!", 
                            "NONE TF COMMAND!"
                        ], 
                        [
                            8, 
                            "071", 
                            10.011, 
                            "071 DATA NOT FOUND", 
                            "071 \u627e\u4e0d\u5230\u5c0b\u627e\u7684\u8cc7\u6599"
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```

    2. List Top 10 of Alarm code by Duration in Group Bar Chart    
        - Query   
        ``` 
        select 'N' as metric, Duration, Code from fns.MAlarmDurationRank("$Group/$Factory", "", "10", "$from", "$to") 
        ```
        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Group Bar Chart
        - Panel Screenshot   
            ![](/images/3.3.3-MAlarmDurationRank-bar.jpg)
        - Return Value Example    
            ```
            [
                {
                    "datapoints": [
                        [
                            8923.11, 
                            "383"
                        ], 
                        [
                            372.27799999999996, 
                            "1081"
                        ], 
                        [
                            100.112, 
                            "300"
                        ], 
                        [
                            80.09299999999999, 
                            "000"
                        ], 
                        [
                            80.092, 
                            "385"
                        ], 
                        [
                            20.026, 
                            "091"
                        ], 
                        [
                            10.014, 
                            "1065"
                        ], 
                        [
                            10.011, 
                            "071"
                        ]
                    ], 
                    "target": "N"
                }
            ]

            ```