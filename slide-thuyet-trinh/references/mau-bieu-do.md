# Mười mẫu hình vẽ theo nội dung

Trước khi vẽ, hỏi nội dung có hình dạng gì, rồi chọn mẫu tương ứng. Mã dưới đây đặt
vào khối hình của slide bài học (xem `khuon-slide.md`). Chữ trong mã là chữ giữ chỗ:
thay bằng chữ của người dùng.

| Nội dung có dạng | Mẫu hình |
|---|---|
| Lọc dần, ít dần | 1. Phễu |
| Tăng dần, leo thang | 2. Cột cao dần |
| Chia phần trăm | 3. Thanh tỷ lệ |
| Hai thứ gộp lại ra một thứ | 4. Phép cộng |
| Các bước nối tiếp | 5. Chuỗi thẻ ngang |
| Các bước nối tiếp, có ảnh minh hoạ | 6. Bước xếp dọc + ảnh |
| Một cái điều khiển nhiều cái | 7. Sơ đồ nhánh |
| Nhiều thứ đỡ một thứ | 8. Trụ và nền |
| Hai lựa chọn đối nhau | 9. Hai thẻ so sánh |
| Một thứ bao gồm nhiều thứ | 10. Khung bao ngoài |

## 1. Phễu

Ba thanh hẹp dần, thanh cuối vàng. Cột phải là ba ý ngắn kẻ ngang.

```html
<div style="flex:1;display:flex;flex-direction:row;gap:70px;align-items:center">
<div style="width:940px;display:flex;flex-direction:column;align-items:center;gap:14px">
<div style="width:940px;display:flex;justify-content:space-between;align-items:center;border:3px solid #111111;border-radius:22px;padding:40px 48px"><h3 style="font-size:46px;font-weight:700">Tầng 1</h3><p style="font-size:40px;font-weight:600;color:#555555">con số</p></div>
<x-shape kind="arrow-down" style="width:24px;height:38px;background:#111111"></x-shape>
<div style="width:720px;display:flex;justify-content:space-between;align-items:center;border:3px solid #111111;border-radius:22px;padding:40px 48px"><h3 style="font-size:46px;font-weight:700">Tầng 2</h3><p style="font-size:40px;font-weight:600;color:#555555">con số</p></div>
<x-shape kind="arrow-down" style="width:24px;height:38px;background:#111111"></x-shape>
<div style="width:520px;display:flex;justify-content:space-between;align-items:center;background:#FFEA00;border:3px solid #111111;border-radius:22px;padding:40px 48px"><h3 style="font-size:46px;font-weight:700">Tầng 3</h3><p style="font-size:40px;font-weight:700">con số</p></div>
</div>
<div style="flex:1;display:flex;flex-direction:column;gap:0">
<p style="font-size:32px;font-weight:600;line-height:1.35;padding:28px 0;border-top:3px solid #111111">Ý ngắn thứ nhất.</p>
<p style="font-size:32px;font-weight:600;line-height:1.35;padding:28px 0;border-top:3px solid #111111">Ý ngắn thứ hai.</p>
</div>
</div>
```

## 2. Cột cao dần

Mỗi cột cao hơn cột trước 80–180px. Cột quan trọng nhất màu vàng: có thể là cột cao
nhất (đích đến) hoặc cột thấp nhất (nền tảng), tuỳ nội dung nói gì.

```html
<div style="flex:1;display:flex;flex-direction:row;align-items:flex-end;gap:20px;padding:0 0 20px">
<div style="flex:1;height:290px;display:flex;flex-direction:column;gap:14px;border:3px solid #111111;border-radius:22px 22px 0 0;padding:30px 30px"><p style="font-size:28px;font-weight:700;background:#FFEA00;border-radius:50%;width:60px;height:60px;line-height:60px;text-align:center">1</p><h3 style="font-size:40px;font-weight:700;line-height:1.2">Bậc 1</h3><p style="font-size:27px;font-weight:500;line-height:1.4;color:#555555">Chú thích</p></div>
<div style="flex:1;height:420px;display:flex;flex-direction:column;gap:14px;border:3px solid #111111;border-radius:22px 22px 0 0;padding:30px 30px"><p style="font-size:28px;font-weight:700;background:#FFEA00;border-radius:50%;width:60px;height:60px;line-height:60px;text-align:center">2</p><h3 style="font-size:40px;font-weight:700;line-height:1.2">Bậc 2</h3><p style="font-size:27px;font-weight:500;line-height:1.4;color:#555555">Chú thích</p></div>
<div style="flex:1;height:550px;display:flex;flex-direction:column;gap:14px;background:#FFEA00;border:3px solid #111111;border-radius:22px 22px 0 0;padding:30px 30px"><p style="font-size:28px;font-weight:700;background:#FFFFFF;border:3px solid #111111;border-radius:50%;width:60px;height:60px;line-height:54px;text-align:center">3</p><h3 style="font-size:40px;font-weight:700;line-height:1.2">Bậc 3</h3><p style="font-size:27px;font-weight:500;line-height:1.4">Chú thích</p></div>
</div>
```

Biến thể cột giá: cột chỉ chứa một con số lớn (64px) căn giữa.

## 3. Thanh tỷ lệ

`flex` của mỗi ô bằng đúng con số phần trăm; hàng nhãn bên dưới dùng cùng tỷ lệ.

```html
<div style="display:flex;flex-direction:column;gap:10px">
<div style="display:flex;flex-direction:row;gap:6px">
<div style="flex:55;height:110px;display:flex;align-items:center;justify-content:center;background:#FFEA00;border:3px solid #111111;border-radius:18px"><h3 style="font-size:54px;font-weight:700">55%</h3></div>
<div style="flex:38;height:110px;display:flex;align-items:center;justify-content:center;background:#E9E9E4;border:3px solid #111111;border-radius:18px"><h3 style="font-size:54px;font-weight:700">38%</h3></div>
<div style="flex:7;height:110px;display:flex;align-items:center;justify-content:center;border:3px solid #111111;border-radius:18px"><h3 style="font-size:28px;font-weight:700">7%</h3></div>
</div>
<div style="display:flex;flex-direction:row;gap:6px">
<p style="flex:55;font-size:26px;font-weight:600;text-align:center">Phần A</p>
<p style="flex:38;font-size:26px;font-weight:600;text-align:center">Phần B</p>
<p style="flex:7;font-size:26px;font-weight:600;text-align:center;white-space:nowrap">Phần C</p>
</div>
</div>
```

## 4. Phép cộng

`[A] + [B] → [C]`, kết quả màu vàng. Dấu `+`, `×`, `=` là chữ cỡ 64–96px.

```html
<div style="display:flex;flex-direction:row;align-items:center;gap:22px">
<div style="flex:1;height:190px;display:flex;align-items:center;justify-content:center;border:3px solid #111111;border-radius:22px"><h3 style="font-size:40px;font-weight:700">Thứ A</h3></div>
<p style="font-size:72px;font-weight:700;line-height:1">+</p>
<div style="flex:1;height:190px;display:flex;align-items:center;justify-content:center;border:3px solid #111111;border-radius:22px"><h3 style="font-size:40px;font-weight:700">Thứ B</h3></div>
<x-shape kind="arrow-right" style="width:44px;height:22px;background:#111111"></x-shape>
<div style="flex:1;height:190px;display:flex;align-items:center;justify-content:center;background:#FFEA00;border:3px solid #111111;border-radius:22px"><h3 style="font-size:40px;font-weight:700">Kết quả</h3></div>
</div>
```

Khi A, B, C là ảnh: ba cột rộng 360px, mỗi cột là ảnh 360×440 rồi tên và chú thích bên
dưới; hàng dùng `align-items:flex-start` để mép trên thẳng nhau; ảnh kết quả bọc trong
khối nền vàng.

## 5. Chuỗi thẻ ngang

Ba hoặc bốn thẻ bước nối bằng mũi tên, thẻ cuối vàng. Chỉ dùng khi nội dung thật sự là
quy trình và không có ảnh. Quá bốn bước thì tách slide. Mã thẻ và mũi tên nằm ở
`khuon-slide.md`, bọc trong:

```html
<div style="flex:1;display:flex;flex-direction:column;justify-content:center">
<div style="display:flex;flex-direction:row;gap:12px">
  <!-- thẻ 1, mũi tên, thẻ 2, mũi tên, thẻ 3 -->
</div>
</div>
```

## 6. Bước xếp dọc + ảnh

```html
<div style="flex:1;display:flex;flex-direction:row;align-items:center;gap:70px">
<div style="width:880px;display:flex;flex-direction:column;align-items:center;gap:12px">
<div style="width:880px;display:flex;flex-direction:row;align-items:center;gap:26px;border:3px solid #111111;border-radius:22px;padding:26px 32px"><p style="font-size:28px;font-weight:700;background:#FFEA00;border-radius:50%;width:60px;height:60px;line-height:60px;text-align:center">1</p><div style="display:flex;flex-direction:column;gap:4px"><h3 style="font-size:36px;font-weight:700;line-height:1.2">Tên bước</h3><p style="font-size:26px;font-weight:500;color:#555555">Chú thích</p></div></div>
<x-shape kind="arrow-down" style="width:24px;height:32px;background:#111111"></x-shape>
<!-- bước 2, mũi tên, bước 3 (nền vàng, ô số nền trắng viền đen) -->
</div>
<img src="/_blob/ID" alt="Mô tả ảnh" style="width:690px;height:528px;object-fit:cover;border-radius:22px">
</div>
```

## 7. Sơ đồ nhánh

Hàng mũi tên và hàng khối dùng cùng cấu trúc `flex:1` để mũi tên rơi đúng giữa mỗi khối.

```html
<div style="width:800px;display:flex;flex-direction:column;align-items:center;gap:12px">
<div style="width:800px;height:150px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;background:#FFEA00;border:3px solid #111111;border-radius:24px"><h3 style="font-size:40px;font-weight:700">Khối ra lệnh</h3><p style="font-size:27px;font-weight:600">Vai trò</p></div>
<div style="width:800px;display:flex;flex-direction:row;gap:24px">
<div style="flex:1;display:flex;justify-content:center"><x-shape kind="arrow-down" style="width:24px;height:38px;background:#111111"></x-shape></div>
<div style="flex:1;display:flex;justify-content:center"><x-shape kind="arrow-down" style="width:24px;height:38px;background:#111111"></x-shape></div>
</div>
<div style="width:800px;display:flex;flex-direction:row;gap:24px">
<div style="flex:1;height:250px;display:flex;flex-direction:column;justify-content:center;gap:10px;border:3px solid #111111;border-radius:24px;padding:0 28px"><h3 style="font-size:32px;font-weight:700;line-height:1.2">Nhánh 1</h3><p style="font-size:25px;font-weight:500;line-height:1.35;color:#555555">Làm gì</p></div>
<div style="flex:1;height:250px;display:flex;flex-direction:column;justify-content:center;gap:10px;border:3px solid #111111;border-radius:24px;padding:0 28px"><h3 style="font-size:32px;font-weight:700;line-height:1.2">Nhánh 2</h3><p style="font-size:25px;font-weight:500;line-height:1.35;color:#555555">Làm gì</p></div>
</div>
</div>
```

## 8. Trụ và nền

```html
<div style="flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:10px">
<div style="width:1500px;height:96px;display:flex;align-items:center;justify-content:center;border:3px solid #111111;border-radius:18px"><h3 style="font-size:36px;font-weight:700">Tên chung</h3></div>
<div style="width:1400px;display:flex;flex-direction:row;gap:120px">
<div style="flex:1;height:290px;display:flex;align-items:center;justify-content:center;border:3px solid #111111"><h3 style="font-size:42px;font-weight:700">Trụ 1</h3></div>
<div style="flex:1;height:290px;display:flex;align-items:center;justify-content:center;border:3px solid #111111"><h3 style="font-size:42px;font-weight:700">Trụ 2</h3></div>
<div style="flex:1;height:290px;display:flex;align-items:center;justify-content:center;background:#FFEA00;border:3px solid #111111"><h3 style="font-size:42px;font-weight:700">Trụ 3</h3></div>
</div>
<div style="width:1640px;height:110px;display:flex;flex-direction:row;align-items:center;justify-content:center;gap:20px;background:#EDEDE8;border-radius:18px"><p style="font-size:28px;font-weight:600;color:#555555">Gốc rễ</p><h3 style="font-size:36px;font-weight:700">Câu làm nền</h3></div>
</div>
```

## 9. Hai thẻ so sánh

```html
<div style="display:flex;flex-direction:row;gap:24px">
<div style="flex:1;height:420px;display:flex;flex-direction:column;justify-content:center;gap:16px;border:3px solid #111111;border-radius:24px;padding:0 44px"><h3 style="font-size:52px;font-weight:700;line-height:1.15;white-space:nowrap">Lựa chọn A</h3><p style="font-size:30px;font-weight:500;line-height:1.4;color:#555555">Mô tả</p><p style="font-size:30px;font-weight:700;line-height:1.4">Kết luận</p></div>
<div style="flex:1;height:420px;display:flex;flex-direction:column;justify-content:center;gap:16px;background:#FFEA00;border:3px solid #111111;border-radius:24px;padding:0 44px"><h3 style="font-size:52px;font-weight:700;line-height:1.15;white-space:nowrap">Lựa chọn B</h3><p style="font-size:30px;font-weight:500;line-height:1.4">Mô tả</p><p style="font-size:30px;font-weight:700;line-height:1.4">Kết luận</p></div>
</div>
```

## 10. Khung bao ngoài

```html
<div style="width:700px;display:flex;flex-direction:column;gap:16px;border:3px dashed #111111;border-radius:28px;padding:32px 32px">
<h3 style="font-size:34px;font-weight:700;line-height:1.2">Tên gói</h3>
<div style="display:flex;flex-direction:column;gap:6px;background:#FFEA00;border:3px solid #111111;border-radius:18px;padding:22px 28px"><h3 style="font-size:30px;font-weight:700;line-height:1.25">Phần chính</h3><p style="font-size:24px;font-weight:500;line-height:1.4">Chú thích</p></div>
<div style="display:flex;align-items:center;border:3px solid #111111;border-radius:18px;padding:24px 28px"><h3 style="font-size:30px;font-weight:700;line-height:1.25">Phần thứ hai</h3></div>
<div style="display:flex;align-items:center;border:3px solid #111111;border-radius:18px;padding:24px 28px"><h3 style="font-size:30px;font-weight:700;line-height:1.25">Phần thứ ba</h3></div>
</div>
```

## Mẫu phụ

- **Dải ngày hoặc dải lặp:** hàng ô `flex:1` cao 150px đánh số 1–7, ô cuối vàng; hoặc
  hàng ô nền `#EDEDE8` lặp cùng một nhãn ("5 phút").
- **Bảng giá:** ba thẻ xếp dọc, nhãn nhỏ ở trên, con số 40px ở dưới, thẻ nên chọn vàng.
- **Lưới 2×2:** hai hàng, mỗi hàng hai ô `flex:1` cao 200px, cho bốn phần ngang hàng.
- **Dải clip trên thanh nhạc:** hàng ô viền đen rộng hẹp khác nhau (`flex:3`, `2`, `4`…)
  nằm trên một thanh vàng dài cao 70px.
- **Lộ trình:** các cột nền `#EDEDE8` cao dần, tên chuyên đề nằm trên đầu cột, cột
  không bắt buộc viền nét đứt, cột cuối vàng.
- **Hàng kết của trang cuối:** năm cột rộng 288px, mỗi cột một ảnh 288×216 và nhãn có
  ô số bên dưới, nối bằng mũi tên, hàng dùng `justify-content:space-between`.

## Lỗi hay gặp

- Chữ rớt dòng trong ô hẹp: thêm `white-space:nowrap` và giảm cỡ chữ, hoặc tăng `flex`
  của ô đó.
- Nhãn bo tròn bị gãy thành hai dòng: mỗi nhãn cần `white-space:nowrap`.
- Con số bị ngắt giữa chừng ("1-" xuống dòng "2 đô"): nối bằng `&nbsp;`.
- Hai màu vàng trên một slide: giữ một, cái còn lại đổi sang viền đen hoặc nền xám.
- Chú thích dài làm một khung cao hơn các khung bên cạnh: dùng `align-items:flex-start`
  cho hàng, bọc ngoài bằng một khối `justify-content:center`.
- Chân cột dính vào khung ghi nhớ: thêm `padding:0 0 20px` cho khối hình.
