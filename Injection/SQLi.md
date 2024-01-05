# Lệnh quét
## Quét nhanh (bỏ qua các tuỳ chọn)
- Lệnh quét nhanh sẽ bỏ qua các tuỳ chọn được đưa ra trong quá trình quét, nhưng vẫn có thể thu về các thông tin cơ bản về lỗ hổng
- Câu lệnh sử dựng khi chưua có thông tin về mục tiêu
  
		sqlmap -u <http:/test.com/www/SQL/sql1.php> --forms --flush-session --answers='form=Y,fill blank fields=n,skip=Y,tests=N,follow=N,keep=N,quit=Y' --batch
	- 
## Quét toàn bộ
