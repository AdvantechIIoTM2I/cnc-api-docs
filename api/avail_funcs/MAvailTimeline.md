# 3.2.2 MAvailTimeline

## Information

* Computes device’s availability information
* Get all device’s Status within query time range
* Support one / multiple devices

## Format

* ### Request

    ```
    fns.MAvailTimeline('path', 'device ID', '$from', '$to')
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
    | DevID | String | Device ID | MC-29 |
    | Status | int | Device Status \(0: OFF, 1: RUN, 2: IDLE, 3: DOWN\) | 1 |
    | Ts | Datetime | Timestamp of the data | 1539679347445 |    
    | Availability | float | Device's Availability within query time range | 90.1 |
  

* ### Example  
    1. Query Availability and status timeline of one device   
        - Query   
        ``` select * from fns.MAvailTimeline("Group1/Child1","{GR-12}", "$from", "$to") ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Timeline List
        - Panel Screenshot      
            ![](/images/3.2.2-MAvailTimeline.jpg)
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
                            "text": "Status", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "datetime", 
                            "text": "Ts", 
                            "type": "time"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "Availability", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            "GR-12", 
                            "0", 
                            1539705600000, 
                            71.53
                        ], 
                        [
                            "GR-12", 
                            "1", 
                            1539746652485, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "2", 
                            1539748724781, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "1", 
                            1539752758308, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "2", 
                            1539754824034, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "1", 
                            1539754864078, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "2", 
                            1539754994228, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "1", 
                            1539755034273, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "2", 
                            1539760752494, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "1", 
                            1539760792540, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "0", 
                            1539761243024, 
                            0
                        ], 
                        [
                            "GR-12", 
                            "0", 
                            1539767049145, 
                            0
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```

 