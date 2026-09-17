# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

- Mã học viên theo lớp: 2A202602262
- Ngày / CVAT local: 2026-09-17 / CVAT local
- Công cụ đã dùng: Mobile SAM

## 1. Bài đã nộp


| Task               | File ZIP đúng tên  | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| ------------------ | --------------------- | ---------------------: | --------------------------------: |
| easy_semantic      | `easy_semantic.zip`   |                  3 / 3 |                                20 |
| medium_instance    | `medium_instance.zip` |                  3 / 3 |                                32 |
| hard_panoptic      | `hard_panoptic.zip`   |                  2 / 2 |                                30 |
| cp1_holes          | `cp1_holes.zip`       |                  1 / 1 |                                 3 |
| cp2_slice          | `cp2_slice.zip`       |                  1 / 1 |                                 3 |
| cp5_occlusion      | `cp5_occlusion.zip`   |                  1 / 1 |                                 3 |
| cp3_thin           | `cp3_thin.zip`        |                  1 / 1 |                                 3 |
| cp4_curb           | `cp4_curb.zip`        |                  1 / 1 |                                 3 |
| cp6_coverage       | `cp6_coverage.zip`    |                  1 / 1 |                                 3 |
| **Tổng tối đa** |                       |                        |                           **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: chưa cung cấp
- Class và quy tắc tôi dùng để chọn biên: chưa cung cấp
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: chưa cung cấp
- Nếu không dùng gợi ý: chưa cung cấp

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: easy_semantic / các ảnh trong ZIP lần export đầu
- Lỗi thuộc loại: sai lớp
- Bằng chứng tôi nhìn thấy: ZIP chứa ảnh và class của medium_instance thay vì easy_semantic.
- Quy tắc và hành động sửa: Đối chiếu tên ảnh và classes.json của task, sau đó export lại đúng task.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.


| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| ------------- | ------------------------ | ------------------- | --------------------------------------- |
| `cp4_curb` / mép bó vỉa giữa lòng đường và vỉa hè | Mép bê tông sát lòng đường có thể thuộc `road` hoặc `sidewalk` vì màu và vật liệu gần nhau | Ranh được xác định theo chức năng sử dụng: phần xe chạy là `road`, phần dành cho người đi bộ là `sidewalk` | Gán phần lòng đường vào `road` và phần vỉa hè phía trong bó vỉa vào `sidewalk` |
| `cp3_thin` / biển báo và cột mảnh | Có thể bỏ sót các nét mảnh hoặc gán chúng vào `sky`/`road` do kích thước nhỏ | Chỉ gán phần vật thể nhìn thấy; dùng brush nhỏ và phóng to để giữ đúng đường viền | Gán cột/biển báo vào đúng class riêng, không mở rộng mask sang nền |
| `cp2_slice` / các xe cùng class đứng gần nhau | Có thể gộp nhiều xe thành một mask hoặc tách sai theo khoảng cách nhỏ giữa chúng | Mỗi xe là một instance riêng dù cùng class và đứng sát nhau | Tách từng xe thành mask riêng, không gộp các vùng chỉ vì cùng nhãn `car` |
