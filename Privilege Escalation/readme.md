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

- 
