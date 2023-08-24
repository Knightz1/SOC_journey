```kql
Event
| where TimeGenerated > ago(90d)
| where EventID == 7040
| extend service = parse_xml(EventData).DataItem.EventData.Data[0].["#text"]
| extend status = parse_xml(EventData).DataItem.EventData.Data[2].["#text"]
| where status =~ "disabled"
| summarize make_list(service) by Computer
```
