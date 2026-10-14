1. Làm cái gì? 
- sử dụng những lệnh đã học để tìm những lỗi TIMEOUT trong những file có đuôi .log

2,3. Phân tích + giải
- Để có thể lấy được ta sẽ sử dung những lệnh như get-content, select-string, và thuộc tính .count để có thể đếm được những lỗi TIMEOUT, ngoài ra ta sẽ dùng thêm lệnh where-object cùng cờ -notmatch để lọc những lỗi "NOT TIMEOUT" trên powershell.
- Trên git bash ta sẽ dung lệnh findstr, grep kết hợp với những cờ như -i -v để có  thể tìm được những lỗi TIMEOUT và lọc những lỗi "NOT TIMEOUT".
- Câu lệnh trên powershell: 
    (get-childitem *.log -r | select-string "TIMEOUT" | where-object { $_ -notmatch "NOT TIMEOUT"}).count
+ get-childitem *.log -r có nghĩa là chúng ta sẽ gọi hết tất cả những file và folder có đuôi là .log, không quan tâm tên file là gì chỉ cần file có tệp đuôi là .log thì sẽ gọi ra hết.
+ select-string "TIMEOUT" được sử dung để tìm những lỗi "TIMEOUT" trong tất cả các file có đuôi là .log
+ where-object { $_ -notmatch "NOT TIMEOUT"} được sử dung để lọc không đếm những dòng có biến là "NOT TIMEOUT".
+ thuộc tính .count dung để đếm số lỗi "TIMEOUT"
- Câu lệnh trên git bash: 
     find -type f -name *.log |xargs grep -i "TIMEOUT" | grep -v -i "NOT TIMEOUT"| wc -l
+ find -type f -name *.log có nghĩa là tìm những loại có thuộc tính là file có tên là *.log. *.log có nghĩa là lấy hết tất cả các file có đuôi là .log, không quan tâm trước đó nó là gì.
+ xargs grep -i "TIMEOUT" có nghĩa là nhận danh sách các output trước đó làm input cho lệnh tiếp theo, grep -i "TIMEOUT" có nghĩa là tìm những dòng có "TIMEOUT" không phân biệt hoa thường
+ grep -v -i "NOT TIMEOUT" có nghĩa là lọc tất cả các dòng không phân biệt hoa thường trừ dòng chữ "NOT TIMEOUT".
+ wc -l có tác dung để đếm số lỗi "TIMEOUT"

4. So sánh: 
- git bash và powershell có những câu lệnh tương đương nhau như: 
+ get-childitem <=> find
+ select-string <=> grep 
+ thuộc tính .count <=> wc -l
=> kết luận: git bash sử dung câu lệnh ngắn gọn và nhanh hơn powershell, powershell thì lại dễ tiếp cận hơn git bash.
