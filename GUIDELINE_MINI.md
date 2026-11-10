# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe chở người loại thông thường, thân xe con; không có khoang hàng hoặc khoang khách cỡ lớn đặc trưng của các lớp khác. | Sedan, hatchback, coupe, SUV/crossover. Phân biệt `van` bằng thân cao, khoang kín rộng và cửa trượt/cửa hậu đặc trưng. |
| `truck` | Xe thiết kế chủ yếu để chở hàng, có thùng hoặc sàn hàng rõ rệt; gồm xe tải nhỏ và xe tải nặng. | Xe tải thùng, xe ben, xe đầu kéo. Không nhầm với van chở hàng có thân kín liền khối, không có thùng/sàn hàng riêng. |
| `bus` | Xe thiết kế chủ yếu để chở nhiều hành khách, có khoang khách lớn và thường có nhiều hàng ghế. | Xe buýt đô thị, xe khách. Phân biệt `van` dựa vào kích thước và khoang khách; không dựa riêng vào màu sắc hay tuyến xe. |
| `van` | Xe thân cao, khoang kín liền khối, cỡ nhỏ hoặc trung bình, dùng chở người hoặc hàng; thường có cửa trượt bên hông hoặc cửa hậu lớn. | Minivan, van chở hàng. Nếu là xe chở nhiều hành khách cỡ lớn thì chọn `bus`; nếu có thùng/sàn hàng riêng biệt thì chọn `truck`. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: bao sát toàn bộ phần xe nhìn thấy, gồm các bộ phận thuộc xe; tránh lấy quá nhiều nền và không suy đoán phần khuất.
- Vật thể bị che khuất: gán nhãn nếu phần nhìn thấy đủ để nhận diện chắc chắn lớp; vẽ box quanh phần nhìn thấy, không bao gồm vật che khuất.
- Vật thể bị cắt bởi rìa ảnh: vẽ box đến đúng rìa ảnh và chỉ bao phần nằm trong ảnh; không ước lượng phần nằm ngoài khung.
- Vật thể rất nhỏ/mơ hồ: chỉ gán nhãn khi có đủ dấu hiệu nhận diện lớp; nếu không thể phân biệt chắc chắn giữa các lớp thì bỏ qua và ghi chú để self-QC, không đoán.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_001` | Xe con bị che một phần, nhưng vẫn thấy rõ thân xe | `car` | Phần nhìn thấy đủ nhận diện xe chở người thông thường; box chỉ bao phần xe nhìn thấy. |
| `drive_005` | Xe bị cắt ở mép ảnh, vẫn nhận ra thùng hàng riêng biệt | `car` | Cấu tạo đuôi xe thấp |
| `drive_012` | không phân biệt đc `van` với `car` do ảnh nhỏ hoặc bị khuất | Bỏ qua | Quyết định dựa vào kích thước và cấu tạo khoang theo schema; không dựa riêng vào màu sắc. |
