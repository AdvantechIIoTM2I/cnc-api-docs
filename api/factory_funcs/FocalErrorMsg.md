# 3.4.8 FocalErrorMsg

## Information
* Get factory's latest error message of each machine within the given time range
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the node path that you want to query.
* This API will return machine's error message within this node path.
  
## Format

* ### Request

  ```
  fns.FocalErrorMsg("path", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path | /Advantech |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | DevID | String | Device ID | MC-29 |
  | AlarmMsg | String | The alarm message of alarm code list (English). | "100 PARAMETER WRITE ENABLE" |
  | AlarmMsgTC | String | The alarm message of alarm code (Traditional Chinese). | "100 可寫入參數" |
  | Ts | Datetime | Timestamp of the data | 1539679347445 |
  
* ### Example
    1. Query the alarm message of machines within {"Advantech" Group / "Taipei" Factory}
        - Query   
        ``` 
        select * from fns.FocalErrorMsg('Advantech/Taipei', '$from', '$to')
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Datatable Panel
        - Panel Screenshot      
            ![](images/3.4.8-FocalErrorMsg.jpg)

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
                            "CTS INVENTER ERROR!", 
                            "CTS INVENTER ERROR!", 
                            1540858115860
                        ], 
                        [
                            "GR-25", 
                            "SP GEAR SHIFT ALARM!", 
                            "SP GEAR SHIFT ALARM!", 
                            1540803577001
                        ], 
                        [
                            "GR-25", 
                            "SP GEAR SHIFT ALARM!", 
                            "SP GEAR SHIFT ALARM!", 
                            1540857048718
                        ], 
                        [
                            "MC-30", 
                            "071 DATA NOT FOUND", 
                            "071 找不到尋找的資料", 
                            1540864416991
                        ], 
                        [
                            "MC-30", 
                            "071 DATA NOT FOUND", 
                            "071 找不到尋找的資料", 
                            1540864437037
                        ], 
                        [
                            "MC-36", 
                            "1561 INDEX ANGLE ERROR", 
                            "1561 INDEX角度不對", 
                            1540791270244
                        ]
                    ], 
                    "type": "table"
                }
            ]
            ```
