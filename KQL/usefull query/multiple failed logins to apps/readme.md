```kql
SigninLogs
| where TimeGenerated > ago(48h)
// | where UserType == "Guest"
| where ResultType in ("53003", "50105", "50126","50055")
| summarize count()
            by AppDisplayName, UserPrincipalName, bin(TimeGenerated,30m)
| where count_ >=5
```
