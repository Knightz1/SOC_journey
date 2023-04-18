### Ví dụ đơn giản

```
SecurityEvent 
| where TimeGenerated  > ago (1h)        // thời gian tạo cách đây trên 1 h
| where EventID == 4624                 // EventID= 4624
| summarize count() by Account          // muốn tạo một bảng tổng các Account có EventID và thời gian tạo như trên
| order by Account asc                  // sắp xếp theo thứ tự tăng dần trong bảng chữ cái
| project Account , SuccessfulLogons = count_   // chọn thông tin muốn hiển thị ra là Account và SuccessfulLogons
```

### Liệt kế các loại thông tin
Ví dụ
```
OfficeActivity
| getschema
```
![image](https://user-images.githubusercontent.com/91442807/232831977-9b6746c0-0f67-43ff-aee6-c44419e5ee58.png)


### Where opearator

```
Allowable predicates:

String predicates: ==, has, contains, startswith, endswith, matches regex, etc
Numeric/Date predicates: ==, !=, <, >, <=, >=
Empty predicates: isempty(), notempty(), isnull(), notnull()
```

ex:
```
SecurityEvent // The table
| where TimeGenerated > ago(1h) // Activity in the last hour
| where EventID == 4624 // Successful logon
| where AccountType =~ "user" // case insensitive
```


