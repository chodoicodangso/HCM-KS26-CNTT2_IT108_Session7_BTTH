Phần 1: Đọc và định vị tệp tin  
Get-Content "logs\\server.log"  
Notepad nạp toàn bộ 500 MB vào RAM nên dễ tràn bộ nhớ và treo máy; PowerShell đọc theo luồng (stream/pipeline) từng dòng nên tốn rất ít RAM và mượt mà.  
Get-ChildItem \-Filter "\*.log" \-r  
Phần 2: Lọc dữ liệu và Pipe  
Get-Content "logs\\server.log" | Select-String "ERROR"  
Vị trí file: Get-ChildItem \-Filter "server.log" \-r  
Tìm lỗi 404 bên trong: Select-String \-Path "logs\\server.log" \-Pattern "404"  
Lệnh kết hợp Pipe: Get-Content "logs\\server.log" | Select-String "404"  
Get-ChildItem \-Filter "\*.log" \-Recurse | Get-Content | Select-String \-Pattern "INFO" \-NotMatch  
Phần 3: Toán tử chuyển hướng \> và \>\>  
Get-Content "logs\\server.log" | Select-String "404" \> "reports\\daily\_report.txt"  
Lệnh thêm dòng: "10:45:00 ERROR 404 Not Found /api/products" \>\> "reports\\daily\_report.txt"  
Dùng nhầm \> sẽ xóa sạch nội dung cũ của báo cáo thay vì ghi tiếp vào cuối file như \>\>.  
Phần 4: Shell Script và lệnh echo  
PowerShell  
Write-Output "Dang loc log..."  
Write-Output "=== LOG REPORT \===" \> "reports\\daily\_report.txt"  
Nội dung file scripts\\auto\_report.ps1:  
PowerShell  
\# Script tu dong loc loi 404 va tao bao cao hang ngay  
Write-Output "Bat dau tien trinh quet log..."  
Write-Output "=== LOG REPORT \===" \> "reports\\daily\_report.txt"  
Get-Content "logs\\server.log" | Select-String "404" \>\> "reports\\daily\_report.txt"  
Phần 5: Viết, chạy và thẩm định Script AI  
(a) Chạy script: .\\scripts\\auto\_report.ps1  
(b) Kiểm tra file: Get-Content "reports\\daily\_report.txt"  
(a) Dòng nguy hiểm: Remove-Item \-r \-Force C:\\\*. Hậu quả: Xóa sạch toàn bộ hệ điều hành, file hệ thống và dữ liệu ổ C, làm sập máy tính/server.  
(b) Sửa an toàn:  
PowerShell  
Remove-Item \-Path ".\\temp\\\*" \-r \-Force  
