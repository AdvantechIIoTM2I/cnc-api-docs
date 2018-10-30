# 3.6.1 MWorkOrder

## Information

* Get device’s Ｗork order, including:
    * OrderStatus
    * WorkOrder
    * Operator
    * ProductName
    * RemainOutput
    * PlanOutput
    * RemainTime
    * StartTime

* Support one / multiple devices


## Format

* ### Request

  ```sql
  fns.MWorkOrder("path", "DevID", "$from", "$to")
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
  | OrderStatus | string | order status, Continuing/O.K. | O.K. |
  | WorkOrder | int | Work order | 21063301 |
  | Operator | string | operator name | 王大明 |
  | ProductName | int | product name | 工作台 |
  | RemainOutput | int | remain output | 0 |
  | PlanOutput | int | plan output | 30 |
  | RemainTime | float | remain time (sec) | 86400 |
  | StartTime | datetime | Timestamp of the work order start time | 1540772178820 |

* ### Example
    1. Query work order basic information of a device or multiple device within a path
        - Query
        ```sql
        SELECT * FROM fns.MWorkOrder("$Group/$Factory/$Category", "", "$from" ,"$to")
        ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * Work Order
        - Panel Screenshot
            ![](/images/3.6.1-MWorkOrder.png)

        - Return Value Example
            ```json
            [
                {
                    "columns": [
                    {
                        "sqltype": "str",
                        "text": "OrderStatus",
                        "type": "string"
                    },
                    {
                        "sqltype": "str",
                        "text": "WorkOrder",
                        "type": "string"
                    },
                    {
                        "sqltype": "str",
                        "text": "Operator",
                        "type": "string"
                    },
                    {
                        "sqltype": "str",
                        "text": "ProductName",
                        "type": "string"
                    },
                    {
                        "sqltype": "int",
                        "text": "RemainOutput",
                        "type": "number"
                    },
                    {
                        "sqltype": "int",
                        "text": "PlanOutput",
                        "type": "number"
                    },
                    {
                        "sqltype": "str",
                        "text": "RemainTime",
                        "type": "string"
                    },
                    {
                        "sqltype": "datetime",
                        "text": "StartTime",
                        "type": "time"
                    }
                    ],
                    "rows": [
                    [
                        "O.K.",
                        "21063305",
                        "許明",
                        "工作台",
                        0,
                        4,
                        "--",
                        1540783747593
                    ],
                    [
                        "--",
                        "--",
                        "--",
                        "--",
                        "--",
                        "--",
                        "--",
                        "--"
                    ],
                    [
                        "O.K.",
                        "21062901",
                        "徐安田",
                        "Ｙ軸馬達座（ＭＥ類）",
                        20,
                        30,
                        "--",
                        1540772178820
                    ]
                    ],
                    "type": "table"
                }
            ]

            ```
