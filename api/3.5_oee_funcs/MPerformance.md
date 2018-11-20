# 3.5.3 MPerformance

## Information

* Computes factory performance information, include
    * Performance
* Need to specify the Query time range (from $from to $to)
* Support only path

## Format

* ### Request

  ``` sh
  fns.MPerformance('path', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | Performance | String | performance unit is percentage | 90 |


* ### Example
    1. Query Performance of path
        - Query
        ``` SQL 
        select Performance from fns.MPerformance("$Group/$Factory/$Category", "$from", "$to") 
        ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * RankingBar
        - Panel Screenshot

            ![](/images/3.5.3-MPerformance.png)
        - Return Value Example

            ``` json
            [
                {
                    "columns": [
                        {
                            "sqltype": "float", 
                            "text": "Performance", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            201.97695736387269
                        ]
                    ], 
                    "type": "table"
                }
            ]
            ```
