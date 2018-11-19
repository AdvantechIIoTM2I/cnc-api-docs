# 3.4.6 FactoryProductionInfo

## Information
* Get factory's production information, includes:
    * Count of Work order
    * Count of finished work order
    * Achievement rate of work order
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the parent node path that you want to query.
* This API will return child nodes' infomation under the input parent node path.
* Special return format for Builder Panel (use timeseries return format)
## Format

* ### Request

  ```
  fns.FactoryProductionInfo("path", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path | /Advantech |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | WOCountKey | String | String combination with "ChildNode Name"+ "-WOCount" | "Taipei-WOCount" |
  | WOCount | Int | Count of Work order | 60 |
  | FinishWOCountKey | String | String combination with "ChildNode Name"+ "-FinishWOCount" | "Taipei-FinishWOCount" |
  | FinishWOCount | Int | Count of finished work order | 59 |
  | AchvKey | String | String combination with "ChildNode Name"+ "-Achv" | "Taipei-Achv" |
  | Achv | float | Achievement rate of work order(%) | 98.333 |

  
* ### Example
    1. Query Quality Summary of "Advantech" Group's child node (contains 1 child node : "Taipei")
        - Query
            - Contains 3 queries for displaying WOCount, FinishWOCount and Achv on Builder Panel
        ``` 
        select WOCountKey as metric, WOCount from fns.FactoryProductionInfo("Advantech", "$from", "$to")
        select FinishWOCountKey as metric, FinishWOCount from fns.FactoryProductionInfo("Advantech", "$from", "$to")
        select AchvKey as metric, Achv from fns.FactoryProductionInfo("Advantech", "$from", "$to")
        ```
        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Builder Panel
        - Panel Screenshot      
            ![](/images/3.4.6-FactoryProductionInfo.jpg)

        - Return Value Example    
            ``` json
            [
                {
                    "datapoints": [
                        [
                            11, 
                            11
                        ]
                    ], 
                    "target": "Taipei-WOCount"
                }, 
                {
                    "datapoints": [
                        [
                            5, 
                            5
                        ]
                    ], 
                    "target": "Taipei-FinishWOCount"
                }, 
                {
                    "datapoints": [
                        [
                            45.45454545454545, 
                            45.45454545454545
                        ]
                    ], 
                    "target": "Taipei-Achv"
                }
            ]       

            ```
