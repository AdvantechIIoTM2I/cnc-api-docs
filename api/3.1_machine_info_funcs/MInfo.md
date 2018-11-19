# 3.1.1 MInfo

## Information

* Get device infomation from WISE-PaaS APM AND device's RAW data from MongoDB
* Support one / multiple devices
* Dependent on WISE-PaaS APM (need to create Group first in APM).

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
    * Use 2 queries to display Machine information on Machine Temp Panel  
    ``` 
    SELECT DevID, DevName, Status, MainPgm as Program, Mode 
    FROM fns.MInfo( "$Group", "$Machine",  "$to")

    SELECT SpinTmp1 as ServTemp, ServTemp0 as SpinTmp1, ServTemp1 as SpinTmp2, ServTemp2 as SpinTmp3, ServTemp3 as SpinTmp4,ServTemp4 as SpinTmp5 
    FROM  fns.MInfo( "$Group", "$Machine",  "$to")
    ```
  - Return Data Format
    * table
  - Query Time Type
    * utc
  - Panel Screenshot
    ![](/images/3.1.1-MInfo-Temperature.jpg)
  - Return Value Example
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
                    "sqltype": "int", 
                    "text": "Status", 
                    "type": "number"
                }, 
                {
                    "sqltype": "str", 
                    "text": "Program", 
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
                    "MC-41", 
                    "MC-41", 
                    1, 
                    "191", 
                    "MEM"
                ]
            ], 
            "type": "table"
        }, 
        {
            "columns": [
                {
                    "sqltype": "int", 
                    "text": "ServTemp", 
                    "type": "number"
                }, 
                {
                    "sqltype": "int", 
                    "text": "SpinTmp1", 
                    "type": "number"
                }, 
                {
                    "sqltype": "int", 
                    "text": "SpinTmp2", 
                    "type": "number"
                }, 
                {
                    "sqltype": "int", 
                    "text": "SpinTmp3", 
                    "type": "number"
                }, 
                {
                    "sqltype": "int", 
                    "text": "SpinTmp4", 
                    "type": "number"
                }, 
                {
                    "sqltype": "int", 
                    "text": "SpinTmp5", 
                    "type": "number"
                }
            ], 
            "rows": [
                [
                    25, 
                    24, 
                    46, 
                    24, 
                    0, 
                    0
                ]
            ], 
            "type": "table"
        }
    ]
    ```
