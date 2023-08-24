```kql
  SecurityEvent
  | where EventID == 4657     / a register value was modified
  | extend EventData = parse_xml(EventData).EventData.Data
  | mv-expand bagexpansion=array EventData
  | evaluate bag_unpack(EventData)
  | extend Key = tostring(column_ifexists('@Name', "")), Value = column_ifexists('#text', "")
  | evaluate pivot(Key, any(Value), TimeGenerated, TargetAccount, Computer, EventSourceName, Channel, Task, Level, EventID, Activity, TargetLogonId, SourceComputerId, EventOriginId, Type, _ResourceId, TenantId, SourceSystem, ManagementGroupName, IpAddress, Account)
  | extend ObjectName = column_ifexists('ObjectName', ""), OperationType = column_ifexists('OperationType', ""), ObjectValueName = column_ifexists('ObjectValueName', "")
  | where ObjectName has 'Schedule\\TaskCache\\Tree' and ObjectValueName == "SD" and OperationType == "%%1906"  // %%1906 - Registry value deleted
  | extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = Account
```
