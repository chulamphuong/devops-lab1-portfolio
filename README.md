# devops-lab1-portfolio
Lab 1 — DevOps Course: My First CI/CD Pipeline
# 🚀 Báo Cáo Thực Hành: DevOps Workflow & CI/CD Pipeline

Báo cáo chi tiết so sánh quy trình triển khai ứng dụng giữa phương pháp truyền thống và quy trình DevOps tự động hóa, kèm sơ đồ luồng thực thi và giải đáp các câu hỏi kỹ thuật.

---

## 4.1. Bảng So Sánh DevOps vs. Truyền Thống

| Tiêu chí | Cách thủ công (Traditional) | Cách DevOps (CI/CD Pipeline) |
| :--- | :--- | :--- |
| **Làm sao để deploy?** | Lập trình viên tự sao chép file, tải mã nguồn lên máy chủ và cấu hình triển khai thủ công. | `git push` code lên GitHub $\rightarrow$ Pipeline tự chạy nếu đã cấu hình workflow phù hợp. |
| **Mất bao lâu?** | Phụ thuộc số bước thực hiện, thường mất vài phút hoặc lâu hơn. | Có thể mất vài giây đến vài phút, tùy pipeline và thời gian triển khai. |
| **Ai làm deploy?** | Lập trình viên hoặc quản trị viên thực hiện trực tiếp. | **GitHub Actions** tự động thực hiện các bước đã khai báo trong workflow. |
| **Có bị sai sót không?** | Dễ xảy ra lỗi do thao tác thủ công, cấu hình sai hoặc bỏ sót bước. | Giảm lỗi thao tác lặp lại nhờ quy trình tự động; vẫn có thể lỗi nếu code hoặc workflow sai. |
| **Rollback nếu lỗi?** | Khôi phục bản sao lưu hoặc triển khai lại phiên bản trước theo cách thủ công. | Dùng `git revert` rồi `push` để tạo bản sửa và kích hoạt triển khai lại. |
| **Kiểm tra thành công?** | Kiểm tra máy chủ, mở website hoặc xem log triển khai. | Xem trạng thái workflow và log trực tiếp trong tab **Actions** của GitHub. |

> 💡 **Nhận xét:** DevOps giúp tự động hóa quy trình triển khai, giảm thao tác lặp lại và dễ dàng truy vết lịch sử thay đổi. Tuy nhiên, hiệu quả thực tế phụ thuộc vào chất lượng kiểm thử (Test), cấu hình pipeline và quy trình xử lý sự cố.

---

## 4.2. Sơ Đồ DevOps Workflow Đã Thực Hành

Mô tả quy trình thực tế: Chỉnh sửa mã nguồn $\rightarrow$ Commit $\rightarrow$ Push lên nhánh `gh-pages` $\rightarrow$ Kiểm tra website.

```mermaid
flowchart TD
    A[1. Lập trình viên sửa index.html] --> B[2. git add index.html]
    B --> C[3. git commit -m 'Update portfolio']
    C --> D[4. git push origin gh-pages]
    D --> E[5. Mã nguồn cập nhật trên GitHub]
    E --> F[6. GitHub Pages triển khai website]
    F --> G{7. Website hoạt động tốt?}
    
    G -- Có --> H([Hoàn thành triển khai])
    G -- Không --> I[Kiểm tra cấu hình và log lỗi]
