# 3.5.2 MQuality

## Information

* Computes factory quality information, include
    * Quality
* Need to specify the Query time range (from $from to $to)
* Support only path

## Format

* ### Request

  ``` sh
  fns.MQuality('path', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | Quality | float | Quality of the given Timestamp | 90.1 |


* ### Example
    1. Query Quality of path
        - Query
        ``` SQL 
        select Quality from fns.FactoryOEE("$Group/$Factory/$Category", "$from", "$to") 
        ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * Singlestat
        - Panel Screenshot

            ![](/images/3.5.2-MQuality.png)
        - Return Value Example

            ``` json
            [
                {
                    "columns": [
                        {
                            "sqltype": "float", 
                            "text": "Quality", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            100.0
                        ]
                    ], 
                    "type": "table"
                }
            ]
            ```
