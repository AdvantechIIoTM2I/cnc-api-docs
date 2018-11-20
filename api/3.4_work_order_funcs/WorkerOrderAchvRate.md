# 3.4.3 WorkerOrderAchvRate

## Information

* Get device’s Work Order achieve rate information, includes:
    * WOCount
    * FinishWOCount
    * AchvRate

* Support one / multiple devices


## Format

* ### Request

  ```sql
  fns.WorkerOrderAchvRate("path", "DevID", "$from", "$to")
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
  | WOCount | Int | Count of Work order | 60 |
  | FinishWOCount | Int | Count of finished work order | 59 |
  | AchiveRate | float | Calculate work order achive rate | 92 |

* ### Example
    1. Query AchiveRate information of a device or multiple device within a path
        - Query
        ```sql
        select * from fns.WorkerOrderAchvRate("$Group/$Factory/$Category", "", "$from", "$to")
        ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * Singlestat
        - Panel Screenshot
            ![](/images/3.4.3-WorkerOrderAchvRate.jpg)

        - Return Value Example
            ```json
            [
                {
                    "columns": [
                        {
                            "sqltype": "int", 
                            "text": "WOCount", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "FinishWOCount", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "float", 
                            "text": "AchvRate", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            24, 
                            11, 
                            45.83333333333333
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```
