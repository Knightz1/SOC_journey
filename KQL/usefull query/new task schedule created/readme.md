```kql
SecurityEvent
| where TimeGenerated > ago(30d)
| where EventID == "4698"
| extend  Event_data = parse_xml( EventData)
| extend task_name = Event_data.EventData.Data[4].["#text"]
| extend task_content = Event_data.EventData.Data[5].["#text"]
| project TimeGenerated, task_name, task_content
```
