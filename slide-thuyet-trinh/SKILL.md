---
name: slide-thuyet-trinh
description: "Dùng khi người dùng muốn làm slide thuyết trình (bộ slide ôn tập khoá học, slide buổi Zoom, slide pitch, slide báo cáo) theo phong cách Phong Menly: nền trắng, chữ đen, vàng chanh chỉ làm điểm nhấn, mỗi slide một hình vẽ theo đúng nội dung, câu từ khoá neo sát đáy, chữ lấy nguyên văn từ nội dung người dùng đưa. Dựng bằng Artifact loại Slides rồi xuất sang Canva hoặc PPTX."
---

# Slide thuyết trình kiểu Phong Menly

Skill này đúc kết từ bộ slide "Hành trình 9 buổi Zoom" của KOL AI System (45 slide,
làm lại hơn chục vòng mới ra đúng ý). Làm theo đúng thứ tự dưới đây thì ra kết quả
ngay từ vòng đầu.

## 1. Sáu nguyên tắc không được phá

1. **Chữ là chữ của người dùng.** Chỉ lấy từ nội dung họ đưa (file bài học, ghi chú,
   lời nhắn). Được cắt bớt, không được tự đặt tiêu đề, không viết câu mới kiểu
   "Sau buổi này, bạn có…". Cần một câu mà nguồn không có thì hỏi, hoặc dùng đúng
   lời họ vừa nhắn và nói rõ là lấy từ đâu.
2. **Thuật ngữ tiếng Anh phải viết đúng.** Nội dung ghi theo âm thì đổi về chữ chuẩn:
   "trà phích" = Traffic, "vai cốt đinh" = Vibe Coding, "AntiGravity" = Antigravity.
   Gặp từ lạ chưa chắc thì hỏi, đừng đoán.
3. **Màu:** nền trắng `#FFFFFF`, chữ đen `#111111`, vàng chanh `#FFEA00` **chỉ cho một
   chỗ quan trọng nhất mỗi slide**. Không nền vàng tràn, không nền đen, không màu khác
   (trừ khi nội dung chính là màu, ví dụ bảng màu thương hiệu).
4. **Không icon, không hình trang trí.** Không vòng tròn, lưới chấm, zigzag, emoji.
5. **Mỗi slide một hình vẽ theo hình dạng của nội dung**, không phải một hàng hộp bằng
   nhau: phễu thì thu hẹp, giá tăng thì cột cao dần, tỷ lệ thì thanh chia đúng tỷ lệ,
   "A + B → C" thì vẽ phép cộng. Mũi tên chỉ dùng khi thật sự là quy trình.
6. **Bố cục cố định:** tiêu đề một dòng ở trên, hình chiếm trọn khoảng giữa, câu từ
   khoá neo sát đáy, nhãn chuyên đề ở góc dưới trái. Không để thừa dòng (một chữ rơi
   xuống dòng hai), không để các khối dính sát nhau.

Bỏ hẳn phần phụ: bài tập, học viên chia sẻ, lời chào. Slide cuối phải cho người xem
thấy họ đã có gì trong tay.

## 2. Quy trình

1. **Đọc hết nguồn nội dung** trước khi vẽ. Liệt kê: mỗi bài một slide, kèm một trang
   mở cho mỗi chuyên đề, một trang bìa, một trang lộ trình, một trang kết.
2. **Làm 3 đến 5 slide mẫu trước**, đưa người dùng xem, được duyệt mới làm hết. Chọn
   mẫu sao cho có đủ mấy kiểu hình khác nhau (xem `references/mau-bieu-do.md`).
3. **Viết từng slide bằng tay** theo khuôn ở `references/khuon-slide.md`. Với mỗi bài,
   hỏi: nội dung này có hình dạng gì (thu hẹp, tăng dần, tỷ lệ, cộng lại, nối tiếp,
   so sánh, bao gồm)? Rồi chọn mẫu hình tương ứng.
4. **Đăng theo đợt** (một chuyên đề một đợt), báo người dùng sau mỗi đợt để họ xem dần.
5. **Soát bằng mắt** khi người dùng yêu cầu kiểm tra: mở trang slide trên trình duyệt,
   đi qua từng slide, tìm chữ rớt dòng, khối lệch hàng, khối dính nhau.
6. **Ảnh:** chỉ dùng ảnh của người dùng. Cách xử lý và những ảnh không dùng nằm ở
   `references/anh.md`.
7. **Xuất:** trên trang slide bấm Chia sẻ › Export › Send to Canva, hoặc tải PPTX.

## 3. Cách dựng bằng Artifact loại Slides

- Tạo deck một lần bằng `type_url` của loại Slides và một `title`; các lần sau dùng
  `url` deck trả về. Không tạo deck thứ hai.
- Nội dung nằm trong `project/deck.json` (thứ tự slide, phông chữ) và
  `project/slides/<id>.html` (mỗi file đúng một `<section id="<id>">` trên khung
  1920×1080, style viết inline, chỉ dùng px và mã màu hex).
- **Đặt file trong thư mục của dự án** (ví dụ `.artifact-tmp/project/...`), rồi đăng
  với `root` = thư mục `.artifact-tmp`, `file_path` = đường dẫn đầy đủ của một file,
  `files` = các file còn lại (đường dẫn deck → đường dẫn dưới `root`). Đăng từ thư mục
  tạm của hệ thống sẽ bị chặn quyền đọc.
- **Luôn truyền `root`.** Đăng một file mà thiếu `root` thì file rơi ra gốc deck
  (`z9-2.html` thay vì `project/slides/z9-2.html`) và slide không đổi. Lỡ rồi thì đăng
  lại có `root` và xoá file lạc bằng `"z9-2.html": null` trong `files`.
- Không lặp file của `file_path` trong `files`.
- Người dùng sửa tay trên trang thì lần đăng kế bị từ chối: đọc lại file đó
  (`action: read`, `path`), ghép sửa đổi rồi đăng lại. Khi đọc lại, **đừng để
  `out_dir` trùng thư mục đang sửa**, kẻo bản tải về ghi đè lên bản vừa sửa.
- Phông chữ: Be Vietnam Pro, khai báo trong `faces` của `deck.json`. Đừng dùng DM Sans
  (thiếu dấu tiếng Việt, chữ lệch nét). Độ đậm 700 cho tiêu đề, không dùng 800–900.
- Ảnh: tải lên bằng `asset: true`, lấy đúng `url` trả về (`/_blob/<id>`) đặt vào
  `<img src>`. Không dùng `data:` hay link ngoài.

## 4. Trước khi báo xong, tự soát

- [ ] Mọi chữ trên slide đều có trong nguồn hoặc trong lời người dùng.
- [ ] Mỗi slide chỉ một chỗ màu vàng (ô số nhỏ không tính).
- [ ] Tiêu đề một dòng; tiêu đề quá dài thì cắt bớt chữ, không thêm chữ.
- [ ] Không có chữ rơi lẻ xuống dòng hai; cụm ngắn dùng `white-space:nowrap`.
- [ ] Câu từ khoá nằm sát đáy, hình nằm giữa, không có khoảng trống lơ lửng.
- [ ] Không ảnh nào dùng hai lần (trừ slide kết tổng hợp lại).
- [ ] Nói rõ với người dùng: slide nào chưa xem lại bằng mắt, ảnh nào để lại và vì sao.

## 5. Tài liệu kèm theo

- `references/khuon-slide.md` — khuôn HTML cho bìa, trang mở chuyên đề, slide bài học,
  slide kết.
- `references/mau-bieu-do.md` — mười mẫu hình vẽ theo nội dung, kèm mã.
- `references/anh.md` — nhận ảnh, cắt gọn, tải lên, và những ảnh không dùng.
