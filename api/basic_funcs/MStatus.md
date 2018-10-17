# MStatus
---
## Information
* Get device's RAW data from MongoDB
* Support one / multiple devices

## Format

* Request  
```  
fns.MStatus('<device ID>', 'to')
```
| Variable | Data Type | Description | Example |
| :---: | :---: | :---: | :---: |
| device ID | String | String of device ids (one or multiple devices) | {Dev-01} or {Dev-01,Dev-02} |
| to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* Response Tags

| Tag Name | Data Type | Description | Example |
| :---: | :---: | :---: | :---: |
| SCADAID | String | SCADA ID | 9bf9c31c-0ee9-4e1d-a415-e18b42ccfb9d |
| DevID | String | Device ID | MC-29 |
| Ts | Datetime | Timestamp of the data | 1539679347445 |
| Status | int | Device Status (0: OFF, 1: RUN, 2: IDLE, 3: DOWN) | 1 |
| AlmCode | dict | Object of Alarm code (Key: array number Value: code) | { "0" : "100","1" : "255","2" : "260",} |
| ServTemp | int | Servo Motor Temperature | 40.1 |
| ServTempX | int | Servo’s X-axis Temperature | 40.1 |
| ServTempY | int | Servo’s Y-axis Temperature | 40.1 |
| ServTempZ | int | Servo’s Z-axis Temperature | 40.1 |
| ServTempA | int | Servo’s A-axis Temperature | 40.1 |
| ServTempB | int | Servo’s B-axis Temperature | 40.1 |
| ServTempC | int | Servo’s C-axis Temperature | 40.1 |
| OvFeed | int | Cutting Feed Override 進給百分比 (%) | 100 |
| OvRapid | int | Rapid Feed Override 快動百分比 (%) | 100 |
| OvSpin | int | Spindle Override 主軸轉速百分比 (%) | 100 |
| MainPgm | String | Main Program | Program-001 |
| Mode | String | Mode | ex: “MDI”, “MEM”, ... |
