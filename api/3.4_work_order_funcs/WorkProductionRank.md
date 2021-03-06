# 3.4.7 WorkProductionRank

## Information

* Sort device’s production information includes:
    * No
    * Product Name
    * Planned Output
    * Yield
    * Working Hour
* Need to specify the Query time range (from $from to $to)
* Can specify number of output records (topN)
* Support only path


## Format

* ### Request

  ``` sh
  fns.WorkProductionRank('path', 'topN', '$from', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | topN | String | number of record to be returned | 5 |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

    | Variable | Data Type | Description | Example |
    | :---: | :---: | :---: | :---: |
    | No | int | Rank number | 1 |
    | ProductName | string | Product Name | Ｙ軸馬達座（ＭＥ類）|
    | PlanOutput | int | plant output number | 10 |
    | Yield | float | yield percentage | 90 |
    | WorkingHour | float | work time | 10.3 |


* ### Example
    1. Query Top 5 PlanOutput ranking under $Group/$Factory path
        - Query
        ``` sql
        select * from fns.WorkProductionRank("$Group/$Factory", "5",  "$from", "$to") 
        ```
        - Return Data Format
            * timeseries
        - Query Time Type
            * utc
        - Panel Type
            * Datatable Panel
        - Panel Screenshot

            ![](/images/3.4.7-WorkProductionRank.png)
        - Return Value Example

            ``` json
            [
                {
                    "columns": [
                    {
                        "sqltype": "int",
                        "text": "No",
                        "type": "number"
                    },
                    {
                        "sqltype": "str",
                        "text": "ProductName",
                        "type": "string"
                    },
                    {
                        "sqltype": "int",
                        "text": "PlanOutput",
                        "type": "number"
                    },
                    {
                        "sqltype": "int",
                        "text": "Yields",
                        "type": "number"
                    },
                    {
                        "sqltype": "int",
                        "text": "WorkTime",
                        "type": "number"
                    }
                    ],
                    "rows": [
                    [
                        1,
                        "Ｙ軸馬達座（ＭＥ類）",
                        30,
                        0,
                        0
                    ],
                    [
                        2,
                        "工作台",
                        4,
                        0,
                        0
                    ]
                    ],
                    "type": "table"
                }
            ]
            ```
