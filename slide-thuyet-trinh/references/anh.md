# Ảnh trong slide

## Nhận ảnh

1. Mở một thư mục trong dự án cho người dùng thả ảnh vào (ví dụ `slide-anh/`), và mở
   thư mục đó bằng File Explorer nếu họ nhờ.
2. Khi họ báo đã thêm, liệt kê file theo thời gian tạo để biết ảnh nào mới.
3. Tạo bản xem nhỏ (cạnh dài 900–1000px) vào thư mục nháp rồi xem **từng ảnh** trước
   khi quyết định đặt ở đâu. Không đoán nội dung ảnh qua tên file.

## Ảnh nào dùng, ảnh nào để lại

Dùng:

- Ảnh người dùng tự chụp, tự tạo, hoặc do AI của họ tạo ra.
- Ảnh chụp màn hình sản phẩm, app, trang bán hàng của chính họ.
- Poster, logo của họ (logo cần bản nền sáng).

Để lại và nói rõ lý do:

- Ảnh của người khác lấy từ Pinterest, Instagram, mạng xã hội. Có thể dùng ảnh chụp
  màn hình cả lưới Pinterest để minh hoạ "tìm ảnh mẫu", không phóng to một tấm ảnh đơn
  của người khác.
- Poster hay tài liệu có tên thương hiệu, số điện thoại của người khác.
- Ảnh hở hang hoặc gợi cảm, nhất là khi slide có câu dặn không dùng loại ảnh đó.
- Ảnh có mặt, tên, tin nhắn riêng của người khác (buổi Zoom, danh sách chat). Nếu
  cần dùng thì cắt chỉ lấy phần của người dùng và báo họ phần nào còn lộ.

Không tự lấy ảnh từ Pinterest hay trang khác đưa vào slide.

## Cắt và thu gọn (Windows, không cần cài gì)

```powershell
Add-Type -AssemblyName System.Drawing
$i = [System.Drawing.Image]::FromFile("D:\du-an\slide-anh\anh.png")
# vùng cắt tính theo tỷ lệ 0..1 của ảnh gốc
$sx=[int]($i.Width*0.0); $sy=[int]($i.Height*0.0); $sw=[int]($i.Width*1.0); $sh=[int]($i.Height*1.0)
$s=[Math]::Min(1.0, 1500/[Math]::Max($sw,$sh)); $w=[int]($sw*$s); $h=[int]($sh*$s)
$b = New-Object System.Drawing.Bitmap $w,$h
$g = [System.Drawing.Graphics]::FromImage($b); $g.InterpolationMode='HighQualityBicubic'
$g.DrawImage($i,(New-Object System.Drawing.Rectangle 0,0,$w,$h),(New-Object System.Drawing.Rectangle $sx,$sy,$sw,$sh),[System.Drawing.GraphicsUnit]::Pixel)
$b.Save("D:\du-an\.artifact-tmp\img\ten-khong-dau.jpg",[System.Drawing.Imaging.ImageFormat]::Jpeg)
$g.Dispose(); $b.Dispose(); $i.Dispose()
```

- Cạnh dài 1500px là đủ nét cho khung 1920×1080 và giữ mỗi ảnh dưới 500 KB.
- Đặt tên file không dấu, không khoảng trắng.
- Ảnh chụp màn hình có nhiều khoảng đen hoặc thanh trình duyệt thì cắt bỏ, chỉ giữ
  phần có nội dung.

## Tải lên và đặt vào slide

Tải lên bằng công cụ Artifact với `asset: true` và `file_paths` (tối đa 25 ảnh một
lần, ảnh phải nằm trong thư mục dự án). Kết quả trả về `/_blob/<id>` cho từng ảnh;
đặt nguyên chuỗi đó vào `src`:

```html
<img src="/_blob/ID" alt="Mô tả ngắn bằng tiếng Việt" style="width:360px;height:440px;object-fit:cover;border-radius:24px">
```

- `<img>` phải có `width` và `height` bằng px.
- Ảnh người, poster: `object-fit:cover`. Logo: `object-fit:contain`.
- Khung ảnh nên cùng tỷ lệ với ảnh gốc, vì `cover` cắt giữa ảnh và không chỉnh được
  điểm neo. Ảnh dọc đặt vào khung ngang sẽ mất mặt người.
- Muốn nhấn một ảnh: bọc trong khối nền vàng rộng hơn ảnh 24px.
- Mỗi ảnh chỉ dùng ở một slide; riêng slide kết được dùng lại ảnh để tổng hợp.
- Ảnh nhỏ hơn 400px mỗi chiều phóng lên sẽ mềm: báo người dùng và xin bản gốc.
