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
  * [MInfo](MInfo.md)
  * [MCurrentStatusDuration](MCurrentStatusDuration.md)
  * [MAlarmCurrent](MAlarmCurrent.md)
* The following APIs return the RAW data trend within the time range
  * [MServoTempTrend](MServoTempTrend.md)
  * [MSpindleTempTrend](MSpindleTempTrend.md)
* The following API is return the Status Timeline of the selected devices
  * [SMStatusTimeline](SMStatusTimeline.md)