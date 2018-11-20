# 3.3.1 MAlarmCategoryCount

## Information

* Get device’s alarm categories of level information in each category
* Support one / multiple devices


## Format

* ### Request

  ```
  fns.MAlarmCategoryCount("path", "device_id",  "level", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path<br>where the device belongs to | /Advantech/Taipei |
  | device_id | String | String of device ids \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | level | String | String of alarm code level<br>"0" = Critical level<br>"1" = Warning level | "0" |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

  - **Note:**
    - 'path' can be empty string if you want to query all devices with the same name of "device_id"
    - 'device_id' can be empty string if you want to query all devices under the specified 'path'
  

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | Level | string | Input alarm code level | "0" |
  | Category* | int | Number of alarm in this category | 20 |
  
  - Note:
    - Category: Can be any string defined in the Alarm code definition of this machine.  
      For example, if one device's alarm code definition contains 7 categories:
        - Electric
        - Controller
        - Axes
        - Spindle
        - Magazine/ATC
        - Oil/Air/Water
        - Peripheral
    - The Response Tags would be as follow:

        | Tag Name | Data Type | Description | Example |
        | :--- | :--- | :--- | :--- |
        | Level | string | Input alarm code level | "0" |
        | Electric | int | Number of alarm (Electric category) | 20 |
        | Controller | int | Number of alarm (Controller category) | 20 |
        | Axes | int | Number of alarm (Axes category) | 20 |
        | Spindle | int | Number of alarm (Spindle category)| 20 |
        | Magazine/ATC | int | Number of alarm (Magazine/ATC category) | 20 |
        | Oil/Air/Water | int | Number of alarm (Oil/Air/Water category)| 20 |
        | Peripheral | int | Number of alarm (Peripheral category) | 20 |

* ### Example  
    1. Query Alarm Categories of multiple device within a path
        - Query   
        ``` sql
        select Level as metric, Electric, Controller, Axes, Spindle, 'Magazine/ATC', 'Oil/Air/Water', 'Peripheral'  
        from fns.MAlarmCategoryCount("$Group/$Factory/$Line/$Category", "",  "0", "$from", "$to") 
        ```
        - Return Data Format   
            * table
        - Query Time Type   
            * utc
        - Panel Type   
            * Radar Chart
        - Panel Screenshot      
            ![](/images/3.3.1-MAlarmCategoryCount-Radar.jpg)

        - Return Value Example    
            ``` json
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
                            "text": "Electric", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Controller", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Axes", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Spindle", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Magazine/ATC", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Oil/Air/Water", 
                            "type": "number"
                        }, 
                        {
                            "sqltype": "int", 
                            "text": "Peripheral", 
                            "type": "number"
                        }
                    ], 
                    "rows": [
                        [
                            "0", 
                            0, 
                            17, 
                            12, 
                            1, 
                            1, 
                            1, 
                            2
                        ]
                    ], 
                    "type": "table"
                }
            ]

            ```
