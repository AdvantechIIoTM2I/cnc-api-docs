# 3.7.1 MTempMonitoring

## Information
* Get factory's Machine temperature information
* For M2I CNC domain, you can query the following tags in this API:
    * SpinTmp1 / SpinTmp2
    * ServTemp0 / ServTemp1 / ... / ServTemp11
    * OvFeed / OvSpin / OvRapid
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the Group path and device ID that you want to query.
* This API will return child nodes' infomation under the input parent node path.

## Format

* ### Request

  ```
  fns.MTempMonitoring("path", "device_id",  "tag_name", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path | /Advantech |
  | device_id | String | String of device id \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | tag_name | String | tag name that you want to query, such as <br> - SpinTmp1 / SpinTmp2  <br>- ServTemp0 / ServTemp1 / ... / ServTemp11<br>-  OvFeed / OvSpin / OvRapid)  | "SpinTmp1" |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | TempName | String | Query tag name | "SpinTmp1" |
  | TempValue | Int | Temperature value or Ov value | 75 |
  | Ts | Datetime | Timestamp of the data | 1539679347445 |    
  | Duration | float | DownTime duration (second) | 200.9 |

  
* ### Example
    1. Display the temperature trend of 4 different tags
        - Query   
          * Use 4 queries for this panel    
            * Note:   
                * Use "select 'xxxx' as metric" to specify the Display Legend Name of these data 
        ``` 
        select SpinTmp1 as metric, TempValue, Ts from fns.MTempMonitoring("$Group","$Machine", "SpinTmp1", "$from", "$to" )    
        select ServTemp0 as metric, TempValue, Ts from fns.MTempMonitoring("$Group","$Machine", "ServTemp0", "$from", "$to" )    
        select ServTemp1 as metric, TempValue, Ts from fns.MTempMonitoring("$Group","$Machine", "ServTemp1", "$from", "$to" )    
        select ServTemp2 as metric, TempValue, Ts from fns.MTempMonitoring("$Group","$Machine", "ServTemp2", "$from", "$to" )   
        ```
        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Datatable Panel
        - Panel Screenshot      
            ![](/images/3.7.1-MTempMonitoring.jpg)

        - Return Value Example    
            ``` json
            [
              {
                "datapoints": [
                  [
                    21, 
                    1541116406326
                  ], 
                  [
                    21, 
                    1541116406326
                  ], 
                  [
                    21, 
                    1541116406326
                  ], 
                  [
                    21, 
                    1541116406326
                  ], 
                  [
                    21, 
                    1541116406326
                  ], 
                  [
                    21, 
                    1541116406326
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127009442
                  ], 
                  [
                    21, 
                    1541127079530
                  ], 
                  [
                    21, 
                    1541127079530
                  ], 
                  [
                    21, 
                    1541127079530
                  ], 
                  [
                    21, 
                    1541127079530
                  ], 
                  [
                    21, 
                    1541127079530
                  ], 
                  [
                    21, 
                    1541127079530
                  ], 
                  [
                    21, 
                    1541127079530
                  ], 
                  [
                    23, 
                    1541138354492
                  ], 
                  [
                    23, 
                    1541138354492
                  ], 
                  [
                    23, 
                    1541138354492
                  ], 
                  [
                    23, 
                    1541138354492
                  ], 
                  [
                    23, 
                    1541138354492
                  ], 
                  [
                    23, 
                    1541138354492
                  ], 
                  [
                    23, 
                    1541138354492
                  ], 
                  [
                    23, 
                    1541138354492
                  ], 
                  [
                    23, 
                    1541138354492
                  ]
                ], 
                "target": "SpinTmp1"
              }, 
              {
                "datapoints": [
                  [
                    32, 
                    1541116406326
                  ], 
                  [
                    32, 
                    1541116606542
                  ], 
                  [
                    32, 
                    1541118169525
                  ], 
                  [
                    32, 
                    1541118369779
                  ], 
                  [
                    32, 
                    1541118879302
                  ], 
                  [
                    32, 
                    1541118939387
                  ], 
                  [
                    32, 
                    1541120510279
                  ], 
                  [
                    32, 
                    1541120530318
                  ], 
                  [
                    32, 
                    1541121320027
                  ], 
                  [
                    32, 
                    1541121330042
                  ], 
                  [
                    32, 
                    1541123349688
                  ], 
                  [
                    32, 
                    1541123379734
                  ], 
                  [
                    32, 
                    1541124159430
                  ], 
                  [
                    32, 
                    1541124169443
                  ], 
                  [
                    32, 
                    1541126199334
                  ], 
                  [
                    32, 
                    1541126238451
                  ], 
                  [
                    32, 
                    1541127009442
                  ], 
                  [
                    32, 
                    1541127079530
                  ], 
                  [
                    32, 
                    1541127109570
                  ], 
                  [
                    32, 
                    1541127119585
                  ], 
                  [
                    32, 
                    1541129099145
                  ], 
                  [
                    32, 
                    1541129139200
                  ], 
                  [
                    32, 
                    1541129918670
                  ], 
                  [
                    32, 
                    1541129968732
                  ], 
                  [
                    32, 
                    1541129998773
                  ], 
                  [
                    32, 
                    1541130008787
                  ], 
                  [
                    32, 
                    1541131992235
                  ], 
                  [
                    32, 
                    1541135244142
                  ], 
                  [
                    32, 
                    1541136023799
                  ], 
                  [
                    32, 
                    1541136073879
                  ], 
                  [
                    32, 
                    1541136743119
                  ], 
                  [
                    32, 
                    1541136763141
                  ], 
                  [
                    32, 
                    1541138334464
                  ], 
                  [
                    32, 
                    1541138354492
                  ]
                ], 
                "target": "ServTemp0"
              }, 
              {
                "datapoints": [
                  [
                    49, 
                    1541116406326
                  ], 
                  [
                    49, 
                    1541116606542
                  ], 
                  [
                    32, 
                    1541118169525
                  ], 
                  [
                    32, 
                    1541118369779
                  ], 
                  [
                    36, 
                    1541118879302
                  ], 
                  [
                    36, 
                    1541118939387
                  ], 
                  [
                    40, 
                    1541120510279
                  ], 
                  [
                    40, 
                    1541120530318
                  ], 
                  [
                    41, 
                    1541121320027
                  ], 
                  [
                    41, 
                    1541121330042
                  ], 
                  [
                    42, 
                    1541123349688
                  ], 
                  [
                    42, 
                    1541123379734
                  ], 
                  [
                    44, 
                    1541124159430
                  ], 
                  [
                    44, 
                    1541124169443
                  ], 
                  [
                    45, 
                    1541126199334
                  ], 
                  [
                    45, 
                    1541126238451
                  ], 
                  [
                    45, 
                    1541127009442
                  ], 
                  [
                    45, 
                    1541127079530
                  ], 
                  [
                    45, 
                    1541127109570
                  ], 
                  [
                    45, 
                    1541127119585
                  ], 
                  [
                    48, 
                    1541129099145
                  ], 
                  [
                    48, 
                    1541129139200
                  ], 
                  [
                    48, 
                    1541129918670
                  ], 
                  [
                    48, 
                    1541129968732
                  ], 
                  [
                    48, 
                    1541129998773
                  ], 
                  [
                    48, 
                    1541130008787
                  ], 
                  [
                    48, 
                    1541131992235
                  ], 
                  [
                    51, 
                    1541135244142
                  ], 
                  [
                    51, 
                    1541136023799
                  ], 
                  [
                    51, 
                    1541136073879
                  ], 
                  [
                    49, 
                    1541136743119
                  ], 
                  [
                    49, 
                    1541136763141
                  ], 
                  [
                    51, 
                    1541138334464
                  ], 
                  [
                    51, 
                    1541138354492
                  ]
                ], 
                "target": "ServTemp1"
              }, 
              {
                "datapoints": [
                  [
                    28, 
                    1541116406326
                  ], 
                  [
                    28, 
                    1541116606542
                  ], 
                  [
                    28, 
                    1541118169525
                  ], 
                  [
                    28, 
                    1541118369779
                  ], 
                  [
                    28, 
                    1541118879302
                  ], 
                  [
                    28, 
                    1541118939387
                  ], 
                  [
                    28, 
                    1541120510279
                  ], 
                  [
                    28, 
                    1541120530318
                  ], 
                  [
                    28, 
                    1541121320027
                  ], 
                  [
                    28, 
                    1541121330042
                  ], 
                  [
                    28, 
                    1541123349688
                  ], 
                  [
                    28, 
                    1541123379734
                  ], 
                  [
                    28, 
                    1541124159430
                  ], 
                  [
                    28, 
                    1541124169443
                  ], 
                  [
                    28, 
                    1541126199334
                  ], 
                  [
                    28, 
                    1541126238451
                  ], 
                  [
                    28, 
                    1541127009442
                  ], 
                  [
                    28, 
                    1541127079530
                  ], 
                  [
                    28, 
                    1541127109570
                  ], 
                  [
                    28, 
                    1541127119585
                  ], 
                  [
                    28, 
                    1541129099145
                  ], 
                  [
                    28, 
                    1541129139200
                  ], 
                  [
                    28, 
                    1541129918670
                  ], 
                  [
                    28, 
                    1541129968732
                  ], 
                  [
                    28, 
                    1541129998773
                  ], 
                  [
                    28, 
                    1541130008787
                  ], 
                  [
                    28, 
                    1541131992235
                  ], 
                  [
                    28, 
                    1541135244142
                  ], 
                  [
                    28, 
                    1541136023799
                  ], 
                  [
                    28, 
                    1541136073879
                  ], 
                  [
                    28, 
                    1541136743119
                  ], 
                  [
                    28, 
                    1541136763141
                  ], 
                  [
                    28, 
                    1541138334464
                  ], 
                  [
                    28, 
                    1541138354492
                  ]
                ], 
                "target": "ServTemp2"
              }
            ]
            ```
