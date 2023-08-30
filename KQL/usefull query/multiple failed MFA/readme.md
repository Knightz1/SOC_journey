```kql
// let privusers=
//     IdentityInfo
//     | where TimeGenerated > ago(21d)
//     | summarize arg_max(TimeGenerated, *) by AccountUPN
//     | where isnotempty(AssignedRoles)
//     | where AssignedRoles != "[]"
//     | distinct AccountUPN;
SigninLogs
| where TimeGenerated > ago(30d)
| where ResultType == "500121"
// | where UserPrincipalName in (privusers)
| mv-expand todynamic(AuthenticationDetails)
| extend ['MFA Failure Type'] = tostring(parse_json(AuthenticationDetails).authenticationStepResultDetail)
| where ['MFA Failure Type'] startswith "MFA denied"
// | distinct ['MFA Failure Type']
| summarize
    ['MFA Failure Count']=count(),
    ['MFA Failure Reasons']=make_list(['MFA Failure Type'])
    by UserPrincipalName, bin(TimeGenerated, 20m)
| where ['MFA Failure Count'] >= 5
```
