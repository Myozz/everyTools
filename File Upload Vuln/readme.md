# Tool fuxploider
- Link: [https://github.com/almandin/fuxploider](https://github.com/almandin/fuxploider)
- Đây là một công cụ có khả năng phát hiện lỗ hổng bằng cách thử tải lên mục tiêu các payload, và kiểm tra xem chúng có thể thực thi hay không
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

    
