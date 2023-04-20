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

### Take/limit

```
SecurityEvent // The table
| where TimeGenerated > ago(1h) // Activity in the last hour
| where EventID == 4624 // Successful logon
| where AccountType =~ "user" // case insensitive
| limit 10 //random data sample or 10 records
```
Giới hạn số kết quả in ra là 10.

### count

```
SecurityEvent // The table
| where TimeGenerated > ago(1h) // Activity in the last hour
| where EventID == 4624 // Successful logon
| where AccountType =~ "user" // case insensitive
| count // Number of successful logons
```

Đếm số lượng account thỏa mãn các điều kiện trên.

Note: thường chúng ta không quan tâm đến số lượng successful logon(4624) mà quan tâm đến successful logon(4625).

### summarize


```
SecurityEvent // The input table
| where TimeGenerated > ago(1h) // Activity in the last hour
| where EventID == 4624 // Successful logon
| summarize count() by AccountType, Computer //Show the number of successful logons per computer and what type of account is being used
```

```
Tablename
| summarize Aggregation [by Group Expression]

Simple aggregation functions: count(), sum(), avg(), min(), max(),
Advanced aggregation functions: arg_min(), arg_max(), percentiles(), makelist(), countif()
```

### render
In ra kết quả theo dạng biểu đồ.

### extend
Thêm một cột dữ liệu vào

```
SecurityEvent
| extend My_Calculation = 8*8
| extend My_Fabricated_Data = "Yay for me!"
```
![image](https://user-images.githubusercontent.com/91442807/232989632-68fffd1b-832c-4d38-9a7d-0693fbcc959a.png)

Note: cái quan trọng của lệnh này là nó kết hợp các dự liệu ta thu thập được và hiển thi nó dưới dạng một cột mới.

### project
Chọn đúng cần những gì cần hiển thị

- project-away
```
Tablename 
| project-away column1, column2, column3*
```
Hiển thị tất cả các cột ngoài tự các cột ở trên.

### union
Kết hợp thông tin các bảng với nhau.

```
SecurityEvent //the table
| union Sec* //merging together all tables beginning with 'Sec'
| summarize count() by Computer //showing all computers from all tables and how many times they are referenced
| sort by Computer asc //displaying Computer names in ascending order
```

### join

Dùng để kết hợp hàng của 2 bảng dựa trên các trường chung.

Cú pháp:
```
LeftTable
|join [JoinParameters] (RightTable) onAttributes
```

Ví dụ:
```
SecurityEvent //table name
| join Heartbeat on Computer //joining SecurityEvent with Heartbeat on the common Computer column
| where EventID == "4688" //Looking for Event ID for new process
| project Computer, OSType, OSMajorVersion, Version //Displaying data from both table
```


