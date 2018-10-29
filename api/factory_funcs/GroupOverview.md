# 3.4.1 GroupOverview

## Information
* Dependence to WISE-PaaS APM (need to create Group first in APM)
* Refer to the Group Node and display its child nodes' Overview with the following information:
    * Address
    * Current RUN / IDLE / DOWN machine count of this group
    * Average OEE within last 7 days
* Special return format for using Worldmap Card Panel
* Support path only

## Format

* ### Request

  ```
  fns.GroupOverview("path", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | location | String | Group name of this data | "Taipei" |
  | latitude | float | latitude of this data | 25.057673 |
  | longitude | float | longitude of this data | 121.38182 |
  | metric | String | Value of this data | "No.27, Wende Rd., Guishan Dist.,Taoyuan,33371,Taoyuan,Taiwan" |
  | hostname | String | Name of this data | "Address" |
  
* ### Example
    1. Query "Advantech" Group's overview (contains 1 child node : "Taipei")
        - Query   
        ``` 
        select * from fns.GroupOverview("Advantech", "$from", "$to")
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Worldmap Card Panel
        - Panel Screenshot      
            ![](/images/3.4.1-GroupOverview.jpg)  

        - Return Value Example    
            ```
            [
                {
                    "columns": [
                        {
                            "sqltype": "str", 
                            "text": "location", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "latitude", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "longitude", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "list", 
                            "text": "metric", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "str", 
                            "text": "hostname", 
                            "type": "string"
                        }
                    ], 
                    "rows": [
                        [
                            "Taipei", 
                            25.057673, 
                            121.38182, 
                            [
                            "No.27, Wende Rd., Guishan Dist.,Taoyuan,33371,Taoyuan,Taiwan"
                            ], 
                            "Address"
                        ], 
                        [
                            "Taipei", 
                            25.057673, 
                            121.38182, 
                            [
                            2
                            ], 
                            "RUN"
                        ], 
                        [
                            "Taipei", 
                            25.057673, 
                            121.38182, 
                            [
                            1
                            ], 
                            "IDLE"
                        ], 
                        [
                            "Taipei", 
                            25.057673, 
                            121.38182, 
                            [
                            0
                            ], 
                            "DOWN"
                        ], 
                        [
                            "Taipei", 
                            25.057673, 
                            121.38182, 
                            [
                            142.23
                            ], 
                            "OEE"
                        ]
                    ], 
                    "type": "table"
                }
            ]


            ```
