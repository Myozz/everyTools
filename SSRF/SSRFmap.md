- SSRF thường bị lợi dụng để thực hiện leo quyền trên một số dịch vụ khác. Framework này nhắm tới việc tìm và khai thác những dịch vụ này một cách dễ dàng. SSRPmap dùng Burp request như là input và một tham số để thực hiện
# Các Modules
- Option ```-m``` cho phép sử dụng các module: ![image](https://github.com/Myozz/everyTools/assets/94811005/ff51c2a1-5c67-426a-b1a2-aa2a6b6c8543)
# Các Option
- ```-r REQFILE```: Chỉ định file request (có thể lấy từ Burp)
- ```-p PARAM```: Tham số SSRF nhắm tới (thường thì là url) ![image](https://github.com/Myozz/everyTools/assets/94811005/44cde476-7c55-4994-b5be-9784e9f0feba)
- ```-m MODULE```: Như đề cập ở phần trước, chọn các chức năng
- ```-l HANDLER```: Tạo một Handler xử lý cho một reverse shell
- ```-v VERBOSE```: Mức độ chi tiết của thông tin trả về
- ```lhost LHOST``` và ```lport LPORT```: LHOST và LPORT reverse shell
- ```--rfiles FILE```: File để đọc với module readfile
- ```--uagent USERAGENT```: User Agent để sử dụng
- ```--ssl [SSL]```: Sử dụng HTTPS mà không xác minh
- ```--proxy PROXY```: Sử dụng HTTPs proxy
- ```--level [LEVEL]```: Level test (default là 1)
