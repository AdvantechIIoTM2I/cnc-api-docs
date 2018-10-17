# 3.1.1 MStatus

## Information

* Get device's RAW data from MongoDB
* Support one / multiple devices

## Format

* ### Request

  ```
  fns.MStatus('<device ID>', '$to')
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | device ID | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | _id | String | MongoDB Record ID | 5bc5a83645cb64004dbe2121 |
  | SCADAID | String | SCADA ID | 9bf9c31c-0ee9-4e1d-a415-e18b42ccfb9d |
  | DevID | String | Device ID | MC-29 |
  | Ts | Datetime | Timestamp of the data | 1539679347445 |
  | Status | int | Device Status \(0: OFF, 1: RUN, 2: IDLE, 3: DOWN\) | 1 |
  | AlmCode | dict | Object of Alarm code \(Key: array number Value: code\) | { "0" : "100","1" : "255","2" : "260",} |
  | ServTemp | int | Servo Motor Temperature | 40.1 |
  | ServTempX | int | Servo’s X-axis Temperature | 40.1 |
  | ServTempY | int | Servo’s Y-axis Temperature | 40.1 |
  | ServTempZ | int | Servo’s Z-axis Temperature | 40.1 |
  | ServTempA | int | Servo’s A-axis Temperature | 40.1 |
  | ServTempB | int | Servo’s B-axis Temperature | 40.1 |
  | ServTempC | int | Servo’s C-axis Temperature | 40.1 |
  | OvFeed | int | Cutting Feed Override 進給百分比 \(%\) | 100 |
  | OvRapid | int | Rapid Feed Override 快動百分比 \(%\) | 100 |
  | OvSpin | int | Spindle Override 主軸轉速百分比 \(%\) | 100 |
  | MainPgm | String | Main Program | Program-001 |
  | Mode | String | Mode | ex: “MDI”, “MEM”, ... |

* ### Example

  - Query
    * Select All Tags:  
    ``` select * from fns.MStatus('{GR-25, MC-02}', '$to') ```
    * Select some Tags:   
    ``` select DevID, Status from fns.MStatus('{GR-25, MC-02}', '$to') ```
  - Return Data Format
    * table
  - Query Time Type
    * utc
  - Panel Screenshot
    * All Tags with Table panel
    ![](/images/3.1.1-MStatus-Table.png)
  - Return Value Example
    * All Tags
    ```
    [
      {
        "columns": [
          {
            "sqltype": "str", 
            "text": "_id", 
            "type": "string"
          }, 
          {
            "sqltype": "str", 
            "text": "ScadaID", 
            "type": "string"
          }, 
          {
            "sqltype": "str", 
            "text": "DevID", 
            "type": "string"
          }, 
          {
            "sqltype": "datetime", 
            "text": "Ts", 
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
            "5bc5a83645cb64004dbe2121", 
            "9bf9c31c-0ee9-4e1d-a415-e18b42ccfb9d", 
            "MC-31", 
            1539680317767, 
            0, 
            {}, 
            29, 
            40, 
            53, 
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
