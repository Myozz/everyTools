# SUDO_KILLER
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
