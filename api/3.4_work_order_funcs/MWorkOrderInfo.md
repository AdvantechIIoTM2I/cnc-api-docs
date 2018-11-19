# 3.6.5 MWorkOrderInfo

## Information

* Get device’s Ｗork order Info, including:
    * DeviceID
    * Status
    * ImgData
* Using this query with fns.MWorkOrder
* Support one / multiple devices


## Format

* ### Request

  ```sql
  fns.MWorkOrderInfo("path", "DevID", "$from", "$to")
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
  | DeviceID | String | Device ID | MC-29 |
  | Status | int | device status 0/1/2 | 0 |
  | ImgData | string | image url or Base64 string| data:image/base64, xxxxx |

* ### Example
    1. Query work order info information of a device or multiple device within a path
        - Query
        ```sql
        SELECT * FROM fns.MWorkOrderInfo("$Group/$Factory/$Category","",  "$from", "$to")
        ```
        - Return Data Format
            * table
        - Query Time Type
            * utc
        - Panel Type
            * Work Order
        - Panel Screenshot
            ![](/images/3.6.5-MWorkOrderInfo.png)

        - Return Value Example
            ```json
            [
                {
                    "columns": [
                    {
                        "sqltype": "str",
                        "text": "DeviceID",
                        "type": "string"
                    },
                    {
                        "sqltype": "int",
                        "text": "Status",
                        "type": "number"
                    },
                    {
                        "sqltype": "str",
                        "text": "ImgData",
                        "type": "string"
                    }
                    ],
                    "rows": [
                    [
                        "MC-35",
                        0,
                        "https://i.ytimg.com/vi/seiZH0TrWyE/hqdefault.jpg",
                    ],
                    [
                        "MC-12",
                        0,
                        "https://i.ytimg.com/vi/seiZH0TrWyE/hqdefault.jpg",
                    ],
                    [
                        "MC-04",
                        1,
                        "https://i.ytimg.com/vi/seiZH0TrWyE/hqdefault.jpg",
                    ]
                    ]
                }
            ]

            ```
