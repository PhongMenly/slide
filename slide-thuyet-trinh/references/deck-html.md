# Khung deck.html — một tệp, mở bằng trình duyệt

Dùng khi không có Artifact và cũng không chạy được lệnh (ví dụ ChatGPT bản web):
AI in ra đúng một tệp, người dùng lưu thành `deck.html` rồi bấm đúp để mở.

Cách dùng: giữ nguyên phần khung dưới đây, chỉ chèn các `<section>` slide vào
giữa hai dòng đánh dấu. **Mỗi `<section>` viết đúng như khuôn ở `references/khuon-slide.md`** —
cùng cỡ chữ, cùng màu, cùng bố cục, nên slide ở đây và slide dựng bằng Artifact
nhìn như nhau.

Phím điều khiển: `→` / `Space` sang trang, `←` lùi, `F` toàn màn hình, `P` in ra
PDF (hộp thoại in của trình duyệt — chọn khổ ngang, lề None, bật "Background
graphics").

```html
<!doctype html>
<html lang="vi">
<head>
<meta charset="utf-8">
<title>Tên bộ slide</title>
<link href="https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  *{box-sizing:border-box}
  html,body{margin:0;padding:0;background:#333;font-family:'Be Vietnam Pro',Arial,sans-serif}
  /* Mỗi slide là khung cố định 1920x1080, thu phóng theo cửa sổ để không vỡ bố cục */
  /* Khung giữ nguyên 1920x1080 rồi thu nhỏ bằng scale. PHẢI đặt tuyệt đối và
     dịch -50% -50%: nếu để trong flex rồi scale thì hộp bố cục vẫn là 1920px
     nên slide lệch sang phải và bị cắt mất mép trái (đã vấp thật). */
  #san{position:relative;height:100vh;overflow:hidden}
  #khung{position:absolute;left:50%;top:50%;transform-origin:center center;width:1920px;height:1080px;background:#fff}
  /* !important là BẮT BUỘC: mỗi section mang sẵn style inline có display:flex,
     mà inline thắng stylesheet thường — không có !important thì mọi slide chồng
     lên nhau, chỉ thấy slide cuối (đã vấp thật khi chụp lại màn hình kiểm tra). */
  section{width:1920px;height:1080px;position:absolute;inset:0;display:none!important;overflow:hidden}
  section.hien{display:flex!important}
  h1,h2,h3,p,ul,ol{margin:0}
  #so{position:fixed;right:18px;bottom:14px;color:#fff;font-size:14px;opacity:.65}
  @media print{
    html,body{background:#fff}
    #san{position:static;height:auto;overflow:visible}
    #khung{position:static;transform:none!important;width:1920px;height:auto}
    section{display:flex!important;position:relative;page-break-after:always;break-after:page}
    #so{display:none}
  }
  @page{size:1920px 1080px;margin:0}
</style>
</head>
<body>
<div id="san"><div id="khung">
<!-- CHÈN CÁC SECTION SLIDE VÀO ĐÂY -->

<!-- HẾT PHẦN SLIDE -->
</div></div>
<div id="so"></div>
<script>
  const ds = [...document.querySelectorAll('section')];
  let i = 0;
  const so = document.getElementById('so');
  function ve() {
    ds.forEach((s, k) => s.classList.toggle('hien', k === i));
    so.textContent = (i + 1) + ' / ' + ds.length;
    location.hash = i + 1;
  }
  function thuPhong() {
    const k = Math.min(innerWidth / 1920, innerHeight / 1080);
    document.getElementById('khung').style.transform = 'translate(-50%,-50%) scale(' + k + ')';
  }
  addEventListener('keydown', (e) => {
    if (e.key === 'ArrowRight' || e.key === ' ' || e.key === 'PageDown') { i = Math.min(i + 1, ds.length - 1); ve(); }
    if (e.key === 'ArrowLeft' || e.key === 'PageUp') { i = Math.max(i - 1, 0); ve(); }
    if (e.key.toLowerCase() === 'f') document.documentElement.requestFullscreen?.();
    if (e.key.toLowerCase() === 'p') print();
  });
  addEventListener('click', (e) => { if (!e.target.closest('a')) { i = Math.min(i + 1, ds.length - 1); ve(); } });
  addEventListener('resize', thuPhong);
  i = Math.max(0, (parseInt(location.hash.slice(1)) || 1) - 1);
  thuPhong(); ve();
</script>
</body>
</html>
```

## Từ deck.html sang PDF, PPTX, Canva

- **PDF**: bấm `P` (hoặc Ctrl/Cmd + P) → khổ ngang, lề None, bật "Background
  graphics" → Save as PDF. Mỗi slide một trang.
- **Canva**: tải PDF lên Canva (Tạo thiết kế → Nhập tệp). Chữ trong PDF vẫn là
  chữ, Canva đọc được và sửa được phần lớn.
- **PowerPoint sửa được từng khối**: dùng đường PPTX ở `references/pptx.md` thay vì đi vòng
  qua PDF — PDF nhập vào PowerPoint chỉ ra ảnh.
