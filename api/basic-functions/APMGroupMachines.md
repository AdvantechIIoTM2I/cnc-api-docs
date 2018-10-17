# 3.1.5 APMGroupMachines

## Information

* Get Machine Names which binded in WISE-PaaS APM Group
* Return machine name belong to input path

## Format

* ### Request

  ```
  APMGroupMachine("path")
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path | /Advantech/Taipei |

* ### Response 
  * Format: Array of machine name
  * Example:
  ``` 
  [
  "MachineName1", 
  "MachineName2"
  ]
  ```

* ### Example

  * Edit Variable in WISE-PaaS Setting     
  * Variable attributes:   
    * Name: "your variable Name"   
    * Type: Query   
    * Data Source: Simple SQL Data Source with api-m2icnc-generic URL   
    * Query:  
      ```
      APMGroupMachine("$Group")
      ```
    * Screenshot   
      ![](/images/3.1.5-APMGroupMachine-setting.jpg)
  * Check if the the Machine name is displayed in "Preview of values"
