# Real-time Machine Info APIs
---

## Information
* Real-time Machine Info APIs return RAW Data of target machines, which includes:
  * Machine ID/Name/Description
  * Machine Status
  * Spindle / Servo Temperatures
  * Alarm information
  * Machine Program / Mode
  * Cutting / Rapid / Spindle Override   
  
* The following APIs return the latest record of the selected devices.
  * [MInfo](api/3.1_machine_info_funcs/MInfo.md)
  * [MCurrentStatusDuration](api/3.1_machine_info_funcs/MCurrentStatusDuration.md)
  * [MAlarmCurrent](api/3.1_machine_info_funcs/MAlarmCurrent.md)
* The following APIs return the RAW data trend within the time range
  * [MServoTempTrend](api/3.1_machine_info_funcs/MServoTempTrend.md)
  * [MSpindleTempTrend](api/3.1_machine_info_funcs/MSpindleTempTrend.md)
* The following API is return the Status Timeline of the selected devices
  * [SMStatusTimeline](api/3.1_machine_info_funcs/SMStatusTimeline.md)