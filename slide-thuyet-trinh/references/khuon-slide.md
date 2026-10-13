# Khuôn slide

Khung vẽ 1920×1080. Mọi style viết inline, chỉ dùng px và mã màu hex. Không dùng
class, `margin`, `var()`, `em`.

## Bảng màu và cỡ chữ

| Dùng cho | Giá trị |
|---|---|
| Nền | `#FFFFFF` |
| Chữ chính, viền | `#111111`, viền `3px solid` |
| Điểm nhấn | `#FFEA00` |
| Chữ phụ | `#555555` |
| Nhãn nhỏ, nhãn góc | `#777777` |
| Nền xám nhạt (khung ghi nhớ, ô phụ) | `#F5F5F2`, `#EDEDE8` |

| Vai trò | Cỡ chữ | Độ đậm |
|---|---|---|
| Tiêu đề slide | 52px | 700 |
| Chữ to trong hình | 40–84px | 700 |
| Tên khối | 34–40px | 700 |
| Chú thích | 25–28px | 500 |
| Câu từ khoá | 30px | 700 |
| Dòng phụ dưới câu từ khoá | 24px | 500 |
| Nhãn góc | 24px | 600 |

Không dùng cỡ chữ dưới 24px.

## Slide bài học

```html
<section id="ID" data-transition="fade" style="background:#FFFFFF;color:#111111;font-family:'Be Vietnam Pro', Arial, sans-serif;padding:88px 140px 128px;display:flex;flex-direction:column;gap:34px">
<h2 style="font-size:52px;font-weight:700;line-height:1.15;white-space:nowrap">TIÊU ĐỀ MỘT DÒNG</h2>
<div style="flex:1;display:flex;flex-direction:column;justify-content:center;gap:40px">
  <!-- HÌNH VẼ: chọn một mẫu trong mau-bieu-do.md -->
</div>
<div style="display:flex;flex-direction:column;gap:6px;background:#F5F5F2;border-left:10px solid #FFEA00;border-radius:18px;padding:24px 36px">
<p style="font-size:30px;font-weight:700;line-height:1.35">Câu từ khoá.</p>
<p style="font-size:24px;font-weight:500;line-height:1.35;color:#555555">Dòng phụ (không bắt buộc).</p>
</div>
<p style="position:absolute;left:140px;bottom:52px;font-size:24px;font-weight:600;color:#777777">Zoom N · Tên chuyên đề</p>
</section>
```

Ba điều làm nên bố cục này:

- Khối hình có `flex:1` nên nó chiếm hết khoảng giữa và đẩy khung ghi nhớ xuống sát đáy.
- Khoảng giữa cao chừng 610–650px. Hình cao hơn mức đó sẽ đè lên khung ghi nhớ.
- Hình dạng cột (đáy bằng nhau) dùng `align-items:flex-end` và thêm
  `padding:0 0 20px` để chân cột không dính vào khung ghi nhớ.

## Khối dùng lại

Thẻ bước (thẻ cuối đổi nền vàng, ô số nền trắng viền đen):

```html
<div style="flex:1;min-height:430px;display:flex;flex-direction:column;justify-content:center;gap:18px;border:3px solid #111111;border-radius:24px;padding:36px 30px">
<p style="font-size:28px;font-weight:700;background:#FFEA00;border-radius:50%;width:60px;height:60px;line-height:60px;text-align:center">1</p>
<h3 style="font-size:38px;font-weight:700;line-height:1.2">Tên bước</h3>
<p style="font-size:27px;font-weight:500;line-height:1.4;color:#555555">Chú thích ngắn</p>
</div>
```

Ô số trên thẻ vàng (không dùng nền đen):

```html
<p style="font-size:28px;font-weight:700;background:#FFFFFF;border:3px solid #111111;border-radius:50%;width:60px;height:60px;line-height:54px;text-align:center">4</p>
```

Mũi tên giữa hai thẻ:

```html
<div style="display:flex;align-items:center"><x-shape kind="arrow-right" style="width:34px;height:18px;background:#111111"></x-shape></div>
```

Mũi tên xuống: `<x-shape kind="arrow-down" style="width:24px;height:38px;background:#111111"></x-shape>`

Dòng kẻ ngang cho danh sách ý:

```html
<p style="font-size:32px;font-weight:600;line-height:1.35;padding:28px 0;border-top:3px solid #111111">Một ý ngắn.</p>
```

Nhãn bo tròn:

```html
<p style="font-size:27px;font-weight:600;white-space:nowrap;background:#EDEDE8;border-radius:32px;padding:12px 26px">TikTok Shop</p>
```

## Trang bìa

```html
<section id="cover" data-transition="fade" style="background:#FFFFFF;color:#111111;font-family:'Be Vietnam Pro', Arial, sans-serif;padding:140px;display:flex;flex-direction:column;justify-content:center;gap:32px">
<p style="font-size:28px;font-weight:600;color:#777777">Tên chương trình · Mùa</p>
<h1 style="font-size:112px;font-weight:700;line-height:1.08;white-space:nowrap">Dòng một<br>Dòng hai</h1>
<div style="width:220px;height:16px;background:#FFEA00"></div>
<p style="font-size:36px;font-weight:500;line-height:1.4;color:#555555;width:900px">Một câu mô tả.</p>
<img src="/_blob/ID" alt="Logo" style="position:absolute;right:150px;top:240px;width:600px;height:600px;object-fit:contain">
</section>
```

Logo phải là bản nền sáng. Không có logo thì bỏ thẻ `<img>`, bìa chỉ cần chữ.

## Trang mở chuyên đề

```html
<section id="d4" data-transition="fade" style="background:#FFFFFF;color:#111111;font-family:'Be Vietnam Pro', Arial, sans-serif;padding:140px;display:flex;flex-direction:column;justify-content:center;gap:28px">
<p style="font-size:34px;font-weight:600;color:#777777">Zoom 4</p>
<h1 style="font-size:88px;font-weight:700;line-height:1.12;white-space:nowrap">Tên Chuyên Đề</h1>
<div style="width:220px;height:16px;background:#FFEA00"></div>
</section>
```

Tên dài thì ngắt bằng `<br>` thành hai dòng cân nhau, không để một chữ lẻ ở dòng hai.

## Trang kết

Tiêu đề lớn (88px), một dòng nói người xem đã có gì, hàng năm ô ảnh sản phẩm thật nối
bằng mũi tên (mã ở mục "Hàng kết của trang cuối" trong `mau-bieu-do.md`), câu chốt ở
đáy. Section dùng `justify-content:space-between`.

## deck.json

```json
{
  "v": 4,
  "createdOnFiles": { "v": 1, "at": "2026-10-12T10:30:00Z" },
  "lists": "css",
  "title": "Tên bộ slide",
  "order": ["cover", "roadmap", "d1", "z1-1"],
  "sections": {
    "s1": { "description": "Mở đầu", "start": "cover" },
    "s2": { "description": "Zoom 1: tên chuyên đề", "start": "d1" }
  },
  "faces": {
    "be-vietnam-pro": { "family": "Be Vietnam Pro", "href": "https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@400;600;700;800;900&display=swap" }
  },
  "designSystems": []
}
```

Đặt id slide theo bài: `z1-1`, `z1-2`, trang mở là `d1`, `d2`.
