# 3.6.6 MWorkAbnormalityRank

## Information

* Get device’s Work order abnormality rank.
* Support one / multiple devices


## Format

* ### Request

  ```sql
  fns.MWorkAbnormalityRank("path", "DevID", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | DevID | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | topN | String | number of record to be returned | 5 |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "DevID"
    - 'DevID' can be empty string if you want to query all devices under the specified 'path'


* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | No | int | ranking number | 1 |
  | Desc | string | the abnormality name | 品質異常排除 |
  | Occurrence | int | occurrence times | 3 |

* ### Example
    1. Query Power time of multiple device within a path
        - Query
        ```sql
        select Desc as metric, Occurrence from fns.MWorkAbnormalityRank("$Group/$Factory/$Category", "", "5", "$from", "$to" )
        ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * Ranking Bar
        - Panel Screenshot
            ![](/images/3.6.6-MWorkAbnormalityRank.png)

        - Return Value Example
            ```json
            [
                {
                    "columns": [
                    {
                        "sqltype": "str",
                        "text": "metric",
                        "type": "string"
                    },
                    {
                        "sqltype": "int",
                        "text": "Occurrence",
                        "type": "number"
                    }
                    ],
                    "rows": [
                    [
                        "品質異常排除",
                        1
                    ]
                    ],
                    "type": "table"
                }
            ]

            ```
