# 3.5.1 YieldRanking

## Information

* Computes device’s yield information, include
    * Yield percnetage
* Need to specify the Query time range (from $from to $to)
* Support only path

## Format

* ### Request

  ``` sh
  fns.YieldRanking('path', '<topN>', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | topN | String | number of record to be returned | 5 |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | No | int | Rank number | 1 |
  | Machine | String | Device ID | MC-29 |
  | Yield | float | Device's yield percentage | 100 |


* ### Example
    1. Query Availability of path
        - Query
        ``` select Machine as Matric, Percentage from fns.YieldRanking('$Group' ,'5', '$from','$to') order by Percentage asc ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * Singlestat
        - Panel Screenshot

            ![](/images/3.5.1-YieldRanking.png)
        - Return Value Example
            ``` json
            [
                {
                    "columns": [
                        {
                            "sqltype": "str",
                            "text": "Matric",
                            "type": "string"
                        },
                        {
                            "sqltype": "float",
                            "text": "Yield",
                            "type": "number"
                        }                    
                    ], 
                    "rows": [
                        [
                            "BO-03", 
                            100.0
                        ], 
                        [
                            "BO-07", 
                            100.0
                        ], 
                        [
                            "BO-08", 
                            100.0
                        ], 
                        [
                            "BO-06", 
                            100.0
                        ], 
                        [
                            "MC-31", 
                            100.0
                        ]
                    ], 
                    "type": "table"
                }
            ]
            ```
