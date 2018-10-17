# 3.1.3 APMGroup

## Information

* Get WISE-PaaS APM Group Name List
* Can be used for creating WISE-PaaS Dashboard Variable

## Format

* ### Request

  ```
  APMGroup()
  ```

* ### Response 
  * Format: Array of Group Name
  * Example:
  ``` 
  [
  "GroupName1", 
  "GroupName2"
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
      APMGroup()
      ```
    * Screenshot   
      ![](/images/3.1.3-APMGroup-setting.jpg)
  * Check if the the Group Name is displayed in "Preview of values"
