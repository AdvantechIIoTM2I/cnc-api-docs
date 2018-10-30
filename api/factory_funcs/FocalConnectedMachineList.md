# 3.4.7 FocalConnectedMachineList

## Information
* Get factory's connected machine, includes:
    * Machine ID
    * Latest status
    * Latest status duration
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the node path that you want to query.
* This API will return the machine information within this node path.
* Only the online machine will be displayed in this API.
  
## Format

* ### Request

  ```
  fns.FocalConnectedMachineList("path", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path | /Advantech |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | Machine | String | Machine ID | MC-29 |
  | StatusDuration | float | Latest Device status duration (sec.) | 300.21 |
  | Status | int | Device Status \(1: RUN, 2: IDLE, 3: DOWN\) | 1 |
  
* ### Example
    1. Query connected machine of {"Advantech" Group / "Taipei" Factory}
        - Query   
        ``` 
        select * from fns.FocalConnectedMachineList('Advantech/Taipei', '$from', '$to')
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Datatable Panel
        - Panel Screenshot      
            ![](/images/3.4.7-FocalConnectedMachineList.jpg)
        - Return Value Example    
            ``` json
            [
                {
                    "columns": [
                        {
                            "sqltype": "str", 
                            "text": "Machine", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "StatusDuration", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Status", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            "FM-04", 
                            3479.109, 
                            1
                        ], 
                        [
                            "MC-12", 
                            85.092, 
                            1
                        ], 
                        [
                            "MC-16", 
                            481.085, 
                            1
                        ], 
                        [
                            "MC-22", 
                            6.929, 
                            2
                        ], 
                        [
                            "MC-30", 
                            459.03, 
                            1
                        ], 
                        [
                            "MC-35", 
                            2329.231, 
                            1
                        ], 
                        [
                            "MC-36", 
                            367.202, 
                            1
                        ], 
                        [
                            "MC-38", 
                            611.439, 
                            1
                        ], 
                        [
                            "PL-03", 
                            9268.62, 
                            1
                        ]
                    ], 
                    "type": "table"
                }
            ]
            ```
