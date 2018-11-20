# 3.6.4 ChildNodeQualitySummary

## Information
* Get factory's Quality Summary, includes:
    * Number of Machines
    * Number of Defect (Pcs)
    * Yield Rate (%)
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the parent node path that you want to query.
* This API will return child nodes' infomation under the input parent node path.

## Format

* ### Request

  ```
  fns.ChildNodeQualitySummary("path", "$from", "$to")
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
  | Defect | Int | Number of Defect (Pcs) | 10 |
  | Yield | float | Yield Rate (%) | 99.9 |

  
* ### Example
    1. Query Quality Summary of "Advantech" Group's child node (contains 1 child node : "Taipei")
        - Query   
        ``` json 
        select * from fns.ChildNodeQualitySummary("Advantech", "$from", "$to")
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Datatable Panel
        - Panel Screenshot      
            ![](/images/3.6.4-ChildNodeQualitySummary.jpg)

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
                            "text": "Defect", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "Yield", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            "Taipei", 
                            0, 
                            100.0
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```
