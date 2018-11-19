# 3.1.4 MSpindleTempTrend

## Information
* Get factory's Machine temperature information
* For M2I CNC domain, you can query the following tags in this API:
    * SpinTmp1 / SpinTmp2 
* Dependent on WISE-PaaS APM (need to create Group first in APM).
* After creating the Group tree in APM, input the Group path and device ID that you want to query.
* This API will return child nodes' infomation under the input parent node path.

## Format

* ### Request

  ```
  fns.MSpindleTempTrend("path", "device_id", "$from", "$to")
  ```

  | Variable | Data Type | Description | Example |
  | :--- | :--- | :--- | :---|
  | path | String | WISE-PaaS APM's Group tree path | /Advantech |
  | device_id | String | String of device id \(one or multiple devices\) | {Dev-01} or {Dev-01,Dev-02} |
  | $from | ISODate String | Grafana Start time variable or ISO Date String | $from or "2018-10-01T00:00:00:000Z" |
  | $to | ISODate String | Grafana End time variable or ISO Date String | $to or "2018-10-10T00:00:00:000Z" |

* ### Response Tags

  | Tag Name | Data Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | TempName | String | Query tag name | "SpinTmp1" |
  | TempValue | Int | Temperature value or Ov value | 75 |
  | Ts | Datetime | Timestamp of the data | 1539679347445 |    

  
* ### Example
    1. Display the Servo temperature trend 
        - Query   
        ``` 
        select TempName as metric, TempValue, Ts from fns.MSpindleTempTrend("$Group","$Machine",   "$from", "$to" )  
        ```
        - Return Data Format   
            * timeseries
        - Query Time Type   
            * utc
        - Panel Type   
            * Datatable Panel
        - Panel Screenshot      
            ![](/images/3.1.4-MSpindleTempTrend.jpg)

        - Return Value Example    
            ``` json
            [
              {
                "datapoints": [
                  [
                    28, 
                    1542585172504
                  ], 
                  [
                    28, 
                    1542585212568
                  ], 
                  [
                    28, 
                    1542585242617
                  ], 
                  [
                    23, 
                    1542586056592
                  ], 
                  [
                    23, 
                    1542586076624
                  ], 
                  [
                    22, 
                    1542587932366
                  ], 
                  [
                    22, 
                    1542588092639
                  ], 
                  [
                    24, 
                    1542589455264
                  ], 
                  [
                    24, 
                    1542589465296
                  ], 
                  [
                    29, 
                    1542590196751
                  ], 
                  [
                    29, 
                    1542590206767
                  ], 
                  [
                    27, 
                    1542591759761
                  ], 
                  [
                    27, 
                    1542591920034
                  ], 
                  [
                    32, 
                    1542594026975
                  ], 
                  [
                    32, 
                    1542594359131
                  ], 
                  [
                    30, 
                    1542595463166
                  ], 
                  [
                    30, 
                    1542595833761
                  ], 
                  [
                    30, 
                    1542595903874
                  ], 
                  [
                    30, 
                    1542595913890
                  ], 
                  [
                    28, 
                    1542596216044
                  ], 
                  [
                    28, 
                    1542596326221
                  ], 
                  [
                    28, 
                    1542596386318
                  ], 
                  [
                    28, 
                    1542596396334
                  ], 
                  [
                    28, 
                    1542596446414
                  ], 
                  [
                    28, 
                    1542596656752
                  ], 
                  [
                    28, 
                    1542596666784
                  ], 
                  [
                    28, 
                    1542596676800
                  ], 
                  [
                    28, 
                    1542597609718
                  ], 
                  [
                    27, 
                    1542598532010
                  ], 
                  [
                    27, 
                    1542598552042
                  ], 
                  [
                    27, 
                    1542598622155
                  ], 
                  [
                    27, 
                    1542598662219
                  ], 
                  [
                    27, 
                    1542598712300
                  ], 
                  [
                    29, 
                    1542599784334
                  ], 
                  [
                    29, 
                    1542599804366
                  ], 
                  [
                    28, 
                    1542604872115
                  ], 
                  [
                    28, 
                    1542604882131
                  ], 
                  [
                    31, 
                    1542605934242
                  ], 
                  [
                    31, 
                    1542605944258
                  ], 
                  [
                    31, 
                    1542605954274
                  ], 
                  [
                    31, 
                    1542605964290
                  ], 
                  [
                    32, 
                    1542607096452
                  ], 
                  [
                    33, 
                    1542607336947
                  ], 
                  [
                    33, 
                    1542607346963
                  ], 
                  [
                    33, 
                    1542607366996
                  ], 
                  [
                    33, 
                    1542607467156
                  ], 
                  [
                    33, 
                    1542607657462
                  ], 
                  [
                    32, 
                    1542608638835
                  ], 
                  [
                    32, 
                    1542608769060
                  ], 
                  [
                    36, 
                    1542611853109
                  ], 
                  [
                    36, 
                    1542611873141
                  ], 
                  [
                    36, 
                    1542613215390
                  ], 
                  [
                    36, 
                    1542613285503
                  ], 
                  [
                    35, 
                    1542614076305
                  ], 
                  [
                    35, 
                    1542614216530
                  ]
                ], 
                "target": "SpinTmp1"
              }
            ]

            ```
