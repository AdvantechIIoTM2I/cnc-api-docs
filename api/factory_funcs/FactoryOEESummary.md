# 3.4.3 FactoryOEESummary

## Information
* Get factory's OEE Summary, includes:
    * OEE (%)
    * Availability (%)
    * Performance (%)
    * Quality (%)
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the parent node path that you want to query.
* This API will return child nodes' infomation under the input parent node path.

## Format

* ### Request

  ```
  fns.FactoryOEESummary("path", "$from", "$to")
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
  | OEE | float | oee value (%) | 90 |
  | Availability | float | availability value (%) | 90 |
  | Performance | float | performance value (%) | 90 |
  | Quality | float | quality value (%) | 90 |

  
* ### Example
    1. Query OEE Summary of "Advantech" Group's child node (contains 1 child node : "Taipei")
        - Query   
        ``` 
        select * from fns.FactoryOEESummary("Advantech", "$from", "$to")
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Datatable Panel
        - Panel Screenshot      
            ![](/images/3.4.3-FactoryOEESummary.jpg)  

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
                            "sqltype": "float", 
                            "text": "OEE", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "Availability", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "Performance", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "Quality", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            "Taipei", 
                            74.58, 
                            81.8, 
                            91.17601856213125, 
                            100.0
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```
