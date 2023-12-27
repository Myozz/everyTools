------------------ADVANCED COMMAND-------------------
# Target:
- **-u URL**: Chỉ định URL mục tiêu
- **-d DIRECT**: Chỉ định trực tiếp vào CSDL mục tiêu
  - **VD**: -d DBMS://DATABASE_FILEPATH
- **-l LOGFILE**: Phân tích mục tiêu từ proxy log file của Burp hay WebScarab
- **-m BULKFILE**: Scan đa mục tiêu từ một file chứa các URL (mỗi dòng một URL)
- **-r REQUESTFILE**: Load HTTP Request từ một file (có thể là HTTP hay HTTPs)
- **-g GOOGLEDORK**: Lấy thông tin thu được từ Google Dork làm các URL mục tiêu
  - **VD**: -g "inurl:test.com intext:admin"
- **-c CONFIGFILE**: Sử dụng các tuỳ chọn trong config file
  - **VD**: ![image](https://github.com/Myozz/everyTools/assets/94811005/30edc653-3b18-41ce-b33c-92210326e19d)


# Request:
  -A: User-agent header (VD: Mozilla/5.0 (Windows NT 10.0; Win64; x64)...)
	-H: Header phụ (VD: X-forwarđe-for: 127.0.0.1)
	--method=<METHOD>: Bắt buộc sử dụng HTTP method được chỉ định (VD: PUT, GET,...)
	--data=DATA: Data string được gửi qua POST (VD: id=1)
	--param-del=<PARA>: Kí tự được sử dụng để phân chia giá trị tham số
	--cookie=COOKIE: Giá trị của HTTP Cookie header
	--random-agent: Sử dụng HTTP User-Agent header ngẫu nhiên
	--proxy=<PROXY>: Sử dụng một proxy để kết nối tới mục tiêu
	--tor: Dùng mạng ẩn danh tor
 
# Optimization
  -o: Bật tất cả các lựa chọn optimization
	--predict-output: Dự đoán kết quả truy vấn
	--keep-alive: Sử dụng các kết nối HTTP liên tục
	--null-connection: Thu thập độ dài trang mà không cần nội dung HTTP thực tế
	--threads=THREADS: Số lượng HTTP request đồng thời tối đa

# Injection:
  -p: Chỉ định những tham số có thể test
	--skip=<SKIP>: Bỏ qua việc test những tham số được chỉ định
	--skip-static: Bỏ qua việc test những tham số tĩnh
	--param-exclude=<PARA>: Ngoại trừ một tham số được chỉ định khỏi quá trình kiểm tra
	--param-filter=<PARA>: Chọn tham só có thể test (VD: POST)
	--dbms=DMMS: Chỉ định loại dtb được sử dụng (VD: MySQL)
	--dbms-cred=DBMS: Cung cấp thông tin xác thực	
	--os=OS: Chỉ định OS của mục tiêu
	--invalid-bignum: Sử dụng những số lớn cho các giá trị không hợp lệ
	--invalid-logical: Sử dụng các phép logic cho các giá trị không hợp lệ
	--invalid-string: Sử dụng các string ngẫu nhiên cho các giá trị không hợp lệ
	--no-cast: Tắt cơ chế truyền payload
	--no-escape: Tắt cơ chế thoát chuỗi
	--tamper=TAMPER: Sử dụng script để xáo trốn các injection data
	--level=LEVEL: Độ sâu của test
	--risk=RISK: Mức độ rủi rỏ (rủi co càng cao -> thành công càng cao
	--string=<STRING>: Xác định một chuỗi, sqlmap sẽ tìm chuỗi đó trong response để xác định truy vấn trả về đúng hay sai
	--not-string=<NOT_STR>: Ngược lại 
	--regexp=REGEXP: Sử dụng biểu thức chính quy để kiểm tra phản hồi đúng/sai
  --crawl: Mức độ thu thập thông tin <1/2/3/4> (độ sâu vào các path con
  --technique: có 5 năm mode
