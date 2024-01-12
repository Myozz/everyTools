![image](https://github.com/Myozz/everyTools/assets/94811005/c2dc88fc-a1fe-469c-a348-69606061cfca)# Tool fuxploider
- Link: [https://github.com/almandin/fuxploider](https://github.com/almandin/fuxploider)
- Đây là một công cụ có khả năng phát hiện lỗ hổng bằng cách thử tải lên mục tiêu các payload, và kiểm tra xem những extension nào có thể sử dụng để khai thác
## Một số tuỳ chọn 
### Tuỳ chọn bắt buộc
- ```--url```: Chỉ định URL mục tiêu
- ```--not-regex <REGEX>```: Cung cấp thông báo upload không thành công
- ```--true-regex <REGEX>```: Cung cấp thông báo upload thành công
### Tuỳ chọn khác
- ```--data <DATA>```: Cung cấp dữ liệu bổ sung qua cho phương thức POST. VD: ```--data "arg1=val1&arg2=val2"
- ```--filesize <INTEGER>```: Kích thước file được sử dụng để tạo và upload (đơn vị KB)
- ```--cookies <COOK>```: Cung cấp cookie, thường được sử dụng khi gặp lỗi cần xác thực trước khi chuyển tới URL
- ```--uploads-path <PATH>```: Đương dẫn nới chứa các dữ liệu được upload
- ```--template TEMP```: Chọn các payload mẫu để thực hiện kiểm thử
  - **phpinfo**: file php đơn giản để lấy phpinfo()
  - **nastgif**: file GIF lấy phpinfo()
  - **nastyjpg**: file JGP lấy phpinfo()
  - **basicjsp** file jsp với với các biểu thức toán học đơn giản
- ```--legit-extensions```: Chỉ định file extension dùng cho payload (VD: php, jpg,..)
- ```-v```, ```-vv``` và ```-vvv```: Mức độ chi tiết của dữ liệu khi thực hiện lệnh
- ```--skip-recon```: Bỏ qua bước recon (ở bước này fuxploider sẽ xác định file extensions nào có thể sử dụng). Bắt buộc kết hợp cùng ```--legit-extension```
- ```-y```: Buộc tìm lỗ hổng trên mọi điểm đầu vào cho tới khi thực thi thành công
- ```--user-agent <AGENT>```: Chỉ định user-agent cho request
- ```-m```: Tắt tự động tìm upload form, sử dụng khi tool không thể phát hiện upload form. Tuỳ chọn này sẽ đi cùng với các tuỳ chọn dưới đây: (sẽ đề cập lại ở phần cách khai thác)
  - ```--input-name <INP_NAME>```: Tên tham số được sử dụng cho đầu vào dữ liệu
  - ```--form-action <PATh>```: Đường dẫn của form action
 
## Sử dụng fuxploider để khai thác lỗ hổng File Upload
- Dưới đây là một ví dụ sử dụng fuxploider để khai thác
- Đây là một upload form cho phép upload hầu hết các định dạng file ![image](https://github.com/Myozz/everyTools/assets/94811005/004890e4-0f1d-4fff-a67c-866bf721e639)
- Câu lệnh dùng để khai thác sẽ là:

      python fuxploider.py -u "http://localhost/vulnerabilities/upload/" --true-regex "succesfully uploaded" -m --input-name "uploaded" --form-action "/vulnerabilities/upload/" --cookies "PHPSESSID=dp0g758u3ofhub7r3p8btiefm5; security=low" --uploads-path "/hackable/uploads/" --data "Upload=Upload" --skip-recon -l php
- Phân tích câu lệnh trên:
  - ```-u "http://localhost/vulnerabilities/upload/"```: Chỉ định mục tiêu là đường dẫn được cung cấp
  - ```--true-regex "succesfully uploaded"```
    - Cung cấp thông báo khi upload thành công, để lấy được thông báo này ta có thể thử upload một file hợp lệ lên mục tiêu. Khi đó thông báo upload thành công sẽ hiện lên
    - Nếu không ta có thể sử dụng ```--not-regex``` để cung cấp thông báo lỗi
    - ```-m```: Vì không thể tự phát hiện form nên tuỳ chọn này sẽ được sử dụng
      - ![image](https://github.com/Myozz/everyTools/assets/94811005/e1419abf-83c5-4792-bb8f-a403e0e9fea9)
      - ```--input-name "uploaded"```: Thông tin này có thể lấy từ Page Source
      - ```--form-action "/vulnerabilities/upload/"```: Thông tin này chỉ đơn giản là đường dẫn của form
    - ```--cookies "PHPSESSID=dp0g758u3ofhub7r3p8btiefm5; security=low"```: Như đã đề cập ở trên, khi gặp trường hợp phải xác thực trước truy cập vào login thì ta cần cung cấp cookies cho fuxploider. Có thể lấy cookie từ Request ![image](https://github.com/Myozz/everyTools/assets/94811005/5f0049ba-6a27-496f-adff-55d947a77f35)
    - ```--uploads-path /hackable/uploads```: Là đường dẫn mà sẽ lưu trữ những dữ liệu mà ta sẽ upload lên đó, ở đây đường dẫn là ```localhost/hackable/uploads```
    - ```data Upload=Upload```: Cung cấp thêm thông tin của upload form, ở đây ta đang cung cấp thông tin của nút upload ![image](https://github.com/Myozz/everyTools/assets/94811005/36951e0d-3ba3-48ba-a766-53f25ae2b1ea)
    - ```--skip-recon -l php```: Cung cấp thông tin rẳng có thể upload file php, bỏ qua kiểm tra
- Kết quả: ![image](https://github.com/Myozz/everyTools/assets/94811005/68feb399-da6d-4175-9677-6523a21ff6bb)

# Tool filepwner
- Link: [https://github.com/artemixer/filepwner?tab=readme-ov-file](https://github.com/artemixer/filepwner?tab=readme-ov-file)
- Là một công cụ có chức năng tương tự với fuxploider. Nhưng thay vì chỉ upload được những template có sẵn thì filepwner cho phép ta khả năng tuỳ chính tốt hơn cũng nhưng đơn giản hơn khi sử dụng file request thay vì phải cung cấp từng thông tin 
## Các tuỳ chọn
- ```-r <FILE>```: Chỉ định request file
- ```-t <TRUE>```: Cung cấp thông báo upload thành công
- ```-f <FALSE>```: Cung cấp thông báo upload lỗi
- ```-a <EXTENSION>```: Chỉ định các extension sẽ được dùng để upload
- ```--rate-limit <RATE>```: Tuỳ chỉnh khoảng thời gian (giây) giữa 2 request
- ```-d <DIR>```: Cung cấp path mà dữ liệu upload sẽ được lưu trữ
- ``` -v 1/2/3```: Mức độ chi tiết của đữ liệu trả về
- ```--timeout```: Số giây chờ trước khi thông báo Request Timeout
- ```--status-codes <CODE>```: Cung cấp HTTP Status Code khi upload thành công (mặc định 200)
- ```--protocol```: Cung cấp giao thức được sử dụng cho upload (mặc định HTTPs)
- ```--enable-redirects```: Nếu được bật, cho phép form chuyển hướng request
- ```--manual-check```: Nếu được bật, sẽ tạm dừng thực thi sau mỗi lần upload shell thành công
- ```--disable-modules <MOD>```: Tắt module chỉ định (mimetype_spoofing, double_extension, double_extension_random_case, 
reverse_double_extension, null_byte_cutoff,name_overflow_cutoff, htaccess_overwrite)
## Tuỳ chỉnh
- Các tuỳ chỉnh của filepwner năm ở trong file ```config.py``` ![image](https://github.com/Myozz/everyTools/assets/94811005/00e098ce-2b7a-45e7-a1f7-eace3dc8d420)
## Cách sử dụng
- Tiếp tục sử dụng DVWA để kiểm thử ![image](https://github.com/Myozz/everyTools/assets/94811005/4961e660-4b20-41b4-a6ab-04fc26d22e0f)
- Command có thể sử dụng ở đây

      python filepwner.py -r burp -t "succesfully uploaded" -d "/hackable/uploads/" --protocol http
  - ```-r burp``` sẽ chỉ định file burp sử dụng cho Request
    - Đoạn Request có thể lấy nhanh từ một cố công cụ như Burp, ZAP
    - Hoặc ta cũng có thể lấy thủ công qua Inspect trên trình duyệt
      - Lấy Request Header: ![image](https://github.com/Myozz/everyTools/assets/94811005/c3410764-e0d4-4c02-a47b-9ccd8ef99946)
      - Lấy Request Payload: ![image](https://github.com/Myozz/everyTools/assets/94811005/ca2e35d2-7e70-4b76-899d-9317e1443747)
      - Ghép 2 thành phần trên thành một file và chỉnh sửa các tham số của filename và nội dung file thành ```*filename*``` và ```*content*``` ![image](https://github.com/Myozz/everyTools/assets/94811005/af863c6a-caf1-47e3-b788-d36be021604d)
    - ```-t "succesfully uploaded"```: Tương tự true-regex của fuxploider
    - ```-d "/hackable/uploads/"```: Tương tự upload-path của fuxploider
    - ```--protocol http```: Chỉ định Request là http (mặc định là https)
- Kết quả: ![image](https://github.com/Myozz/everyTools/assets/94811005/4e0bc88c-7d1d-410c-8600-3094fe4b8aed)

# Tool Upload-Bypass
- Link: [https://github.com/sAjibuu/Upload_Bypass?tab=readme-ov-fileƯ](https://github.com/sAjibuu/Upload_Bypass?tab=readme-ov-file)
- Là một phiển bản nguyên thuỷ hơn của filepwn nhưng do công cụ này thường upload các payload có extension là .com nên không thể kiểm tra tính thực thi của payload được (Điều này có lẽ sẽ được giải quyết nếu chỉnh sửa lại mã nguồn)
## Tuỳ chọn
- Vẫn mang các tuỳ chọn như filepwner, tuy nhiên vẫn có những chức năng khá nổi bật
  - **Webshell mode**: Công cụ sẽ thử upload một Webshell với tên ngẫu nhiên, và nếu upload-path được chỉ định thì công cụ sẽ thực hiện upload shell
  - **Eicar mode** (```--eicar```): Công cụ sẽ thử upload một Anti-Mailware test file thay vì một Webshell. Nếu upload-path được chỉ định, công cụ sẽ kiểm tra xem file có upload thành công và tồn tại trên hệ thống hay không để xác định nếu hệ thống có Anti-Mailware
  - **Output**: Khi thực hiện test xong sẽ lưu lại directory của file được upload cùng tên host dưới dạng file Text hay Excel (có thể chỉ định đường dẫn bằng ```-o```)
  - ```--insecure```: Công cụ sẽ bỏ qua TLS/SSL cert
  - ```--resume <STATE>```: Cung cấp một file trạng thái để tiếp tục scan hoàn chỉnh (.json)
