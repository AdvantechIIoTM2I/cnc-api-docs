# 3.3.2 MAlarmOccurrenceRank

## Information

* Get device’s ranking top number information from alarm occurrence of each code.
* Support single / multiple devices


## Format

* ### Request

  ```
  fns.MAlarmOccurrenceRank("path", "device_id", "topN", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | topN | String | Top "N" of occurrence rank | 5 |
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
  | Occurrence | Int | The alarm code occurrence count | 10000.11 |  
  | AlarmMsg | String | The alarm message of alarm code list (English). | "100 PARAMETER WRITE ENABLE" |
  | AlarmMsgTC | String | The alarm message of alarm code (Traditional Chinese). | "100 可寫入參數" |
  

* ### Example  
    1. List Top 10 Alarm code by Occurrence   
        - Query   
        ``` sql
        select * from fns.MAlarmOccurrenceRank("$Group/$Factory", "", "10", "$from", "$to") 
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Table
        - Panel Screenshot      
            ![](/images/3.3.2-MAlarmOccurrenceRank-table.jpg)
        - Return Value Example    
            ``` json
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
                            "sqltype": "int", 
                            "text": "Occurrence", 
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
                            26, 
                            "383 n AXIS : PULSE MISS (EXT)", 
                            "383 n\u8ef8:\u76f8\u4f4d\u5931\u8aa4(EXT)"
                        ], 
                        [
                            2, 
                            "1081", 
                            8, 
                            "", 
                            ""
                        ], 
                        [
                            3, 
                            "000", 
                            3, 
                            "000 PLEASE TURN OFF POWER !", 
                            "000 \u8acb\u95dc\u96fb\u518d\u958b"
                        ], 
                        [
                            4, 
                            "385", 
                            2, 
                            "385 n AXIS : SERIAL DATA ERROR (EXT)", 
                            "385 n\u8ef8:\u4e32\u5217\u8cc7\u6599\u8aa4\u5dee(EXT)"
                        ], 
                        [
                            5, 
                            "071", 
                            1, 
                            "071 DATA NOT FOUND", 
                            "071 \u627e\u4e0d\u5230\u5c0b\u627e\u7684\u8cc7\u6599"
                        ], 
                        [
                            6, 
                            "300", 
                            1, 
                            "300 APC ALARM:nth-AXIS ORIGIN RETURN", 
                            "300 \u7b2cn\u8ef8\u539f\u9ede\u5fa9\u6b78"
                        ], 
                        [
                            7, 
                            "1065", 
                            1, 
                            "NONE TF COMMAND!", 
                            "NONE TF COMMAND!"
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```

    2. List Top 10 of Alarm code by Occurrence in Group Bar Chart    
        - Query   
        ``` sql
        select 'N' as metric, Occurrence, Code from fns.MAlarmOccurrenceRank("$Group/$Factory", "", "10", "$from", "$to") 
        ```
        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Group Bar Chart
        - Panel Screenshot   
            ![](/images/3.3.2-MAlarmOccurrenceRank-bar.jpg)
        - Return Value Example    
            ``` json
            [
                {
                    "datapoints": [
                        [
                            26, 
                            "383"
                        ], 
                        [
                            8, 
                            "1081"
                        ], 
                        [
                            3, 
                            "000"
                        ], 
                        [
                            2, 
                            "091"
                        ], 
                        [
                            2, 
                            "385"
                        ], 
                        [
                            1, 
                            "071"
                        ], 
                        [
                            1, 
                            "300"
                        ], 
                        [
                            1, 
                            "1065"
                        ]
                    ], 
                    "target": "N"
                }
            ]

            ```
