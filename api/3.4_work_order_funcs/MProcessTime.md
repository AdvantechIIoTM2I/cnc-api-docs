# 3.4.4 MProcessTime

## Information

* Get device’s Process Time information
* Support one / multiple devices


## Format

* ### Request

  ```sql
  fns.MPowerTime("path", "DevID", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | DevID | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "DevID"
    - 'DevID' can be empty string if you want to query all devices under the specified 'path'


* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | ProcessTime | float | unit is sec | 10800 |

* ### Example
    1. Query Process time of multiple device within a path
        - Query
        ```sql
        select * from fns.MPowerTime("$Group", "$Machine", "$from", "$to")
        ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * Singlestat
        - Panel Screenshot
            ![](/images/3.4.4-MProcessTime.png)

        - Return Value Example
            ```json
            [
                {
                    "columns": [
                    {
                        "sqltype": "float",
                        "text": "ProcessTime",
                        "type": "number"
                    }
                    ],
                    "rows": [
                    [
                        10440.0
                    ]
                    ],
                    "type": "table"
                }
            ]

            ```
