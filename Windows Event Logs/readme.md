### Một số Event id liên quan đến hành vi đăng nhập:
```
4624 – Successful Logon
4625 – Failed Logon
4634 / 4647- Successful Logoff
4672 -Account logon with superuser rights (Administrator)
```

### Logon type code
```
2: Logon via a console (that is, using the keyboard)
3: Network logon (often using something like SMB for drive mapping)
4: Batch logon (Scheduled Tasks)- non-interactive
5: Windows Service logon- non-interactive
7: Lock or unlock of screen
8: Network logon sending credentials in cleartext (potentially indicative of a downgrade attack or older admin tool)
9: Different credentials used to authenticate than those currently logged on with (runas command or similar)
10: Remote interactive logon (Terminal Services/Remote Desktop Protocol)
11: Cached credentials used to log on due to system not in communication with the domain controller
12: Cached credentials used for a remote interactive logon (RDP). Previously rare, but now being seen when Microsoft “live” accounts are used for authentication on standalone workstations.
13: Cached credentials used for an unlock operation
```

### RDP (remote desktop protocol)

```
ID 4778 cho biết rằng một phiên RDP được bắt đầu
ID 4779 khi kết thúc một phiên
```

- Note: 
```
event ID 4624 gần như đồng thời với event ID 4778, tức là 1 session remote thành công và thêm đó là 1 lần xác thực (4624 với logon type 10), tương tự đó với event ID 4779 và ID 4647 (đăng xuất thành công).
```

```
Ngoài ra, còn một lưu ý nữa, đó là có thể kết hợp check thêm log Remote Desktop Services.

Event ID 131 trong log RDPCoreTS và Event ID 1149 trong log TerminalServices-RemoteConnectionManager ghi lại địa chỉ IP remote, user và ngày/giờ kết nối thành công.
```
