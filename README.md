# Skill làm slide thuyết trình

Skill cho Claude Code để làm slide thuyết trình theo phong cách Phong Menly: nền trắng,
chữ đen, vàng chanh làm điểm nhấn, mỗi slide một hình vẽ theo đúng nội dung, chữ lấy
nguyên văn từ nội dung của bạn.

## Chạy được ở đâu

Ba đường dựng, dùng chung một khuôn, chỉ khác bước xuất ra:

| Đường | Cần gì | Ra cái gì |
|---|---|---|
| **A · Artifact** | Claude Code hoặc Claude.ai | Bộ slide bấm xem được, có nút xuất Canva/PPTX |
| **B · PPTX** | Chạy được lệnh + `pip install python-pptx` | File `.pptx` sửa được từng khối, nhập thẳng Canva |
| **C · deck.html** | Chỉ cần trình duyệt | Một tệp HTML, bấm đúp là mở, in ra PDF |

Dùng Claude thì đi đường A. Dùng **Codex, app ChatGPT bản chạy lệnh** thì đi đường
B — ra file PowerPoint thật, sửa được từng chữ. Dùng **ChatGPT web hay Gemini**
(chỉ trả lời chữ) thì đi đường C: AI in ra một tệp, bạn lưu thành `deck.html` rồi
bấm đúp để mở.

## Cài đặt

Chép thư mục `slide-thuyet-trinh` vào thư mục skill của bạn:

**Windows (PowerShell)**

```powershell
git clone https://github.com/PhongMenly/slide.git
Copy-Item -Recurse slide\slide-thuyet-trinh "$env:USERPROFILE\.claude\skills\"
```

**macOS / Linux**

```bash
git clone https://github.com/PhongMenly/slide.git
cp -r slide/slide-thuyet-trinh ~/.claude/skills/
```

Mở lại Claude Code. Gõ `/slide-thuyet-trinh` để gọi skill, hoặc cứ nhắn "làm slide
thuyết trình cho tôi", Claude sẽ tự dùng.

Muốn skill chỉ có trong một dự án thì chép vào `<dự án>/.claude/skills/` thay cho thư
mục ở trên.

## Cách dùng

### 1. Đưa nội dung

Nói cho Claude biết nội dung nằm ở đâu. Ví dụ:

> Làm slide ôn tập khoá học, nội dung nằm trong file `src/data/zoomLessons.ts`, mỗi bài
> một slide.

hoặc dán thẳng nội dung vào khung chat. Skill chỉ dùng chữ của bạn, không tự viết thêm,
nên nội dung càng đủ thì slide càng đủ.

### 2. Duyệt 3 đến 5 slide mẫu

Claude làm vài slide mẫu trước và gửi đường link. Bạn xem, góp ý, rồi mới cho làm hết.
Góp ý nhanh nhất là chụp màn hình slide chưa ổn và nói chỗ nào chưa ổn.

### 3. Thêm ảnh

Nhắn "mở thư mục để tôi thêm ảnh". Claude tạo thư mục `slide-anh` trong dự án và mở
lên. Bạn thả ảnh vào rồi nhắn "tôi thêm ảnh rồi". Claude xem từng ảnh và đặt vào slide
phù hợp.

Nên dùng ảnh của chính bạn: ảnh tự chụp, ảnh AI bạn tạo, ảnh chụp màn hình sản phẩm,
poster, logo nền sáng. Ảnh của người khác (Pinterest, Instagram, poster có tên và số
điện thoại người khác) Claude sẽ để lại và báo cho bạn.

### 4. Soát lỗi

Nhắn "kiểm tra giúp tôi chính tả và bố cục". Claude mở bộ slide trên trình duyệt, đi
qua từng trang, sửa chữ rớt dòng, khối lệch, khối dính nhau, rồi báo lại những gì đã
sửa và những gì cần bạn quyết.

### 5. Đưa sang Canva hoặc PowerPoint

**Đường A** — trên trang slide bấm **Chia sẻ › Export**:

- **Send to Canva** để mở trong Canva.
- **PPTX** để tải file PowerPoint, sau đó nhập vào Canva hoặc Google Slides.

**Đường B** — đã là file `.pptx` sẵn: mở bằng PowerPoint, hoặc tải lên Canva /
Google Slides. Đây là cách duy nhất cho ra file **sửa được từng khối chữ**.

**Đường C** — mở `deck.html` rồi bấm `P` (hoặc Ctrl/Cmd + P) → khổ ngang, lề
None, bật "Background graphics" → Save as PDF. Canva nhập được file PDF này.

## Câu lệnh mẫu

| Bạn muốn | Nhắn |
|---|---|
| Bắt đầu | "Làm slide thuyết trình từ nội dung trong file X, mỗi bài một slide" |
| Sửa một slide | chụp màn hình slide đó + "chỗ này đang thừa dòng" |
| Đổi trọng tâm | "Slide 9.2 tôi muốn nói về việc thực thi hơn là nói về đội" |
| Sửa thuật ngữ | "'vai cốt đinh' đúng là Vibe Coding" |
| Thêm ảnh | "Tôi thêm ảnh rồi, bạn tìm và đặt vào" |
| Soát lần cuối | "Kiểm tra chính tả, cái gì thừa, còn thiếu ảnh gì" |

## Skill sẽ luôn giữ

- Chữ của bạn, không tự bịa. Thuật ngữ tiếng Anh viết đúng.
- Nền trắng, chữ đen, vàng chỉ ở một điểm nhấn mỗi slide. Không nền đen, không icon.
- Tiêu đề một dòng, hình ở giữa, câu từ khoá sát đáy, không thừa dòng.
- Hình vẽ theo nội dung: phễu, cột tăng dần, thanh tỷ lệ, phép cộng, chuỗi bước.

## Trong kho này có gì

```
slide-thuyet-trinh/
  SKILL.md                     hướng dẫn cho AI: nguyên tắc, quy trình, ba đường dựng
  references/
    khuon-slide.md             khuôn HTML: bìa, trang mở, slide bài học, trang kết
    mau-bieu-do.md             mười mẫu hình vẽ theo nội dung, kèm mã
    anh.md                     nhận ảnh, cắt gọn, tải lên, ảnh nào không dùng
    pptx.md                    đường B: dựng thẳng ra PowerPoint, kèm mã lam-slide.py
    deck-html.md               đường C: một tệp deck.html có bộ xem bàn phím
```

