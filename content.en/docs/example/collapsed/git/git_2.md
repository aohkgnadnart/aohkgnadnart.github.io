---
title: "Cách xóa hoàn toàn một commit khỏi lịch sử"
---
Để xóa hoàn toàn một commit khỏi lịch sử (biến mất không dấu vết), bạn sẽ cần phải **viết lại lịch sử commit** của nhánh bằng cách sử dụng lệnh **git reset** hoặc **git rebase -i** rồi **force push** lên remote. Dưới đây là các bước cụ thể:

# 1. Sử dụng **git reset** (nếu commit cần loại bỏ là commit cuối cùng hoặc gần cuối)
- **Bước 1:** Xác định commit trước commit bạn muốn loại bỏ. Giả sử bạn muốn xóa commit cuối cùng, bạn có thể đưa nhánh về commit trước đó:
  ```bash
  git reset --hard HEAD~1
  ```
- **Bước 2:** Sau đó, force push thay đổi lên remote:
  ```bash
  git push origin <branch-name> --force
  ```
  *Lưu ý:* Việc sử dụng `--force` sẽ ghi đè lịch sử trên remote, vì vậy hãy chắc chắn rằng không có ai khác đang làm việc trên nhánh đó.

# 2. Sử dụng **git rebase -i** (nếu commit cần xóa nằm giữa lịch sử commit)
- **Bước 1:** Chạy rebase tương tác bắt đầu từ commit ngay trước commit cần loại bỏ:
  ```bash
  git rebase -i <commit-hash>^
  ```
  Trong đó, `<commit-hash>` là mã của commit bạn muốn loại bỏ.
- **Bước 2:** Trong trình soạn thảo, tìm dòng chứa commit đó và thay đổi từ `pick` thành `drop` (hoặc xóa dòng đó).
- **Bước 3:** Lưu và thoát trình soạn thảo để hoàn thành rebase.
- **Bước 4:** Sau đó, force push lên remote:
  ```bash
  git push origin <branch-name> --force
  ```
# 3. Sự khác biệt --force và --force-with-lease
Cả hai tùy chọn đều dùng để ép buộc ghi đè lịch sử commit trên remote, nhưng chúng khác nhau ở chỗ:

- **--force:**  
  - Khi sử dụng, Git sẽ ghi đè trực tiếp lên remote mà không kiểm tra sự thay đổi của người khác.  
  - Nếu có người khác đã đẩy commit mới lên remote, bạn có thể vô tình ghi đè và làm mất dữ liệu của họ.

- **--force-with-lease:**  
  - Tùy chọn này an toàn hơn vì Git sẽ kiểm tra trước xem remote có thay đổi nào không so với lần đẩy cuối cùng của bạn.  
  - Nếu remote đã được cập nhật (ví dụ: có commit của người khác), lệnh sẽ từ chối push để bảo vệ dữ liệu.  
  - Chỉ khi remote vẫn giữ nguyên trạng thái như lần bạn lấy về (fetch) thì push sẽ được thực hiện.

Tóm lại, **--force-with-lease** là lựa chọn an toàn hơn khi cần ghi đè, giúp tránh việc vô tình ghi đè commit của người khác trên remote.
