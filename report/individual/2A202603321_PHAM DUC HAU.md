# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: PHẠM ĐỨC HẬU
- MSSV: 2A202603321
- Email: 26ai.haupd@vinuni.edu.vn
- Lớp: LAB E403
- Link repo bài làm: https://github.com/haudcph/K5-L2-DAY02-HAUPD-2A202603321-ObjectDetection
- Link Colab đã chạy:https://colab.research.google.com/drive/1cmrvfM53jp7tCBaJUTuoln5_Qg0gd6jW?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train:
- Kết quả checker và lỗi đã xử lý:
- Danh sách ít nhất 10 ảnh đã rà bằng mắt:
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
- Commit khóa nhãn ban đầu:

## 4. Gold QC và rework

| Chỉ số | Lần đầu (log ban đầu) | Hiện tại (chạy lại) |
|---|---:|---:|
| TP | 18 | 568 |
| FP | 995 | 450 |
| FN | 635 | 85 |
| Precision | 0.0178 | 0.5580 |
| Recall | 0.0276 | 0.8698 |
| F1 | 0.0216 | 0.6798 |
| mean_iou_of_matches | 0.8105 | 0.8196 |
| passed | false | false |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Cột “Lần đầu” lấy từ log đánh giá ban đầu; cột “Hiện tại” là kết quả chạy lại trên nhãn hiện có. Kết quả hiện tại vẫn chưa đạt ngưỡng F1 0.80. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do; không suy nguyên nhân chỉ từ FP/FN.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.7326 |
| Recall | 0.5790 |
| mAP50 | 0.6344 |
| mAP50–95 | 0.3954 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Truck có recall thấp nhất (0.371, trên 5 instances). drive_051.jpg
2. Kiểm tra độ khít và tọa độ/kích thước box so với ground truth. mAP50 khá cao (0.634) nhưng mAP50–95 thấp hơn đáng kể (0.395), gợi ý cần kiểm tra box lệch, quá rộng/hẹp hoặc chưa ôm sát vật thể ở các ngưỡng IoU cao.
3. Chưa thể kết luận lỗi class nào liên quan guideline chỉ từ bảng chỉ số. Cần xem các trường hợp dự đoán sai class trong từng ảnh, đối chiếu nhãn và quy tắc guideline, rồi ghi ảnh/vật thể làm bằng chứng.
4. Không dùng 10 ảnh eval để train để giữ tập đánh giá độc lập, tránh rò rỉ dữ liệu và có kết quả khách quan trên ảnh không dùng để cập nhật trọng số. Trong notebook, chúng đóng vai trò tập validation/eval để kiểm tra dự đoán và tính các chỉ số, không phải dữ liệu huấn luyện.



## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Gold QC và đối chiếu dự đoán | Gold QC chưa đạt (`passed: false`); các chỉ số FP/FN chưa đủ để xác định nguyên nhân. Khi rà soát, phát hiện nhãn truck, van và bus trong dữ liệu tham chiếu có trường hợp không khớp ảnh. | Đối chiếu ảnh gốc, box/class dự đoán, nhãn tham chiếu và quy tắc trong guideline; không sửa nhãn chỉ để tăng điểm. | Ghi nhận trường hợp nghi nhãn sai; cần xác minh từng ảnh, sửa nếu ảnh và schema xác nhận, rồi chạy checker và Gold QC lại. |

## 7. Tự đánh giá theo rubric

**Đánh giá:** Gold QC hiện `passed: false` (TP 568, FP 450, FN 85; precision 0.558, recall 0.8698, F1 0.6798, mean IoU 0.8196). Kết quả cho thấy bộ nhãn chưa qua kiểm tra; precision thấp hơn recall và IoU trung bình chưa đủ để kết luận nguyên nhân. Chưa thể khẳng định gold bị lỗi chỉ dựa trên các số này: FP/FN cũng có thể liên quan đến khác biệt giữa nhãn và dự đoán hoặc quy tắc ghép của evaluator.

**Cách xử lý:** xem các trường hợp FP/FN và match trong `outputs/annotation_evaluation.json`, mở ảnh gốc và đối chiếu từng box/class với schema, guideline. Ghi ảnh và lỗi cụ thể; chỉ sửa nhãn khi ảnh và quy tắc xác nhận nhãn sai, không sửa chỉ để tăng điểm. Sau đó chạy checker và Gold QC lại, lưu kết quả trước/sau và commit phiên bản nhãn đã kiểm tra. Nếu chưa làm các bước này, ghi rõ là chưa xác minh/chưa rework; không dùng gold chưa xác nhận để tuyên bố kết quả đánh giá cuối cùng.

Đối chiếu [RUBRIC.md](../../RUBRIC.md): khi đối chiếu dự đoán với ảnh, phát hiện nhãn truck, van và bus trong đề bị nhầm; các dự đoán được rà soát là đúng theo ảnh nhưng có thể bị tính sai do nhãn tham chiếu không khớp. 

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
