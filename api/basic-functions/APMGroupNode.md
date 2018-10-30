# 3.1.4 APMGroupNode

## Information

* Get WISE-PaaS APM Group Node name
* Return the child nodes of input PATH node

## Format

* ### Request

  ```
  APMGroupNode("path")
  ```

  | Variable | Data Type | Description | Example |
  | :---: | :---: | :---: | :---: |
  | path | String | WISE-PaaS APM's Group tree path | /Advantech/Taipei |

* ### Response 
  * Format: Array of Child node name
  * Example:
  ```  json
  [
  "NodeName1", 
  "NodeName2"
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
      APMGroupNode("$Group")
      ```
    * Screenshot   
      ![](/images/3.1.4-APMGroupNode-setting.jpg)
  * Check if the the Child node name is displayed in "Preview of values"
