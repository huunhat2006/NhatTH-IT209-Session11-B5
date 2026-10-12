# Bài 5: Nối Job tự động Build & Push Docker Image sau khi Test Gradle xanh

Thư mục này chứa tệp cấu hình CI/CD (`.github/workflows/ci.yml`) sử dụng GitHub Actions, nhằm tạo một luồng pipeline với 2 Job riêng biệt có liên kết thứ tự.

## Mô tả cấu trúc Workflow (`ci.yml`)
Workflow này bao gồm 2 Job chính:
1. **`test`**: 
   - Nhiệm vụ: Cài đặt JDK, cấp quyền và chạy lệnh `./gradlew test`.
   - Mục đích: Đảm bảo code vượt qua các bài kiểm thử (JUnit Test) trước khi sang bước tiếp theo.
2. **`docker-build`**:
   - Nhiệm vụ: Đăng nhập vào GitHub Container Registry và dùng `docker/build-push-action@v5` để build/push Docker Image lên ghcr.io.
   - Tính năng nối Job: Sử dụng chỉ thị `needs: test` để Job này chỉ được kích hoạt nếu Job `test` hoàn tất thành công (màu xanh). Nếu Job `test` thất bại, Job `docker-build` sẽ tự động chuyển trạng thái thành **Skipped**.

## Sản phẩm nộp bài
- Tệp kịch bản `.github/workflows/ci.yml` (đã được tạo sẵn trong thư mục này).
- **Lưu ý**: Bạn cần chụp ảnh màn hình biểu đồ **Workflow trên tab Actions** hiển thị sơ đồ kết nối thành công giữa 2 Job (Mũi tên chỉ từ `test` sang `docker-build`) để nộp bài.
