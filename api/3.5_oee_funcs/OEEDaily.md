# 3.5.5 OEEDaily

## Information

* Computes factory oee trend daily information within query time range
* Need to specify the Query time range (from $from to $to)
* Support only path


## Format

* ### Request

  ``` sh
  fns.OEEDaily('path', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

    | Variable | Data Type | Description | Example |
    | :---: | :---: | :---: | :---: |
    | OEE | float | OEE of the given Timestamp | 90.1 |
    | Ts | Datetime | Timestamp of the data | 1539679347445 |


* ### Example
    1. Query OEE of path
        - Query
        ```  sql
        select OEEDaily as metric, OEE, Ts from fns.OEEDaily("$Group/$Factory/$Category", "$from", "$to") 
        ```
        - Return Data Format
            * timeseries
        - Query Time Type
            * utc
        - Panel Type
            * Graph
        - Panel Screenshot

            ![](/images/3.5.5-OEEDaily.png)
        - Return Value Example

            ``` json
            [
                {
                    "datapoints": [
                    [
                        97.76457844928272,
                        1540137600000
                    ],
                    [
                        0.0,
                        1540224000000
                    ],
                    [
                        88.06010874329225,
                        1540310400000
                    ],
                    [
                        76.3237768220493,
                        1540396800000
                    ],
                    [
                        2881.414461959448,
                        1540483200000
                    ],
                    [
                        0.0,
                        1540569600000
                    ],
                    [
                        0.0,
                        1540656000000
                    ],
                    [
                        0.0,
                        1540779858240
                    ]
                    ],
                    "target": "OEEDaily"
                }
            ]
            ```
