# 3.4.4 FactoryDowntimeSummary

## Information
* Get factory's Downtime Summary, includes:
    * Number of Machines
    * Down state occurrence count
    * DownTime duration (second)
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the parent node path that you want to query.
* This API will return child nodes' infomation under the input parent node path.

## Format

* ### Request

  ```
  fns.FactoryDowntimeSummary("path", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path | /Advantech |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | Factory | String | Node name of this record | "Taipei" |
  | Machines | Int | Number of Machines under the "Factory" | 10 |
  | Occurrence | Int | Down state occurrence count | 10 |
  | Duration | float | DownTime duration (second) | 200.9 |

  
* ### Example
    1. Query Downtime Summary of "Advantech" Group's child node (contains 1 child node : "Taipei")
        - Query   
        ``` 
        select * from fns.FactoryDowntimeSummary("Advantech", "$from", "$to")
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Datatable Panel
        - Panel Screenshot      
            ![](/images/3.4.4-FactoryDowntimeSummary.jpg)

        - Return Value Example    
            ``` json
            [
                {
                    "columns": [
                        {
                            "sqltype": "str", 
                            "text": "Factory", 
                            "type": "string"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Machines", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Occurrence", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "Duration", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            "Taipei", 
                            3, 
                            28, 
                            2891123.3210000005
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```
