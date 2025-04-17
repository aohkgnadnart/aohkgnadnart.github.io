---
title: "Cách chuyển đổi tài khoản github nhanh chóng để push commit"
---

# Problem
khi có nhiều tài khoản github, việc push commit đúng tài khoản là vấn đề.
# Solution
## GitHub CLI
Dưới đây là hướng dẫn cơ bản để sử dụng GitHub CLI (gh) nhằm đăng nhập, kiểm tra trạng thái, và chuyển đổi giữa các tài khoản GitHub:

---

### 1. Cài đặt GitHub CLI

- **Tải và cài đặt:**  
  Truy cập trang chính thức của GitHub CLI tại [cli.github.com](https://cli.github.com/) để tải và cài đặt phiên bản phù hợp với hệ điều hành của bạn.

---

### 2. Đăng nhập vào tài khoản GitHub

- **Sử dụng lệnh đăng nhập:**  
  Mở terminal và chạy lệnh:
  ```bash
  gh auth login
  ```
  Lệnh này sẽ hướng dẫn bạn chọn giữa đăng nhập qua web hoặc nhập token. Bạn có thể chọn đăng nhập qua web để tiện lợi:
  - Chọn “GitHub.com” khi được hỏi.
  - Chọn “Web browser” để mở trình duyệt và xác thực.
  - Sau khi xác thực thành công, terminal sẽ thông báo bạn đã đăng nhập thành công.

- **Ví dụ đăng nhập:**
  ```bash
  $ gh auth login
  ? What account do you want to log into? GitHub.com
  ? What is your preferred protocol for Git operations? HTTPS
  ? Authenticate Git with your GitHub credentials? Yes
  - Opening https://github.com/login/device in your browser...
  ```
  
---

### 3. Kiểm tra trạng thái đăng nhập

- **Xem tài khoản hiện tại:**  
  Sử dụng lệnh:
  ```bash
  gh auth status
  ```
  Lệnh này sẽ hiển thị thông tin tài khoản hiện đang đăng nhập cùng với các scopes được cấp phép.

---

### 4. Chuyển đổi giữa các tài khoản

Nếu bạn có nhiều tài khoản GitHub, bạn có thể chuyển đổi theo các bước sau:

- **Đăng xuất khỏi tài khoản hiện tại:**  
  ```bash
  gh auth logout
  ```
  Lệnh này sẽ đăng xuất bạn khỏi tài khoản đang đăng nhập. Bạn sẽ được hỏi xác nhận đăng xuất.

- **Đăng nhập vào tài khoản khác:**  
  Sau khi đăng xuất, chạy lại lệnh:
  ```bash
  gh auth login
  ```
  Và thực hiện quá trình đăng nhập như hướng dẫn ở bước 2 với tài khoản mong muốn.


---

### Tóm lại

- **Đăng nhập:** Sử dụng `gh auth login` để đăng nhập.
- **Kiểm tra trạng thái:** Dùng `gh auth status` để xem tài khoản hiện tại.
- **Chuyển đổi tài khoản:** Đăng xuất bằng `gh auth logout` rồi đăng nhập lại với tài khoản khác.

Với GitHub CLI, bạn có thể dễ dàng quản lý và chuyển đổi giữa các tài khoản GitHub mà không cần phải thay đổi nhiều cấu hình thủ công.

---

Tham khảo thêm tài liệu chính thức của GitHub CLI tại [docs.github.com/en/cli](https://docs.github.com/en/cli) để biết thêm chi tiết.

