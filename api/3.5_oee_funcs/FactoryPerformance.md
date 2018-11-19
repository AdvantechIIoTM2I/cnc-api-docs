# 3.5.3 FactoryPerformance

## Information

* Computes factory performance information, include
    * Performance
* Need to specify the Query time range (from $from to $to)
* Support only path

## Format

* ### Request

  ``` sh
  fns.FactoryQuality('path', '$from', '$to')
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
    1. Query Availability of path
        - Query
        ``` select Performance from fns.FactoryOEE("$Group/$Factory/$Category", "$from", "$to") ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * RankingBar
        - Panel Screenshot

            ![](/images/3.5.2-FactoryQuality.png)
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
                        "text": "Percentage",
                        "type": "number"
                    }
                    ],
                    "rows": [
                    [
                        "MC-35",
                        100.0
                    ],
                    [
                        "MC-12",
                        100.0
                    ],
                    [
                        "FM-04",
                        100.0
                    ]
                    ],
                    "type": "table"
                }
            ]

            ```
