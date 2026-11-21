# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): longtk292 Người kiểm (học viên): taducthang  
Ngày: 21/11/2026 Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `cvatday11.zip` (export CVAT job 17, 28 ảnh), không kèm manifest nên không có `revision`. Người kiểm tách thành longtk292-front.zip (A01–A16) và longtk292-fisheye.zip (B01–B12) để chạy `road_check lint`  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng) — A01, A03, A04, A07, B01, B06 Số nhãn đã kiểm (shape + tag): 50

## Tổng hợp theo mã

| Mã                                   | Loại lỗi                              |                       Số mục kiểm | Số lỗi | Mức          |
| ------------------------------------ | ------------------------------------- | --------------------------------: | -----: | ------------ |
| QC1-01 tag camera                    | sai thuộc tính / bỏ sót               |                                24 |     19 | nhẹ / nặng   |
| QC1-02 đủ L1, R1                     | bỏ sót                                |                                10 |      2 | nặng         |
| QC1-03 position                      | sai thuộc tính / thừa                 |                                11 |      3 | nặng         |
| QC1-04 tâm vạch, chiều, điểm dừng    | sai phạm vi / bỏ sót                  |                                11 |      0 | chính        |
| QC1-05 vạch đứt, che                 | sai phạm vi / sai thuộc tính          |                                11 |      1 | chính        |
| QC1-06 style, color, kind            | sai thuộc tính                        |                                11 |      2 | chính        |
| QC1-07 vùng lái                      | sai phạm vi / bỏ sót / thừa           |                                17 |      6 | chính        |
| QC1-08 đèn, màu                      | bỏ sót / sai phạm vi / sai thuộc tính | 12 (11 đèn đã gán + 1 đèn bỏ sót) |     12 | chính / nặng |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính                        |                                17 |      4 | chính        |
| QC1-10 hình in, đủ biển              | bỏ sót / sai phạm vi                  |                                 6 |      2 | chính        |
| QC1-11 fisheye                       | sai phạm vi / sai thuộc tính          |                                 5 |      0 | chính        |
| QC1-12 file                          | lỗi file                              |                                69 |      0 | nhẹ / nặng   |

## Danh sách lỗi (mỗi lỗi một dòng)

| #   | Mã     | Ảnh | Nhãn (label, id)                          | Mức   | Mô tả ngắn                                                                                                                      |
| --- | ------ | --- | ----------------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------- |
| 1   | QC1-01 | A01 | tag:camera                                | nặng  | không có tag camera (ảnh không có tag nào) → phải là camera=front                                                               |
| 2   | QC1-01 | A01 | tag:timeofday                             | nhẹ   | thiếu tag timeofday (day)                                                                                                       |
| 3   | QC1-01 | A01 | tag:weather                               | nhẹ   | thiếu tag weather (clear)                                                                                                       |
| 4   | QC1-01 | A01 | tag:source                                | nhẹ   | thiếu tag source (real)                                                                                                         |
| 5   | QC1-06 | A01 | lane#3@(706,720)                          | chính | R1 là vạch trắng ĐỨT nhưng style=solid → dashed                                                                                 |
| 6   | QC1-07 | A01 | drivable#5@(718,720)                      | chính | polygon làn bên phải (giữa R1 và vạch vàng R2) để area_type=direct → alternative                                                |
| 7   | QC1-07 | A01 | drivable#6@(0,605)                        | chính | polygon làn bên trái (giữa L2 và L1) để area_type=direct → alternative                                                          |
| 8   | QC1-09 | A01 | traffic_sign#7@(551,408)                  | chính | biển chỉ dẫn xanh lá lớn gán group=prohibitory → information                                                                    |
| 9   | QC1-09 | A01 | traffic_sign#0@(431,463)                  | chính | biển xanh lá nhỏ ở xa gán group=prohibitory → information                                                                       |
| 10  | QC1-01 | A03 | tag:camera                                | nặng  | không có tag camera (ảnh không có tag nào) → phải là camera=front                                                               |
| 11  | QC1-01 | A03 | tag:timeofday                             | nhẹ   | thiếu tag timeofday                                                                                                             |
| 12  | QC1-01 | A03 | tag:weather                               | nhẹ   | thiếu tag weather                                                                                                               |
| 13  | QC1-01 | A03 | tag:source                                | nhẹ   | thiếu tag source                                                                                                                |
| 14  | QC1-02 | A03 | (thiếu) lane L1                           | nặng  | không có L1: cặp vạch vàng bên trái làn đang đi thấy rõ (≈(220,700)→(530,380))                                                  |
| 15  | QC1-02 | A03 | (thiếu) lane R1                           | nặng  | không có R1: vạch trắng đứt giữa đường thấy rõ (≈(690,455)→(600,385))                                                           |
| 16  | QC1-07 | A03 | drivable#3@(975,681)                      | chính | làn bên phải R1 gán direct (phải là alternative) và tràn sang dải đỗ xe sát hàng xe đỗ                                          |
| 17  | QC1-08 | A03 | traffic_light#5@(627,305)                 | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 18  | QC1-08 | A03 | traffic_light#6@(707,314)                 | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 19  | QC1-08 | A03 | traffic_light#7@(593,328)                 | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 20  | QC1-08 | A03 | traffic_light#8@(603,344)                 | nặng  | đèn đang sáng XANH, facing front, gán color=red (box 7 px, không bắt buộc nhưng đã gán thì phải đúng màu)                       |
| 21  | QC1-08 | A03 | traffic_light#9@(538,339)                 | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 22  | QC1-08 | A03 | traffic_light#10@(528,332)                | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 23  | QC1-08 | A03 | traffic_light#11@(577,340)                | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 24  | QC1-08 | A03 | traffic_light#12@(495,349)                | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 25  | QC1-09 | A03 | traffic_sign#4@(216,170)                  | chính | thấy MẶT SAU tấm biển (vỏ xám, không có mặt biển) nhưng facing=front → back                                                     |
| 26  | QC1-10 | A03 | (thiếu) traffic_sign ≈(1000-1040;285-325) | chính | bỏ sót biển vàng-xanh báo trường học (warning)                                                                                  |
| 27  | QC1-10 | A03 | (thiếu) traffic_sign ≈(795-830;315-345)   | chính | bỏ sót biển cam hình thoi công trường (warning)                                                                                 |
| 28  | QC1-01 | A04 | tag:camera                                | nặng  | không có tag camera (ảnh không có tag nào) → phải là camera=front                                                               |
| 29  | QC1-01 | A04 | tag:timeofday                             | nhẹ   | thiếu tag timeofday                                                                                                             |
| 30  | QC1-01 | A04 | tag:weather                               | nhẹ   | thiếu tag weather                                                                                                               |
| 31  | QC1-01 | A04 | tag:source                                | nhẹ   | thiếu tag source                                                                                                                |
| 32  | QC1-03 | A04 | lane#0@(720,535)                          | nặng  | vạch trắng đứt sát bên phải xe là R1 nhưng position=other (lô không có R1)                                                      |
| 33  | QC1-03 | A04 | lane#8@(1280,536)                         | nặng  | vạch trắng liền bên phải (mép làn, R2) gán position=L1 (để nguyên mặc định L1/solid/white/single)                               |
| 34  | QC1-03 | A04 | lane#7@(1279,515)                         | nặng  | vạch mép làn xe đạp xanh bên phải gán position=L1 (để nguyên mặc định) — không phải L1                                          |
| 35  | QC1-05 | A04 | lane#1@(65,552)+lane#2@(24,553)           | chính | vạch vàng đôi vẽ thành 2 polyline, mỗi đường trên một nét → phải là MỘT polyline trên tâm cặp vạch                              |
| 36  | QC1-06 | A04 | lane#0@(720,535)                          | chính | vạch R1 là vạch ĐỨT nhưng style=solid → dashed                                                                                  |
| 37  | QC1-07 | A04 | drivable#6@(728,532)                      | chính | làn cùng chiều bên phải (giữa R1 và R2) gán direct → alternative                                                                |
| 38  | QC1-08 | A04 | traffic_light#9@(551,272)                 | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 39  | QC1-08 | A04 | traffic_light#10@(603,278)                | nặng  | đèn đang sáng XANH, facing front, gán color=red                                                                                 |
| 40  | QC1-01 | A07 | tag:camera                                | nặng  | không có tag camera (ảnh không có tag nào) → phải là camera=front                                                               |
| 41  | QC1-01 | A07 | tag:timeofday                             | nhẹ   | thiếu tag timeofday                                                                                                             |
| 42  | QC1-01 | A07 | tag:weather                               | nhẹ   | thiếu tag weather (rain)                                                                                                        |
| 43  | QC1-01 | A07 | tag:source                                | nhẹ   | thiếu tag source                                                                                                                |
| 44  | QC1-07 | A07 | drivable#2@(4,582)                        | chính | vùng lái direct khoét quanh xe phía trước (mép trên đi theo gầm xe ≈(440,370)→(660,410)) — guideline: không khoét quanh xe khác |
| 45  | QC1-07 | A07 | drivable#3@(795,569)                      | chính | làn cùng chiều bên phải (giữa R1 và R2) gán direct → alternative                                                                |
| 46  | QC1-08 | A07 | (thiếu) traffic_light ≈(655-667;230-244)  | chính | bỏ sót cụm đèn đang sáng xanh ở xa (cao ≈ 10 px)                                                                                |
| 47  | QC1-08 | B01 | traffic_light#1@(350,174)                 | chính | đèn quay lưng về xe (chỉ thấy vỏ, không thấy đèn sáng) mà gán color=red → unknown/off                                           |
| 48  | QC1-09 | B01 | traffic_light#1@(350,174)                 | chính | thấy mặt sau cụm đèn nhưng facing=front → back                                                                                  |
| 49  | QC1-01 | B06 | tag:timeofday                             | nhẹ   | thiếu tag timeofday                                                                                                             |
| 50  | QC1-01 | B06 | tag:weather                               | nhẹ   | thiếu tag weather                                                                                                               |
| 51  | QC1-01 | B06 | tag:source                                | nhẹ   | thiếu tag source                                                                                                                |

## Ca mơ hồ

| Ảnh     | Câu hỏi cho lead                                                                                                                                                                        | Lời đáp (nếu có) |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| A07     | Vạch trắng mờ sát dải phân cách bê tông bên trái (≈(250,430)→(420,385)) có tính là L1 không? Nếu có thì lô thiếu L1 (QC1-02 nặng) và drivable#2 tràn sang lề.                           |                  |
| B06     | Ảnh fisheye_left không có lane nào, trong khi thấy vạch trắng đứt ở làn xa (≈(180,250)→(450,70)). Có tính bỏ sót lane position=other không, và ghi mã nào (QC1-11)?                     |                  |
| (cả lô) | Bạn gửi MỘT file cvatday11.zip gộp 28 ảnh (một job CVAT), không tách <tên>-front.zip / <tên>-fisheye.zip và không kèm manifest. Mình đã tự tách để kiểm. Có tính QC1-12 không, mức nào? |                  |

## Ghi thêm ngoài mẫu (không tính vào tỉ lệ, chỉ để bạn sửa)

`road_check lint` trên cả lô còn báo các lỗi mức nặng ở ảnh ngoài 6 ảnh mẫu. Mình chưa soi bằng mắt từng chỗ, bạn tự kiểm lại:

- Thiếu tag camera: A05, A06, A08, A10, A11, B02, B07. B09 (`_FV`) gán camera = fisheye_rear, phải là fisheye_front.
- Ảnh camera hai bên dùng L1/R1 thay vì `other`: B07 lane#0, lane#1; B08 lane#6.
- Chưa có R1: A08, A09, A11, A14, A16. Chưa có L1/R1: A05, A06 (nếu ảnh thật không có vạch thì nhờ coach xác nhận miễn).
- Nhiều ảnh có 2–4 polyline cùng position L1 (A08, A09, A11, A16, B07): có thể là do để nguyên bộ mặc định L1/solid/white/single khi vẽ.
- Nhiều ảnh thiếu tag timeofday / weather / source (nhẹ).

Gợi ý khi Rework: gắn đủ 4 tag cho mọi ảnh trước, mỗi lần vẽ lane xong thì mở Details đổi position/style/color/kind, kiểm tra màu đèn bằng cách phóng to, chỉnh `area_type` cho làn bên cạnh thành alternative, rồi export lại thành hai file `<tên>-front.zip` và `<tên>-fisheye.zip` kèm manifest với `--revision 2`.

## Quyết định

Lỗi nặng: 19 Lỗi chính: 17 / 50 nhãn = 34.0% Lỗi nhẹ: 15 Ca chờ lead: 3  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): có 19 lỗi nặng → Rework.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Mẫu số là số nhãn đã kiểm (shape + tag), không phải số ảnh.
