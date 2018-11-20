# 3.5.7 OEEDailyP

## Information

* Computes factory performance trend daily information within query time range
* Need to specify the Query time range (from $from to $to)
* Support only path


## Format

* ### Request

  ``` sh
  fns.OEEDailyP('path', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

    | Variable | Data Type | Description | Example |
    | :---: | :---: | :---: | :---: |
    | Performance | float | Performance of the given Timestamp | 90.1 |
    | Ts | Datetime | Timestamp of the data | 1539679347445 |


* ### Example
    1. Query Performance of path
        - Query
        ``` sql
        select PerformanceDaily as metric, Performance, Ts from fns.OEEDailyP("$Group/$Factory/$Category", "$from", "$to") 
        ```
        - Return Data Format
            * timeseries
        - Query Time Type
            * utc
        - Panel Type
            * Graph
        - Panel Screenshot

            ![](/images/3.5.7-OEEDailyP.png)
        - Return Value Example

            ``` json
            [
                {
                    "datapoints": [
                    [
                        123.65349014740552,
                        1540137600000
                    ],
                    [
                        0,
                        1540224000000
                    ],
                    [
                        106.5293385127306,
                        1540310400000
                    ],
                    [
                        98.31541989969644,
                        1540396800000
                    ],
                    [
                        3475.9771357948403,
                        1540483200000
                    ],
                    [
                        0,
                        1540569600000
                    ],
                    [
                        0,
                        1540656000000
                    ],
                    [
                        0,
                        1540779858240
                    ]
                    ],
                    "target": "PerformanceDaily"
                }
            ]
            ```
