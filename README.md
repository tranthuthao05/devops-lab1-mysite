# devops-lab1-mysite

## Thông tin sinh viên
- **Họ và tên:** Trần Thu Thảo
- **MSV:** DTC235180168
- **Lớp:** KTPM-K22B
- **Website:** https://tranthuthao05.github.io/devops-lab1-mysite/



## Bước 4: So sánh DevOps vs Truyền thống

### 4.1 Bảng so sánh

| Tiêu chí | Cách THỦ CÔNG (Traditional) | Cách DEVOPS (CI/CD Pipeline) |
|---|---|---|
| **Làm sao để deploy?** | Tải file về máy, upload lên server/hosting bằng FTP hoặc thao tác tay, rồi cấu hình lại | Push code lên GitHub → pipeline tự động chạy và deploy |
| **Mất bao lâu?** | Khoảng 15-30 phút mỗi lần | Khoảng 10 giây |
| **Ai làm deploy?** | Con người (dev hoặc sysadmin) làm bằng tay | GitHub Actions (máy tự làm) |
| **Có bị sai sót không?** | Có: dễ quên file, upload nhầm, cấu hình lệch giữa các lần | Không đáng kể: pipeline chạy cùng một quy trình mỗi lần |
| **Rollback nếu lỗi?** | Tìm bản backup rồi upload lại bằng tay, dễ nhầm bản | `git revert` + push → pipeline tự deploy lại bản cũ |
| **Làm sao biết deploy thành công?** | Tự mở website kiểm tra bằng mắt | Tab Actions hiển thị ✅ hoặc ❌ |

### 4.2 Sơ đồ workflow

```mermaid
flowchart LR
    A[Sửa code<br/>VS Code] --> B[git push]
    B --> C[GitHub Actions]
    C --> D[Checkout Code]
    D --> E[Validate HTML]
    E --> F[Deploy]
    F --> G[Nhánh gh-pages]
    G --> H[Website live<br/>*.github.io]
```
### 4.3 Trả lời câu hỏi

**1. DevOps workflow tự động hóa những bước nào mà cách thủ công phải làm bằng tay?**

Ba bước chính: **build, kiểm tra (test) và deploy**.
- Kiểm tra: pipeline tự chạy bước *Validate HTML* để xác nhận `index.html` tồn tại.
- Deploy: pipeline tự đẩy code lên nhánh `gh-pages`, không cần tải file hay upload thủ công.
- Các bước này chạy tự động mỗi khi `git push`, không cần con người can thiệp.

**2. Nếu deploy sai (website bị lỗi), làm sao để quay lại phiên bản cũ?**

- Dùng `git revert <mã commit>` để tạo commit đảo ngược thay đổi lỗi, rồi `git push`.
- Pipeline tự chạy lại và deploy phiên bản cũ lên website.
- Cách khác: `git reset --hard <mã commit>` rồi push, nhưng cách này ghi đè lịch sử nên `git revert` an toàn hơn.

**3. GitHub Actions pipeline đã giúp bạn tiết kiệm bao nhiêu thời gian so với cách thủ công?**

- **Thủ công:** tải file → upload lên server → cấu hình → kiểm tra, mất khoảng **15-30 phút** mỗi lần.
- **DevOps:** chỉ cần `git push`, pipeline hoàn tất trong khoảng **10 giây**.
- Tiết kiệm phần lớn thời gian, và không còn nguy cơ upload thiếu hoặc nhầm file.
