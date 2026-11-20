# Báo cáo cá nhân — Ngày 11

Họ tên: Tạ Đức Thắng Mã học viên: 2A202603163  
Guideline: Road v1.0 Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 20/11/2026 23:19 (UTC+7); manifest ghi `2026-11-20T16:19:40+00:00` Số lần nộp lại sau Rework: 0

## 1. Kiểm project

| Mục                   | Đúng như guideline Road v1.0? | Ghi chú                                                                                                        |
| --------------------- | ----------------------------- | -------------------------------------------------------------------------------------------------------------- |
| 6 label, đúng kiểu    | Có                            | lane, road_curb: polyline · crosswalk, drivable: polygon · traffic_light, traffic_sign: rectangle              |
| Thuộc tính và giá trị | Có                            | Khớp `configs/road_v1_labels.json` (in từ `python -m road_lab.taxonomy`); đã so qua API `/labels?project_id=6` |
| 4 tag ảnh             | Có                            | camera, timeofday, weather, source: mỗi tag là label kiểu Tag có một thuộc tính select `value`                 |

Project `d11-road-taducthang` trên CVAT local có **một task** (id 20, 28 ảnh, 1 job), không tách thành 4 task. Vì vậy tôi export cả task, rồi tách thành `-front.zip` (A01–A16) và `-fisheye.zip` (B01–B12) bằng script gộp/lọc theo tên ảnh. Tên ảnh giữ nguyên.

Cách kết thúc polyline trên bản CVAT này: bấm phím **N** sau điểm cuối; vẽ từ gần xe (đáy ảnh) ra xa.  
Cách đặt tag ảnh trên bản CVAT này: công cụ **Tag** ở thanh bên trái → chọn label (camera trước tiên) → mở **Details** trong bảng Objects để chọn `value`. CVAT tự điền giá trị đầu danh sách (`weather = clear`), nên phải kiểm lại từng tag.

## 2. Số lượng đã gán

| Task                         | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| ---------------------------- | --: | ---: | --------: | --------: | -------: | ------------: | -----------: |
| front                        |  12 |   26 |        16 |         4 |       19 |            38 |           34 |
| front-extra (đã làm 4 / 4)   |   4 |   10 |         1 |         1 |        7 |            13 |           12 |
| fisheye                      |   8 |    5 |         2 |         7 |        8 |            13 |            6 |
| fisheye-extra (đã làm 4 / 4) |   4 |    0 |         0 |         4 |        3 |             0 |            1 |

## 3. Bảng ca khó

| Ảnh       | Nhãn                               | Phân vân giữa                      | Đã chọn                                                    | Lý do                                                                                             |
| --------- | ---------------------------------- | ---------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| A05       | lane L1/R1                         | vẽ / không vẽ                      | không vẽ                                                   | Phố không kẻ vạch; chỉ có mép vỉa → gán `road_curb`. Lint báo QC1-02, xin coach xác nhận miễn     |
| A09       | lane R1                            | vẽ / không vẽ                      | không vẽ                                                   | Bên phải chỉ có mép vỉa (đã gán `road_curb`), không có vạch sơn. Xin miễn QC1-02                  |
| A12       | lane L1/R1                         | vẽ vạch xa sau ngựa vằn / không vẽ | không vẽ                                                   | Ngã tư, sát xe không có vạch; vạch ở xa sau ngựa vằn không phải biên làn đang đi. Xin miễn QC1-02 |
| A06       | lane L1                            | trắng liền / vàng đôi              | vàng đôi (`yellow`, `double`)                              | Phóng to thấy hai nét vàng song song; lúc đầu tôi để nhầm giá trị mặc định trắng/liền             |
| A06       | lane R1                            | vạch mép / không phải lane         | R1 trắng liền                                              | Vạch trắng ở góc phải dưới là vạch gần xe nhất bên phải                                           |
| A01       | lane R2                            | `yellow` R2 / position khác        | R2 vàng liền                                               | Ảnh ở Israel: mép phải đường cao tốc sơn vàng, khác quy ước Mỹ (vàng bên trái)                    |
| A03       | lane L1 `kind`                     | single / double                    | single                                                     | Hai nét vàng không song song suốt chiều dài (một nét là mép đảo giao thông)                       |
| A06       | traffic_light (đi bộ) `color`      | green / unknown                    | green                                                      | Đèn hiện hình người đi bộ màu trắng = tín hiệu được đi                                            |
| A08       | traffic_sign "PASSENGER CARS ONLY" | prohibitory / supplementary        | prohibitory                                                | Biển hạn chế loại xe; nằm **trên** biển chỉ hướng chứ không phải tấm phụ dưới biển chính          |
| B03       | lane position (camera sau)         | theo ảnh / theo hướng xe           | theo hướng xe (trái ảnh = phải xe)                         | Guideline tính position theo làn đang đi; cần lead xác nhận quy ước cho camera sau                |
| B04       | lane                               | vạch đứt / mép vỉa                 | không gán lane                                             | Phóng to: dải trắng bên trái là mép vỉa hè, không phải vạch sơn                                   |
| B11       | lane                               | gán vạch ô đỗ / không gán          | không gán                                                  | Bãi đỗ xe; guideline: vạch ô đỗ không gán lane                                                    |
| A13, B05… | weather                            | clear / overcast / rain            | rain (A07, A10, A13), overcast (trời nhiều mây, đường khô) | Theo định nghĩa tag weather ở guideline mục 3                                                     |

## 4. Phiếu QC 1 nhận được

Bạn kiểm lô của tôi: [điền tên bạn] Quyết định nhận được: [Release / Hold / Rework]  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| [điền theo phiếu nhận được] | | | |

Tự kiểm trước khi đổi lô (lint + script self-QC), các lỗi tôi tự phát hiện và đã sửa:

| Mã     | Số lỗi | Ví dụ                                                                            | Đã sửa?                                |
| ------ | -----: | -------------------------------------------------------------------------------- | -------------------------------------- |
| QC1-05 |  2 ảnh | A13 có 3 polyline cùng `L1`, A06 có 2 (vạch mới vẽ giữ nguyên `L1` mặc định)     | Có: đổi thành R1/R2, xóa vạch ngoài R2 |
| QC1-04 |      2 | Vẽ từ xa về gần (A06, A13)                                                       | Có: đảo chiều                          |
| QC1-03 |      1 | A15: vẽ vạch của đường ngược chiều bên kia dải phân cách thành L1                | Có: xóa                                |
| QC1-07 |      3 | `road_curb` quá ngắn, 12–32 px (A12); vùng `direct` trùm làn bên cạnh (A06, A13) | Có                                     |

## 5. Kiểm file export

| File                   | Mở lại được?                                   | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| ---------------------- | ---------------------------------------------- | --------------------------- | --------------------------- | ------------------------ |
| taducthang-front.zip   | Có (`road_check lint`: 16 ảnh, đủ 4 tag 16/16) | A01: 9 / 9                  | A02: 5 / 5                  | Có (`front`)             |
| taducthang-fisheye.zip | Có (`road_check lint`: 12 ảnh, đủ 4 tag 12/12) | B01: 4 / 4                  | B02: 11 / 11                | Có (`fisheye_front`)     |

Manifest `taducthang-manifest.json`, revision 1:

- `contains_images = false` cho cả hai file;
- sha256 front `7977ea95d84e…`, fisheye `69f3c4138f0c…`;
- lint: 5 cảnh báo nặng, 0 chính, 0 nhẹ. Cả 5 đều là QC1-02 ở A05, A09, A12 (xem mục 3).

## 6. Ảnh chụp màn hình
> Ảnh 2–3 có chứa pixel ảnh BDD100K/WoodScape nên **không đưa lên repo public** (WoodScape không cho phân phối lại; SUBMISSION.md: "không gửi ảnh"). Ảnh nằm trong `submission/bao_cao/` trên máy, gửi coach riêng nếu cần.


1. Tab Labels của project: đã kiểm qua API `/labels?project_id=6`, khớp `configs/road_v1_labels.json` (xem mục 1). _(ảnh chụp tab Labels gửi coach riêng)_
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển). ![front](bao_cao/hinh2_front_A08.png) _(A08, chụp trên CVAT)_
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong. ![fisheye](bao_cao/hinh3_fisheye_B03_zoom.png) _(B03, chụp trên CVAT)_
4. Một đoạn XML có `<polyline label="lane">` (trích từ `taducthang-front.zip`):

```xml
<image id="0" name="A01_bc5fadac-fa6dd225.jpg" width="1280" height="720">
  <polyline label="lane" source="file" occluded="0" points="1257.10,700.40;1004.20,640.80;747.50,576.30;685.90,562.50;618.90,545.20;595.20,541.00;554.70,529.40;524.70,524.00;460.40,504.80" z_order="0">
    <attribute name="position">R2</attribute>
    <attribute name="style">solid</attribute>
    <attribute name="color">yellow</attribute>
    <attribute name="kind">single</attribute>
  </polyline>
```

## 7. Tự đánh giá

Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
**QC1-05 / QC1-03, gốc là QC1-06:** khi vẽ thêm vạch, tôi để nguyên bộ thuộc tính CVAT tự điền `L1 / solid / white / single`. Hậu quả: A06 và A13 có nhiều polyline cùng `L1`, gồm cả vạch nằm bên phải xe và một vạch vàng đôi bị ghi trắng liền. Tôi còn hai lần vẽ từ xa về gần (QC1-04).

Cách tránh ở Ngày 20:

- vẽ xong mỗi vạch thì mở **Details** sửa ngay `position/style/color/kind` trước khi vẽ vạch tiếp theo;
- luôn click từ đáy ảnh lên;
- trước khi export, chạy lint/self-QC: tìm dòng "2 polyline cùng position" và "lane còn bộ mặc định".

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

Ảnh A01, vạch R1 (tính bằng `python -m road_lab.rowanchor taducthang-front.zip --image A01 --position R1`):

| y                    |          720 |    680 |    640 |    600 |    560 |
| -------------------- | -----------: | -----: | -----: | -----: | -----: |
| x của chúng tôi (R1) | không có làn |  653.8 |  600.1 |  545.3 |  483.9 |
| x của bạn kia        |       [điền] | [điền] | [điền] | [điền] | [điền] |

1. Điểm đầu R1 nằm ở y ≈ 682 (capô che phần dưới), nên hàng 720 đã là "không có làn". Nếu dừng polyline sớm 40 px ở **đầu xa**, các hàng 560–600 vẫn còn (vạch kéo tới y ≈ 505). Nếu cắt 40 px ở **đầu gần**, hàng 680 thành "không có làn".
2. [Điền sau khi so với bạn.] Lệch ở hàng gần xe (680–720) ảnh hưởng LKA nhiều hơn, vì đó là vị trí ngang của xe so với vạch ngay lúc này.
3. Phép nội suy x theo y không đổi khi polyline vẽ ngược chiều (`x_at_y` tìm đoạn chứa hàng y bất kể chiều). Nhưng các script giả định điểm đầu là điểm gần xe sẽ sai: `road_check` so đầu mút và báo QC1-04, `rowanchor` in cảnh báo.
