# 3.5.4 FactoryOEE

## Information

* Computes factory OEE information, include
    * OEE
    * yield
    * performance
    * quality

* Need to specify the Query time range (from $from to $to)
* Support only path

## Format

* ### Request

  ``` sh
  fns.FactoryOEE('path', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "device ID"


* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | OEE | String | oee unit is percentage | 90 |
  | Availability | String | availability unit is percentage | 90 |
  | Performance | String | performance unit is percentage | 90 |
  | Quality | String | quality unit is percentage | 90 |


* ### Example
    1. Query Availability of path
        - Query
        ``` select * from fns.FactoryOEE("$Group/$Factory/$Category", "$from", "$to") ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * Singlestat
        - Panel Screenshot

            ![](/images/3.5.4-FactoryOEE.png)
        - Return Value Example

            ``` json
            [
            {
                "columns": [
                    {
                        "sqltype": "float",
                        "text": "OEE",
                        "type": "number"
                    },
                    {
                        "sqltype": "float",
                        "text": "Availabilty",
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
                        113.15,
                        80.69,
                        140.22999045714718,
                        100.0
                    ]
                    ],
                    "type": "table"
                }
            ]


            ```
