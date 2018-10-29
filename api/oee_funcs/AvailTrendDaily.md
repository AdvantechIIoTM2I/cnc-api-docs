# 3.5.8 AvailTrendDaily

## Information

* Computes factory availability trend daily information within query time range
* Need to specify the Query time range (from $from to $to)
* Support only path


## Format

* ### Request

  ``` sh
  fns.PerformanceTrendDaily('path', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "device ID"


* ### Response Tags

    | Variable | Data Type | Description | Example |
    | :---: | :---: | :---: | :---: |
    | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
    | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
    | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |


* ### Example
    1. Query Availability of path
        - Query
        ``` select AvailDaily as metric, Availability, Ts from fns.AvailTrendDaily("$Group/$Factory/$Category", "$from", "$to") ```
        - Return Data Format
            * timeseries
        - Query Time Type
            * utc
        - Panel Type
            * Graph
        - Panel Screenshot

            ![](/images/3.5.8-AvailTrendDaily.png)
        - Return Value Example

            ``` json
            [
                {
                    "datapoints": [
                    [
                        79.0633392820041,
                        1540137600000
                    ],
                    [
                        84.45934644569022,
                        1540224000000
                    ],
                    [
                        82.66277625742393,
                        1540310400000
                    ],
                    [
                        77.63154233579687,
                        1540396800000
                    ],
                    [
                        82.89509249894891,
                        1540483200000
                    ],
                    [
                        0.0,
                        1540569600000
                    ],
                    [
                        0,
                        1540656000000
                    ],
                    [
                        96.91635219341998,
                        1540779858240
                    ]
                    ],
                    "target": "AvailDaily"
                }
            ]
            ```
