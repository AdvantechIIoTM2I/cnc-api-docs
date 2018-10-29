# 3.4.2 FactoryWorkOrderAch

## Information
* Get factory's work order achievement information, includes:
    * Count of Work order
    * Count of finished work order
    * Achievement rate of work order
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the parent node path that you want to query.
* This API will return child nodes' infomation under the input parent node path.

## Format

* ### Request

  ```
  fns.FactoryWorkOrderAch("path", "$from", "$to")
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
  | WOCount | Int | Count of Work order | 60 |
  | FinishWOCount | Int | Count of finished work order | 59 |
  | Achv | float | Achievement rate of work order(%) | 98.333 |

  
* ### Example
    1. Query work order achievement information of "Advantech" Group's child node (contains 1 child node : "Taipei")
        - Query   
        ``` 
        select * from fns.FactoryWorkOrderAch("Advantech", "$from", "$to")
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Datatable Panel
        - Panel Screenshot      
            ![](/images/3.4.2-FactoryWorkOrderAch.jpg)  

        - Return Value Example    
            ```
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
                            "text": "WOCount", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "FinishWOCount", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "Achv", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            "Taipei", 
                            4, 
                            4, 
                            100.0
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```
