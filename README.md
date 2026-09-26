🔐 HỆ THỐNG XÁC THỰC NGƯỜI DÙNG - MINISUPERMARKET

Môn học: Lập trình Ứng dụng .NET Core
Mã môn: 229162
Buổi thực hành: Authentication - Xây dựng Web API xác thực người dùng và kết nối WinForms Client

🏗️ 1. Mô hình Kiến trúc Hệ thống

Dự án được xây dựng theo mô hình Client - Server, tách biệt giữa Backend và Frontend:

MiniSupermarket.API (Backend): Dự án ASP.NET Core Web API chịu trách nhiệm xử lý xác thực người dùng, kiểm tra thông tin đăng nhập và cung cấp các API phục vụ Authentication.

MiniSupermarket.WinForms (Frontend Client): Ứng dụng Windows Forms đóng vai trò là client, gửi thông tin đăng nhập đến Web API và hiển thị kết quả xác thực cho người dùng.

Luồng hoạt động:

┌──────────────────────────┐
│   MiniSupermarket        │
│       WinForms            │
│        Client             │
└────────────┬─────────────┘
             │
             │ HTTP Request
             ▼
┌──────────────────────────┐
│   MiniSupermarket.API    │
│      ASP.NET Core        │
│        Web API           │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Authentication / User    │
│      Validation          │
└──────────────────────────┘

🛠️ 2. Công nghệ Sử dụng

Ngôn ngữ: C#

Framework: .NET 8.0

Backend: ASP.NET Core Web API

Frontend: Windows Forms .NET 8.0

Authentication: Xác thực người dùng thông qua API

HTTP Client: HttpClient, System.Net.Http.Json

API Testing: Swagger UI

Data: In-Memory Data / dữ liệu phục vụ thực hành

📂 3. Cấu trúc Solution
MiniSupermarketSystem/
│
├── MiniSupermarket.API/              # Backend Web API
│   ├── Controllers/
│   │   └── AuthController.cs         # API đăng nhập/xác thực
│   │
│   ├── Models/
│   │   └── User.cs                   # Model người dùng
│   │
│   └── Program.cs                    # Cấu hình Web API
│
└── MiniSupermarket.WinForms/         # Frontend Client
    ├── FormLogin.cs                  # Giao diện đăng nhập
    └── ApiClientService.cs            # Gọi API Authentication


Tên file có thể thay đổi tùy theo cấu trúc thực tế của project.

🔐 4. Chức năng Authentication

Hệ thống tập trung vào chức năng xác thực người dùng:

Đăng nhập

Người dùng nhập:

Tên đăng nhập

Mật khẩu

WinForms gửi thông tin đến Web API thông qua HTTP request.

API thực hiện kiểm tra thông tin tài khoản và trả về kết quả xác thực.

Ví dụ:

POST /api/auth/login


Request:

{
  "username": "admin",
  "password": "123456"
}


Response thành công:

{
  "success": true,
  "message": "Đăng nhập thành công"
}


Response thất bại:

{
  "success": false,
  "message": "Tên đăng nhập hoặc mật khẩu không chính xác"
}

🔄 5. Luồng xử lý đăng nhập
Người dùng
    │
    │ Nhập Username + Password
    ▼
WinForms Client
    │
    │ POST /api/auth/login
    ▼
ASP.NET Core Web API
    │
    │ Kiểm tra tài khoản
    ▼
Authentication
    │
    ├── Hợp lệ ──────► Đăng nhập thành công
    │
    └── Không hợp lệ ► Thông báo lỗi

🚀 6. Hướng dẫn Chạy và Kiểm thử Dự án
Bước 1: Chạy Backend

Mở Solution bằng Visual Studio 2022.

Nhấp chuột phải vào project:

MiniSupermarket.API


Chọn:

Set as Startup Project


Nhấn F5 để chạy Web API.

Trình duyệt sẽ mở Swagger UI.

Tại Swagger, có thể kiểm tra API Authentication, ví dụ:

POST /api/auth/login

Bước 2: Kiểm thử API bằng Swagger

Trong Swagger:

Tìm endpoint đăng nhập.

Chọn POST /api/auth/login.

Nhấn Try it out.

Nhập thông tin username và password.

Nhấn Execute.

Kiểm tra HTTP Status Code và Response.

Bước 3: Chạy WinForms Client

Đảm bảo địa chỉ API trong HttpClient hoặc ApiClientService khớp với địa chỉ Web API đang chạy.

Ví dụ:

https://localhost:XXXXX


Sau đó:

Nhấp chuột phải vào project MiniSupermarket.WinForms.

Chọn Debug → Start new instance.

Nhập username và password.

Nhấn Đăng nhập.

Kiểm tra kết quả xác thực từ Web API.

🧪 7. Các trường hợp kiểm thử
STT	Trường hợp	Kết quả mong đợi
1	Username và password đúng	Đăng nhập thành công
2	Username sai	Thông báo tài khoản không tồn tại
3	Password sai	Thông báo mật khẩu không chính xác
4	Bỏ trống username	Thông báo yêu cầu nhập username
5	Bỏ trống password	Thông báo yêu cầu nhập password
📌 8. Kết quả đạt được

Sau khi hoàn thành bài thực hành, hệ thống có thể:

Xây dựng Web API bằng ASP.NET Core .NET 8.

Tạo API phục vụ Authentication.

Tiếp nhận và kiểm tra thông tin đăng nhập.

Kết nối ứng dụng WinForms với Web API bằng HttpClient.

Kiểm thử API thông qua Swagger UI.

Xử lý kết quả đăng nhập từ Backend trên Client.

👨‍💻 9. Tác giả

Họ tên sinh viên: Huỳnh Nhật Lâm

Mã sinh viên: 2124110334

Lớp học phần: CCQ2411C