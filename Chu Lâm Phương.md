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
    📋 Giải thích chi tiết các bước:
Code: Chỉnh sửa nội dung website trực tiếp trong file index.html.

Stage: Sử dụng git add để chọn các file thay đổi đưa vào Staging Area.

Commit: Sử dụng git commit để ghi lại phiên bản thay đổi vào Git history.

Push: Sử dụng git push origin gh-pages để gửi commit lên repository trên GitHub.

Deploy: GitHub Pages tự động phát hiện thay đổi và triển khai phiên bản mới từ nhánh gh-pages.

Verify: Mở URL website để kiểm tra giao diện và kiểm tra log nếu xuất hiện lỗi.

4.3. Trả Lời Câu Hỏi Tự Đánh Giá
❓ Câu 1: DevOps workflow tự động hóa những bước nào mà cách thủ công phải làm bằng tay?
Trả lời:
DevOps workflow tự động hóa các khâu Build (xây dựng), Test (kiểm thử) và Deploy (triển khai) thông qua GitHub Actions.

Khi lập trình viên đẩy code lên GitHub, workflow sẽ tự động kích hoạt theo các trigger đã thiết lập.

Nhờ đó, quy trình giảm thiểu tối đa thao tác thủ công, hạn chế rủi ro do con người và đảm bảo tính nhất quán trên các môi trường.

❓ Câu 2: Nếu deploy sai (website bị lỗi), làm sao để quay lại phiên bản cũ?
Trả lời:
Phương pháp an toàn nhất là sử dụng lệnh git revert:

Bash
# Đảo ngược thay đổi của commit gây lỗi
git revert <commit_hash>

# Push commit đảo ngược lên GitHub để kích hoạt lại pipeline
git push origin gh-pages
⚠️ Lưu ý: Tránh dùng git reset --hard trên các nhánh dùng chung (main, gh-pages) vì lệnh này làm thay đổi lịch sử commit và có thể gây mất dữ liệu hoặc xung đột cho các thành viên khác trong team.

❓ Câu 3: GitHub Actions pipeline giúp tiết kiệm bao nhiêu thời gian so với cách thủ công?
Trả lời:

Triển khai thủ công: Thường mất 15 – 30 phút (cho các bước nén file, FTP/SSH lên server, cấu hình web server, kiểm tra thủ công).

Triển khai tự động (GitHub Actions): Lập trình viên chỉ mất khoảng 10 giây để thực hiện lệnh push, thời gian còn lại do runner tự động thực thi.

Thời gian tiết kiệm ước tính: Khoảng 14 phút 50 giây – 29 phút 50 giây cho mỗi lần deploy.
    G -- Có --> H([Hoàn thành triển khai])
    G -- Không --> I[Kiểm tra cấu hình và log lỗi]
