# 3.2.4 MAvailDaily

## Information

* Get device’s daily availability information, include:
    * Availability per day
    * Run/Down/Idle/Off time per day
* Support single / multiple devices
* The data start from the “DATE” of “$from” (don’t care about time)
* One information per day from historical data in MongoDB
* Calculate End time’s availability (00:00 today to $to) from realtime data in MongoDB

## Format

* ### Request

    ```
    fns.MAvailDaily("path",'device_id', "$from", "$to")
    ```

    | Variable | Data Type | Description | Example |
    | :---: | :---: | :---: | :---: |
    | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
    | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
    | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
    | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

    - **Note:**
        - 'path' can be empty string if you want to query all devices with the same name of "device ID"
        - 'device_id' can be empty string if you want to query all devices under the specified 'path'
  

* ### Response Tags

    | Tag Name | Data Type | Description | Example |
    | :---: | :---: | :---: | :---: |
    | DevID | String | Device ID | MC-29 |
    | Ts | Datetime | Timestamp of the data | 1539679347445 |    
    | OffTime | float | Device's total Off time(sec.) refer to the given timestamp | 100.11 |
    | RunTime | float | Device's total Run time(sec.) refer to the given timestamp | 60000.11 |
    | IdleTime | float | Device's total Idle time(sec.) refer to the given timestamp | 10000.11 |  
    | DownTime | float | Device's total Down time(sec.) refer to the given timestamp | 50.11 |
    | Total | float | RunTime + IdleTime + DownTime (sec.) refer to the given timestamp  | 70050.33 |
    | DownCount | int | Number of Down state refer to the given timestamp  | 2 |
    | Availability | float | Device's Availability refer to the given timestamp  | 90.1 |
  

* ### Example  
    1. Query Daily Availability of one device   
        - Query   
        ``` select DevID as metric, Availability, Ts from fns.MAvailDaily("Group1", '{BO-07}',"$from","$to") ```
        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Graph
        - Panel Screenshot      
            ![](/images/3.2.4-MAvailDaily-Avail.jpg)
        - Return Value Example    
            ``` json
            [
                {
                    "datapoints": [
                        [
                            0, 
                            1539100800000
                        ], 
                        [
                            5.978824932577841, 
                            1539187200000
                        ], 
                        [
                            73.56582886830947, 
                            1539273600000
                        ], 
                        [
                            100.0, 
                            1539360000000
                        ], 
                        [
                            100.0, 
                            1539446400000
                        ], 
                        [
                            74.3505097593457, 
                            1539532800000
                        ], 
                        [
                            76.91675318926967, 
                            1539619200000
                        ], 
                        [
                            62.116643311103104, 
                            1539772882196
                        ]
                    ], 
                    "target": "BO-07"
                }
            ]
            ```  
    2. Query Daily Status composition of one device   
        - Query  
            * Use 4 queries for this panel 
            ``` 
            select RUN as metric, RunTime, Ts from fns.MAvailDaily("", "{BO-07}", "$from", "$to")
            select IDLE as metric, IdleTime, Ts from fns.MAvailDaily("", "{BO-07}", "$from", "$to")
            select DOWN as metric, DownTime, Ts from fns.MAvailDaily("", "{BO-07}", "$from", "$to")
            select OFF as metric, OffTime, Ts from fns.MAvailDaily("", "{BO-07}", "$from", "$to") 
            ```
        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Grouped Bar Chart Panel
        - Panel Screenshot      
            ![](/images/3.2.4-MAvailDaily-Stack.jpg)
        - Return Value Example    
            ``` json
            [
                {
                    "datapoints": [
                        [
                            0, 
                            1539100800000
                        ], 
                        [
                            2074.232, 
                            1539187200000
                        ], 
                        [
                            44145.028000000006, 
                            1539273600000
                        ], 
                        [
                            86400.0, 
                            1539360000000
                        ], 
                        [
                            86400.0, 
                            1539446400000
                        ], 
                        [
                            45555.42499999999, 
                            1539532800000
                        ], 
                        [
                            26559.721, 
                            1539619200000
                        ], 
                        [
                            12438.1, 
                            1539773084798
                        ]
                    ], 
                    "target": "RUN"
                }, 
                {
                    "datapoints": [
                        [
                            0, 
                            1539100800000
                        ], 
                        [
                            32618.738999999998, 
                            1539187200000
                        ], 
                        [
                            15862.49, 
                            1539273600000
                        ], 
                        [
                            0, 
                            1539360000000
                        ], 
                        [
                            0, 
                            1539446400000
                        ], 
                        [
                            15715.742, 
                            1539532800000
                        ], 
                        [
                            7970.755000000002, 
                            1539619200000
                        ], 
                        [
                            7788.282, 
                            1539773084798
                        ]
                    ], 
                    "target": "IDLE"
                }, 
                {
                    "datapoints": [
                        [
                            0, 
                            1539100800000
                        ], 
                        [
                            0, 
                            1539187200000
                        ], 
                        [
                            0, 
                            1539273600000
                        ], 
                        [
                            0, 
                            1539360000000
                        ], 
                        [
                            0, 
                            1539446400000
                        ], 
                        [
                            0, 
                            1539532800000
                        ], 
                        [
                            0, 
                            1539619200000
                        ], 
                        [
                            0, 
                            1539773084798
                        ]
                    ], 
                    "target": "DOWN"
                }, 
                {
                    "datapoints": [
                        [
                            86400.0, 
                            1539100800000
                        ], 
                        [
                            51707.029, 
                            1539187200000
                        ], 
                        [
                            26392.482, 
                            1539273600000
                        ], 
                        [
                            0, 
                            1539360000000
                        ], 
                        [
                            0, 
                            1539446400000
                        ], 
                        [
                            25128.833, 
                            1539532800000
                        ], 
                        [
                            51869.524000000005, 
                            1539619200000
                        ], 
                        [
                            47258.416, 
                            1539773084798
                        ]
                    ], 
                    "target": "OFF"
                }
            ]  
            ```

 