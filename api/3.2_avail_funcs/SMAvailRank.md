# 3.2.4 SMAvailRank

## Information

* Sort device’s availability information by given input (rank_type), includes:
    * OffTime / RunTime / IdleTime / DownTime
    * Total
    * DownCount
    * Availability
* Can specify number of output records (topN)
* Support one / multiple devices

## Format

* ### Request

    ```
    fns.SMAvailRank("path",'device_id', 'rank_type', 'topN', "$from", "$to")
    ```

    | Variable | Data Type | Description | Example |
    | :---: | :---: | :---: | :---: |
    | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
    | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
    | rank_type | String | Tag that you want to rank by | OffTime / RunTime / IdleTime / DownTime<br>Total / DownCount / Availability |
    | topN | String | number of record to be returned | 5 |
    | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
    | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

    - **Note:**
        - 'path' can be empty string if you want to query all devices with the same name of "device ID"
        - 'device_id' can be empty string if you want to query all devices under the specified 'path'
  

* ### Response Tags

    | Tag Name | Data Type | Description | Example |
    | :---: | :---: | :---: | :---: |
    | No | int | Rank number | 1 |
    | DevID | String | Device ID | MC-29 |
    | OffTime | float | Device's total Off time(sec.) within query time range | 100.11 |
    | RunTime | float | Device's total Run time(sec.) within query time range  | 60000.11 |
    | IdleTime | float | Device's total Idle time(sec.) within query time range | 10000.11 |  
    | DownTime | float | Device's total Down time(sec.) within query time range | 50.11 |
    | Total | float | RunTime + IdleTime + DownTime (sec.) within query time range | 70050.33 |
    | DownCount | int | Number of Down state within query time range  | 2 |
    | Availability | float | Device's Availability within query time range  | 90.1 |
  

* ### Example  
    1. Top 5 DownTime device ranking under $Group/$Factory path  
        - Query   
        ``` select DevID as metric, DownTime from fns.SMAvailRank("$Group/$Factory", "", "DownTime", "5", "$from", "$to") ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Ranking Bar
        - Panel Screenshot      
            ![](/images/3.2.4-SMAvailRank.jpg)
        - Return Value Example    
            ``` json
            [
                {
                    "columns": [
                        {
                            "sqltype": "str", 
                            "text": "metric", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "DownTime", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            "FM-02", 
                            67626.342
                        ], 
                        [
                            "FM-01", 
                            26987.006999999994
                        ], 
                        [
                            "MC-27", 
                            17480.194000000003
                        ], 
                        [
                            "FA-01", 
                            6513.322
                        ], 
                        [
                            "MC-23", 
                            1850.8619999999999
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```

 