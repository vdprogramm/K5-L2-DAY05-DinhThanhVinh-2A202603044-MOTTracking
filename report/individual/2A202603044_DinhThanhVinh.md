Báo cáo cá nhân – MOT Tracking
Bài thực hành: Lab Ngày 5 – Multi-Object Tracking
Video: MOT17-09 · Số frame: 150 (frame 1–150)
Nguồn dữ liệu: MOTChallenge · Giấy phép: CC BY-NC-SA 3.0

0. Thông tin học viên
Thông tin	Nội dung
Họ và tên	Đinh Thành Vinh
MSSV	2A202603044
Mã đề	A
Email	dinhthanhvinhnb205@gmail.com
Repository	K5-L2-DAY05-DinhThanhVinh-2A202603044-MOTTracking
Giờ bắt đầu	4:00 PM
Giờ kết thúc	12:00 AM


1. Xem trước đoạn video (CP0)
Ghi nhận đặc điểm từng đối tượng trước khi tiến hành gán nhãn.
Mã	Frame xuất hiện	Frame cuối thấy được	Rẽ / dừng / đổi tốc độ	Bị che khuất	Ghi chú
P1	0	149	Di chuyển đều suốt đoạn, hơi đổi góc nhẹ quanh frame 70–76	Không bị che	Xuất hiện xuyên suốt toàn bộ 150 frame
P2	0	149	Đổi tốc độ và hướng quanh frame 45–57 và cuối đoạn 143–149	Bị che nhiều đoạn (tổng 52 frame), khuất hẳn ở 42–44	Bị người đi ngang che khuất thoáng qua
P3	0	147	Chuyển hướng trước khi khuất (frame 105) và sau khi hiện lại (137–143)	Bị che 16 frame, khuất hẳn từ frame 111 đến 136	Biến mất hoàn toàn 26 frame rồi xuất hiện lại
P4	60	149	Bắt đầu vào khung hình ở frame 60, đổi hướng và tốc độ liên tục từ frame 64–146	Bị che khuất một phần ở 40 frame	Xuất hiện muộn từ giữa video (frame 60)
P5	0	149	Đổi hướng, tốc độ và kích thước box liên tục từ frame 60 đến 149	Bị che khuất một phần ở 64 frame	Đi qua khu vực đông người, bị che khuất và đổi hướng nhiều nhất


2. Keyframe và thời gian (CP1, CP4)
Số lượng keyframe được lấy từ kết quả chạy src/check_submission.py.
Mã	Số keyframe	Số frame có mặt	Keyframe / 100 frame	Thời gian (phút)	Chỗ khó
P1	19	150	12.7	12	Giữ box ôm sát toàn thân khi sải bước ở đoạn giữa
P2	25	147	17.0	18	Bị che khuất nhiều lần và mất hẳn ở frame 42–44
P3	14	122	11.5	15	Đoạn khuất hẳn kéo dài 26 frame (111–136), phải canh lại đúng vị trí khi hiện lại
P4	35	90	38.9	20	Xuất hiện từ frame 60, tốc độ và kích thước box thay đổi liên tục khi tiến lại gần
P5	69	150	46.0	25	Bị che khuất tới 64 frame và liên tục đổi hướng, tốc độ nên nội suy tuyến tính dễ bị trôi
Tổng	162	659	24.6	90	—


<details>
<summary><strong>Chi tiết frame đặt keyframe của từng đối tượng</strong></summary>- P1 (19 keyframe): 0, 10, 20, 30, 40, 50, 60, 70, 72, 76, 80, 90, 100, 110, 120, 130, 140, 142, 149
- P2 (25 keyframe): 0, 20, 30, 40, 45, 46, 47, 51, 52, 53, 54, 55, 57, 75, 84, 94, 104, 114, 124, 134, 143, 144, 145, 146, 149
- P3 (14 keyframe): 0, 10, 20, 30, 40, 50, 105, 137, 138, 139, 140, 141, 142, 143
- P4 (35 keyframe): 60, 64, 66, 67, 68, 69, 71, 72, 74, 77, 79, 80, 81, 86, 88, 93, 98, 99, 100, 101, 104, 110, 113, 120, 121, 123, 125, 126, 133, 135, 140, 142, 143, 144, 146
- P5 (69 keyframe): 0, 10, 20, 30, 40, 50, 60, 62, 64, 65, 68, 69, 70, 71, 72, 76, 77, 79, 81, 82, 83, 84, 87, 88, 91, 92, 94, 96, 98, 99, 100, 101, 102, 104, 105, 106, 107, 108, 109, 113, 114, 115, 116, 117, 118, 119, 120, 121, 122, 123, 125, 126, 127, 128, 129, 130, 132, 133, 135, 138, 139, 140, 141, 142, 143, 144, 145, 148, 149
</details>Cách tính mật độ keyframe:
\[
\text{Keyframe / 100 frame}
= \frac{\text{Tổng keyframe}}{\text{Tổng frame có mặt}} \times 100
= \frac{162}{659} \times 100
= 24.6
\]
Bạn đặt keyframe nhiều nhất ở người nào? Vì sao?

Tôi đặt keyframe nhiều nhất ở người P5 (69 keyframe, trung bình 46.0 keyframe / 100 frame). Nguyên nhân là vì từ frame 60 trở đi, người này di chuyển qua khu vực đông đúc, bị che khuất một phần tới 64 frame, đồng thời liên tục đổi hướng đi và thay đổi tốc độ khiến đường nội suy tuyến tính của CVAT dễ bị lệch (drift) khỏi cơ thể nếu không chèn keyframe bám sát.
3. Đoạn bị che (CP2)
Đối tượng được theo dõi: P3 (Track 3 trong MOT / Track 2 trong CVAT).
Mốc	Frame
Bắt đầu bị che một phần (bật occluded)	105
Mất hẳn (bật outside)	111
Hiện lại (tắt outside)	137
Thấy rõ trở lại (tắt occluded)	143


- Thời gian khuất hẳn: 26 frame = 0.87 giây (tính theo 30 FPS: 26 ÷ 30 ≈ 0.87 giây).
- Quyết định: Giữ cùng ID, không tạo track mới.
Lý do:
1. Thời gian khuất so với ngưỡng 60 frame: Đối tượng chỉ bị khuất hẳn trong 26 frame (khoảng 0.87 giây), ngắn hơn nhiều so với ngưỡng quy định 60 frame (2 giây) của lớp.
2. Ngoại hình: Khi xuất hiện trở lại ở frame 137, trang phục, dáng người và màu sắc quần áo hoàn toàn trùng khớp với đối tượng trước khi bị che ở frame 110.
3. Hướng và tốc độ: Vị trí xuất hiện lại nằm đúng trên quỹ đạo di chuyển, cùng hướng đi và tốc độ bước chân ước tính trước lúc bị che khuất nên chắc chắn là cùng một người.
Ảnh chụp màn hình
Bổ sung 3 ảnh tương ứng trên CVAT vào thư mục report/individual/images/.

Nguồn ảnh: MOT17, MOTChallenge (Milan et al., 2016).
4. Tự review ID (CP3)
Tôi thực hiện hai lượt kiểm tra:
- Lượt 1 – Theo người: Đi ngược từ frame 149 về frame 0 trên CVAT.
- Lượt 2 – Theo cảnh: Nhảy cách mỗi lần 10 frame.
Các loại lỗi sử dụng đúng 7 mã: id_switch, fragmentation, lost, merge, false_track, drift, flag.
Frame	Mã người	Loại lỗi	Mô tả	Phát hiện ở lượt	Đã sửa?
82	P5	drift	Box nội suy bị trôi lệch về phía sau gót chân khi đối tượng bước nhanh hơn.	Lượt 1 (theo người)	Đã sửa
111	P3	flag	Quên bật cờ outside ở frame đầu tiên đối tượng bị che khuất hoàn toàn.	Lượt 1 (theo người)	Đã sửa
70	P4	merge	Box của P4 và P5 hơi chồng lấn vào nhau khi hai người đi lướt qua gần nhau.	Lượt 2 (theo cảnh)	Đã sửa


Tổng hợp số lỗi theo loại
id_switch	fragmentation	lost	merge	false_track	drift	flag
0	0	0	1	0	1	1


Lỗi nào chỉ lượt 2 (theo cảnh) mới thấy, lượt 1 (theo người) không thấy? Vì sao?

Các lỗi tương tác giữa nhiều người như id_switch (tráo ID khi hai người đi ngang qua nhau) hoặc merge (hai box chồng lấn, ôm nhầm sang người bên cạnh) chỉ dễ phát hiện ở lượt 2 (xem toàn cảnh). Vì ở lượt 1 ta lọc hiển thị từng người đơn lẻ nên không thấy được vị trí tương quan giữa box của người này với các người đi xung quanh trong cùng một khung hình.
5. File xuất và kết quả tự kiểm (CP4)
5.1. Thông tin file xuất
Kiểm tra	Kết quả
Tên file MOT 1.1	src/exports/anh.zip
Tên file CVAT for video 1.1	src/exports/video.zip
Số track ID khác nhau trong gt/gt.txt (yêu cầu: 5)	5
Frame outside không có dòng trong gt/gt.txt	Đúng
Job đã completed trên CVAT máy cá nhân	Đã completed


5.2. Kết quả từ src/check_submission.py
Số frame in theo CVAT (bắt đầu từ 0). Trong gt.txt, frame_id = frame CVAT + 1.

<details>
<summary><strong>Xem chi tiết kết quả kiểm tra</strong></summary>=== File MOT 1.1: anh.zip ===
  Số track ID: 5   |   Tổng số box: 659
  [OK]        Đúng 5 track ID.

  Track | Frame có mặt | Số frame | Đoạn vắng (outside)
      1 |   0–149      |      150 | -
      2 |   0–149      |      147 | 42–44
      3 |   0–147      |      122 | 111–136
      4 |   0–149      |      150 | -
      5 |  60–149      |       90 | -


=== File CVAT for video 1.1: video.zip ===

  Track | Nhãn   | Frame thấy | Keyframe | KF/100 frame | Frame occluded | Lần bật outside
      0 | person |        150 |       19 |         12.7 |              0 |               0
      1 | person |        147 |       25 |         17.0 |             52 |               1
      2 | person |        122 |       14 |         11.5 |             16 |               2
      3 | person |         90 |       35 |         38.9 |             40 |               0
      4 | person |        150 |       69 |         46.0 |             64 |               0

  Tổng: 162 keyframe / 659 frame có mặt = 24.6 keyframe / 100 frame
  [OK]        Đọc được 5 track từ annotations.xml.

=== Tóm tắt ===
  Lỗi: 0   |   Cảnh báo: 0
  Đạt. Dán phần tóm tắt này vào báo cáo mục 5.
</details>6. Ba câu kết
1. Nếu được gán lại, bạn sẽ đặt keyframe khác ở đâu? Vì sao?

Nếu được gán lại, tôi sẽ giảm bớt các keyframe đặt định kỳ mỗi 10 frame ở những đoạn người đi bộ di chuyển thẳng và đều (ví dụ đoạn 0–60 của P1 và P5), thay vào đó chỉ tập trung đặt keyframe tại đúng các điểm đổi hướng, đổi tốc độ và ngay trước/sau khi bị che. Điều này giúp đường nội suy mượt mà hơn, tránh hiện tượng box bị giật cục giữa các keyframe gần nhau và tiết kiệm thời gian gán nhãn.

2. Có chỗ nào bạn không chắc "cùng ID hay ID mới"? Bạn đã quyết định và ghi chú thế nào?

Ở đoạn đối tượng P3 biến mất hoàn toàn từ frame 111 đến 136 (26 frame), ban đầu tôi phân vân vì phía sau vật cản có nhiều người đi qua lại. Tuy nhiên, sau khi đếm số frame vắng (26 frame < 60 frame theo quy tắc 2 giây) và đối chiếu kỹ màu áo, dáng bước chân cũng như vector hướng di chuyển từ frame 110 sang frame 137, tôi quyết định giữ nguyên cùng một Track ID và bật/tắt cờ outside đúng ranh giới che khuất.

3. Một lỗi ID trong job của bạn (nếu không còn sót, chọn lỗi đã sửa) có thể làm xe tự lái dự đoán sai chuyển động của người đó như thế nào? Lỗi đó ảnh hưởng MOTA hay IDF1 nhiều hơn?

Nếu lỗi merge hoặc id_switch xảy ra khi hai người đi lướt qua nhau (như trường hợp P4 và P5 ở frame 70) không được sửa, hệ thống lập kế hoạch của xe tự lái sẽ tính toán sai vector vận tốc và hướng di chuyển (tưởng rằng người đang đi dọc vỉa hè đột ngột ngoặt ngang ra lòng đường), dẫn đến phanh gấp nguy hiểm hoặc đánh lái sai. Lỗi tráo đổi ID này ảnh hưởng đến IDF1 nhiều hơn, vì MOTA chỉ phạt 1 lần tại frame xảy ra switch, trong khi IDF1 tính sai toàn bộ chuỗi định danh của đối tượng ở tất cả các frame sau đó.
7. Tài liệu tham khảo và công cụ AI đã dùng
Tài liệu tham khảo
- Tài liệu hướng dẫn thực hành Lab Ngày 5:
  - docs/GUIDELINE.md
  - docs/CVAT_CHEATSHEET.md
  - docs/MOT_FORMAT.md
  - CHECKPOINTS.md
- Bộ dữ liệu MOT17 (MOTChallenge – Milan et al., 2016), giấy phép CC BY-NC-SA 3.0.
Công cụ AI đã dùng
- Gemini: Hỗ trợ giải thích quy trình thiết lập môi trường CVAT local, giải đáp quy ước nhãn occluded / outside và hỗ trợ tổng hợp số liệu từ kết quả script kiểm tra để hoàn thiện báo cáo.
