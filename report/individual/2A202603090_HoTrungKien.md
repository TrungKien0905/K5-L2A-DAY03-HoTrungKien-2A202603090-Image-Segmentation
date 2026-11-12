# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603090
- Ngày / CVAT local: 12/CVAT local
- Công cụ đã dùng: không có

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Tôi đã thực hiện gán nhãn cho các task dưới đây. Tình trạng Save và ZIP export cần đối chiếu trực tiếp với thư mục `submissions/` trước khi nộp.

| Task | File ZIP dự kiến | Hoàn thành mấy ảnh đã gán nhãn | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` (chưa xác nhận export) | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` (chưa xác nhận export) | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` (chưa xác nhận export) | 2 / 2 | 30 |
| cp1_holes | `cp1_holes.zip` (chưa xác nhận export) | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` (chưa xác nhận export) | 1 / 1 | 3 |
| cp5_occlusion | `cp5_occlusion.zip` (chưa xác nhận export) | 1 / 1 | 3 |
| cp3_thin | `cp3_thin.zip` (chưa xác nhận export) | 1 / 1 | 3 |
| cp4_curb | `cp4_curb.zip` (chưa xác nhận export) | 1 / 1 | 3 |
| cp6_coverage | `cp6_coverage.zip` (chưa xác nhận export) | 1 / 1 | 3 |
| **Tổng tối đa** | | **14 / 14 ảnh đã gán nhãn (theo thông tin người thực hiện)** | **100** |

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Chưa có thông tin xác định ảnh và object đầu tiên; cần đối chiếu lại Job `medium_instance`.
- Class và quy tắc tôi dùng để chọn biên: Gán class theo danh sách `person`, `bicycle`, `car`, `motorcycle`, `bus`, `truck`; mask chỉ bao phủ phần vật thể nhìn thấy, không gộp các vật thể cùng class đứng sát nhau.
- Việc dùng gợi ý tự động: Chưa xác nhận; không ghi nhận đã dùng hoặc đã sửa gợi ý khi không có bằng chứng.

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: `cp1_holes` — vùng xe máy Honda, đặc biệt khu vực kính, khe trong thân xe và giá đỡ bánh sau.
- Lỗi thuộc loại: Cân nhắc biên mask và vùng không thuộc vật thể.
- Bằng chứng tôi nhìn thấy: Giá đỡ bánh sau nằm bên ngoài cấu trúc xe; các vùng kính và khe bên trong xe cần áp dụng quy tắc không khoét lỗ tùy tiện.
- Quy tắc và hành động sửa: Đã rà soát mask cùng quy tắc CP1; cần xác nhận trên CVAT rằng giá đỡ được loại khỏi mask và các vùng kính/khe không bị khoét tùy tiện. Chưa có bằng chứng xác nhận đã chỉnh sửa xong.
- Sau sửa đã Save và export lại chưa? Chưa xác nhận.

Kết quả tự đánh giá GitHub Actions hoặc script: Chưa có điểm được cung cấp.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `hard_panoptic` — dải phân cách ở giữa mặt đường | Gán `road` hoặc để ngoài các class được gán | Bộ 12 class không có `median` hay `traffic island`; `sidewalk` chỉ phù hợp với vỉa hè | Không tự tạo class mới; cần coach xác nhận quy tắc cho dải phân cách nổi |
| `cp1_holes` — kính và khe bên trong xe Honda | Khoét lỗ hoặc giữ vùng này trong mask `motorcycle` | Hướng dẫn CP1 yêu cầu không khoét kính/khe tùy tiện | Giữ vùng kính/khe thuộc cấu trúc xe trong mask; phân biệt với nền thực sự bên ngoài vật thể |
| `cp3_thin` — nhiều cột trong một ảnh | Tạo label khác nhau cho từng cột hoặc dùng chung `pole` | Semantic segmentation phân loại theo pixel, không yêu cầu định danh từng cột | Dùng chung class `pole` cho tất cả cột thuộc lớp này; có thể tạo nhiều vùng mask cùng class |