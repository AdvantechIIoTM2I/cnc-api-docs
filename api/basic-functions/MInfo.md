# 3.1.2 MInfo

## Information

* Get device infomation from WISE-PaaS APM AND device's RAW data from MongoDB
* Support one / multiple devices

## Format

* ### Request

  ```
  fns.MInfo("path","device_id", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | DevID | String | Device ID | MC-29 |
  | DevName | String | Device Name | MC-29 |
  | DevDesc | String | Device Description | Type : H630B |
  | ImgData | String | Device's image URL or binary | https://i.imgur.com/60Z4Pz9.jpg |
  | _id | String | MongoDB Record ID | 5bc5a83645cb64004dbe2121 |
  | s | String | SCADA ID | 9bf9c31c-0ee9-4e1d-a415-e18b42ccfb9d |
  | d | String | Device ID | MC-29 |
  | ts | Datetime | Timestamp of the data | 1539679347445 |
  | Status | int | Device Status \(0: OFF, 1: RUN, 2: IDLE, 3: DOWN\) | 1 |
  | AlmCode | dict | Object of Alarm code \(Key: array number Value: code\) | { "0" : "100","1" : "255","2" : "260",} |
  | SpinTmp1 | int | Spindle Temperature | 40.1 |
  | ServTemp0 | int | Servo’s 1st Temperature | 40.1 |
  | ServTemp1 | int | Servo’s 2nd Temperature | 40.1 |
  | ... | ... | ... | ... |
  | ServTemp11 | int | Servo’s 11th Temperature | 40.1 |
  | OvFeed | int | Cutting Feed Override 進給百分比 \(%\) | 100 |
  | OvRapid | int | Rapid Feed Override 快動百分比 \(%\) | 100 |
  | OvSpin | int | Spindle Override 主軸轉速百分比 \(%\) | 100 |
  | MainPgm | String | Main Program | Program-001 |
  | Mode | String | Mode | ex: “MDI”, “MEM”, ... |

* ### Example

  - Query
    * Select All Tags:  
    ``` select * from fns.MInfo("Advantech/Taipei","{MC-31}", "$to") ```
    * Select some Tags:   
    ``` select DevID, DevName, DevDesc from fns.MStatus("Advantech/Taipei","{MC-31}", "$to") ```
  - Return Data Format
    * table
  - Query Time Type
    * utc
  - Panel Screenshot
    * All Tags with Table panel
    ![](/images/3.1.2-MInfo-Table.jpg)
  - Return Value Example
    * All Tags
    ``` json
    [
        {
            "columns": [
            {
                "sqltype": "str", 
                "text": "DevID", 
                "type": "string"
            }, 
            {
                "sqltype": "str", 
                "text": "DevName", 
                "type": "string"
            }, 
            {
                "sqltype": "str", 
                "text": "DevDesc", 
                "type": "string"
            }, 
            {
                "sqltype": "str", 
                "text": "ImgData", 
                "type": "string"
            }, 
            {
                "sqltype": "ObjectId", 
                "text": "_id", 
                "type": "string"
            }, 
            {
                "sqltype": "str", 
                "text": "s", 
                "type": "string"
            }, 
            {
                "sqltype": "str", 
                "text": "d", 
                "type": "string"
            }, 
            {
                "sqltype": "datetime", 
                "text": "ts", 
                "type": "time"
            }, 
            {
                "sqltype": "int", 
                "text": "Status", 
                "type": "number"
            }, 
            {
                "sqltype": "dict", 
                "text": "AlmCode", 
                "type": "string"
            }, 
            {
                "sqltype": "int", 
                "text": "ServTemp", 
                "type": "number"
            }, 
            {
                "sqltype": "int", 
                "text": "ServTempX", 
                "type": "number"
            }, 
            {
                "sqltype": "int", 
                "text": "ServTempY", 
                "type": "number"
            }, 
            {
                "sqltype": "int", 
                "text": "ServTempZ", 
                "type": "number"
            }, 
            {
                "sqltype": "int", 
                "text": "OvFeed", 
                "type": "number"
            }, 
            {
                "sqltype": "int", 
                "text": "OvRapid", 
                "type": "number"
            }, 
            {
                "sqltype": "int", 
                "text": "OvSpin", 
                "type": "number"
            }, 
            {
                "sqltype": "str", 
                "text": "MainPgm", 
                "type": "string"
            }, 
            {
                "sqltype": "str", 
                "text": "Mode", 
                "type": "string"
            }
            ], 
            "rows": [
            [
                "MC-31", 
                "MC-31", 
                "Type : H630B", 
                "https://i.imgur.com/60Z4Pz9.jpg", 
                "ObjectId('5bc6d1bf45cb64004dbe6e05')", 
                "9bf9c31c-0ee9-4e1d-a415-e18b42ccfb9d", 
                "MC-31", 
                1539756486770, 
                1, 
                {}, 
                24, 
                36, 
                51, 
                32, 
                100, 
                25, 
                100, 
                "5249", 
                "MEM"
            ]
            ], 
            "type": "table"
        }
    ]
    ```
