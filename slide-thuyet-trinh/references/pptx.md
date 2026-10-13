# Đường B — dựng thẳng ra PowerPoint, không cần Artifact

Dùng khi AI **chạy được lệnh trên máy** (Codex CLI, app ChatGPT bản tải về,
Claude Code) hoặc chạy được Python trong khung chat (ChatGPT Advanced Data
Analysis). Kết quả là file `.pptx` thật: mở bằng PowerPoint, **sửa được từng
khối chữ**, nhập thẳng vào Canva hay Google Slides.

Cách này dựng lại đúng khuôn ở `references/khuon-slide.md` bằng hình khối PowerPoint: cùng khung
1920×1080, cùng màu, cùng cỡ chữ, cùng bố cục. Toạ độ ghi theo px nên hai đường
A và B ra cùng một thứ.

## Ba bước

**1. Cài thư viện (một lần):**

```bash
pip install python-pptx
```

**2. Lưu đoạn mã ở cuối mục này thành `lam-slide.py`.**

**3. Viết nội dung ra `noi-dung.json` rồi chạy:**

```bash
python lam-slide.py noi-dung.json ket-qua.pptx
```

Máy đã cài font Be Vietnam Pro thì thêm `--font "Be Vietnam Pro"` để đúng font
thương hiệu. Không có thì cứ để mặc định Arial — bố cục không đổi.

## Viết noi-dung.json

Một danh sách slide. Mỗi slide có `kieu` và dữ liệu của kiểu đó. Ba khoá dùng
chung cho mọi kiểu:

| Khoá | Nghĩa |
|---|---|
| `tieu_de` | Tiêu đề một dòng ở trên |
| `chan` | Nhãn chuyên đề ở góc dưới trái |
| `ghi_nho` | Câu từ khoá trong khung xám vạch vàng, sát đáy |

Mười một kiểu, chọn theo **hình dạng của nội dung** (xem `references/mau-bieu-do.md` để biết nội
dung nào hợp hình nào):

```jsonc
// pheu — thu hẹp dần: traffic → hoà vốn → best seller
{ "kieu": "pheu", "tieu_de": "...", "chan": "...",
  "muc": [ {"ten":"Traffic","phu":"1-2 đô"}, {"ten":"Hoà vốn","phu":"vài triệu"}, {"ten":"Best seller","phu":"x10-20"} ],
  "ds": ["Chỉ 2 nền tảng: TikTok và Fanpage.", "Chọn 1 ngành duy nhất."],
  "ghi_nho": "Case thật: 200 nghìn × 10.000 đơn." }

// cot — cột cao dần: giá tăng, số liệu tăng. "cao" từ 0 đến 1
{ "kieu": "cot", "muc": [ {"nhan":"2 đô","cao":0.25}, {"nhan":"5 đô","cao":0.6}, {"nhan":"10 đô","cao":1.0} ], "ds": ["..."] }

// ty_le — thanh chia đúng tỷ lệ. "tren" là danh sách gạch ngang phía trên (bỏ được)
{ "kieu": "ty_le", "tren": ["1 loại trang phục"], "muc": [ {"nhan":"Ngôn ngữ cơ thể","phan":55}, {"nhan":"Ngữ điệu","phan":38}, {"nhan":"Lời nói","phan":7} ] }

// cong — A + B → C
{ "kieu": "cong", "muc": [ {"ten":"Ảnh mẫu đẹp","mo_ta":"Pinterest"}, {"ten":"Ảnh nhân vật","mo_ta":"Của mình"}, {"ten":"Ảnh tương tự","mo_ta":"Giữ gương mặt"} ] }

// the_ngang — 3 đến 5 thẻ ngang hàng. "nhan_manh" là chỉ số thẻ tô vàng (từ 0)
{ "kieu": "the_ngang", "muc": [ {"ten":"...","mo_ta":"..."} ], "nhan_manh": 2 }

// buoc_doc — các bước xếp dọc, tự đánh số 01, 02...
{ "kieu": "buoc_doc", "muc": [ {"ten":"...","mo_ta":"..."} ] }

// so_sanh — hai thẻ đối nhau
{ "kieu": "so_sanh", "trai": {"nhan":"Thuê ngoài","ten":"500 nghìn/ảnh"}, "phai": {"nhan":"AI","ten":"Vài phút"}, "nhan_manh": "phai" }

// danh_sach — chỉ một danh sách gạch ngang, chữ to
{ "kieu": "danh_sach", "muc": ["...", "...", "..."] }

// anh_chu — ảnh bên trái, danh sách bên phải
{ "kieu": "anh_chu", "anh": "anh/man-hinh-app.png", "rong_anh": 760, "ds": ["...", "..."] }

// bia — trang bìa. Xuống dòng trong "ten" bằng \n
{ "kieu": "bia", "nhan": "KOL AI System · Mùa 3", "ten": "Hành trình\n9 buổi Zoom", "mo_ta": "Một câu." }

// mo_phan — trang mở một chuyên đề
{ "kieu": "mo_phan", "so": "02", "ten": "Bán hàng bằng hình ảnh" }
```

## Trước khi giao file cho người dùng

- Mở thử file `.pptx` bằng PowerPoint (hoặc tải lên Google Slides) và **nhìn qua
  từng trang**. Đừng giao file chưa mở lần nào.
- Chữ dài quá khung thì cắt bớt chữ, **đừng giảm cỡ chữ** — khuôn sống nhờ cỡ
  chữ đồng nhất.
- Mỗi slide chỉ một chỗ vàng. Kiểu `cot`, `pheu`, `cong` tự tô vàng khối cuối;
  đừng thêm `nhan_manh` ở cùng slide nữa.
- Ảnh thiếu thì script vẽ khung trống và ghi `[thiếu ảnh: ...]` ngay trên slide
  chứ không gãy cả bộ — thấy khung đó thì sửa đường dẫn rồi chạy lại.

## Mã nguồn `lam-slide.py`

```python
"""Dựng bộ slide PPTX theo khuôn tối giản — không cần Artifact, chạy ở mọi AI.

Dùng:
    pip install python-pptx
    python lam-slide.py noi-dung.json ket-qua.pptx

noi-dung.json là một danh sách slide. Mỗi slide có "kieu" và dữ liệu của kiểu đó —
xem phần "Mười kiểu slide" trong tài liệu. Toạ độ và cỡ chữ ghi theo px trên khung
1920×1080, giống hệt khuôn HTML, nên hai đường dựng ra cùng một thứ.
"""

import json
import sys

from pptx import Presentation
from pptx.dml.color import RGBColor
from pptx.enum.shapes import MSO_SHAPE
from pptx.enum.text import MSO_ANCHOR, PP_ALIGN
from pptx.util import Emu, Pt

# ---------------------------------------------------------------- khung & màu

PX = 6350  # 1 px trên khung 1920 rộng = 6350 EMU (slide 13.333 inch)
# Font mặc định phải là font CHẮC CHẮN có sẵn. Đặt "Be Vietnam Pro" mà máy mở
# file chưa cài font đó thì PowerPoint tự thay bằng một font bất kỳ — đã thử
# thật và nó rơi vào một font chữ viết tay, hỏng cả bộ slide. Muốn đúng font
# thương hiệu thì cài Be Vietnam Pro trước rồi chạy với: --font "Be Vietnam Pro"
FONT = "Arial"

DEN = RGBColor(0x11, 0x11, 0x11)
TRANG = RGBColor(0xFF, 0xFF, 0xFF)
VANG = RGBColor(0xFF, 0xEA, 0x00)
XAM_CHU = RGBColor(0x55, 0x55, 0x55)
XAM_NHAN = RGBColor(0x77, 0x77, 0x77)
XAM_NEN = RGBColor(0xF5, 0xF5, 0xF2)

LE = 140  # lề trái/phải
RONG = 1920 - LE * 2  # 1640
Y_TIEU_DE = 88
Y_NOI_DUNG = 196  # dưới tiêu đề
Y_GHI_NHO = 880  # khung ghi nhớ dưới cùng
Y_CHAN = 992  # nhãn chuyên đề
CAO_NOI_DUNG = 650  # từ Y_NOI_DUNG xuống, chừa chỗ cho ghi nhớ


def _e(px):
    return Emu(int(px * PX))


# ---------------------------------------------------------------- khối cơ bản


def chu(slide, x, y, w, h, text, size=32, dam=True, mau=DEN, canh="trai", giua_doc=True):
    """Một khối chữ. Không viền, không nền."""
    o = slide.shapes.add_textbox(_e(x), _e(y), _e(w), _e(h))
    tf = o.text_frame
    tf.word_wrap = True
    tf.margin_left = tf.margin_right = tf.margin_top = tf.margin_bottom = 0
    if giua_doc:
        tf.vertical_anchor = MSO_ANCHOR.MIDDLE
    p = tf.paragraphs[0]
    p.alignment = {"trai": PP_ALIGN.LEFT, "giua": PP_ALIGN.CENTER, "phai": PP_ALIGN.RIGHT}[canh]
    r = p.add_run()
    r.text = text
    r.font.size = Pt(size * 0.5)
    r.font.bold = dam
    r.font.color.rgb = mau
    r.font.name = FONT
    p.line_spacing = 1.15
    return o


def hop(slide, x, y, w, h, nen=None, vien=True, bo_tron=True):
    """Hộp bo góc: viền đen 3px, nền trắng hoặc vàng."""
    shape = MSO_SHAPE.ROUNDED_RECTANGLE if bo_tron else MSO_SHAPE.RECTANGLE
    o = slide.shapes.add_shape(shape, _e(x), _e(y), _e(w), _e(h))
    if bo_tron:
        o.adjustments[0] = min(0.5, 22.0 / max(1, min(w, h)))  # bo 22px như khuôn HTML
    o.fill.solid()
    o.fill.fore_color.rgb = nen if nen is not None else TRANG
    if vien:
        o.line.color.rgb = DEN
        o.line.width = Pt(1.5)  # 3px
    else:
        o.line.fill.background()
    o.shadow.inherit = False
    o.text_frame.text = ""
    return o


def hop_chu(slide, x, y, w, h, text, size=40, nen=None, phu=None, size_phu=30):
    """Hộp có chữ chính ở giữa; `phu` là chữ xám nằm bên phải."""
    hop(slide, x, y, w, h, nen=nen)
    if phu:
        chu(slide, x + 34, y, w * 0.6, h, text, size=size, canh="trai")
        chu(slide, x + w * 0.4 - 34, y, w * 0.6, h, phu, size=size_phu, mau=XAM_CHU, canh="phai")
    else:
        chu(slide, x, y, w, h, text, size=size, canh="giua")


def gach(slide, x, y, w):
    """Đường kẻ ngang 3px — dùng ngăn các dòng trong danh sách."""
    o = slide.shapes.add_shape(MSO_SHAPE.RECTANGLE, _e(x), _e(y), _e(w), _e(3))
    o.fill.solid()
    o.fill.fore_color.rgb = DEN
    o.line.fill.background()
    o.shadow.inherit = False
    return o


def danh_sach_gach(slide, x, y, w, dong, size=32, cao_dong=96):
    """Danh sách có đường kẻ phía trên mỗi dòng — khối hay dùng nhất của khuôn."""
    for i, d in enumerate(dong):
        yy = y + i * cao_dong
        gach(slide, x, yy, w)
        chu(slide, x, yy + 18, w, cao_dong - 30, d, size=size, dam=True)


def ghi_nho(slide, text):
    """Khung ghi nhớ xám, vạch vàng bên trái, nằm sát đáy."""
    cao = 92
    o = slide.shapes.add_shape(MSO_SHAPE.ROUNDED_RECTANGLE, _e(LE), _e(Y_GHI_NHO), _e(RONG), _e(cao))
    o.adjustments[0] = 0.12
    o.fill.solid()
    o.fill.fore_color.rgb = XAM_NEN
    o.line.fill.background()
    o.shadow.inherit = False
    v = slide.shapes.add_shape(MSO_SHAPE.RECTANGLE, _e(LE), _e(Y_GHI_NHO), _e(10), _e(cao))
    v.fill.solid()
    v.fill.fore_color.rgb = VANG
    v.line.fill.background()
    v.shadow.inherit = False
    chu(slide, LE + 36, Y_GHI_NHO, RONG - 72, cao, text, size=30, dam=True)


def nen_trang(slide):
    slide.background.fill.solid()
    slide.background.fill.fore_color.rgb = TRANG


def khung(prs, tieu_de=None, chan=None, co_ghi_nho=False):
    """Tạo một slide trắng, đặt tiêu đề và nhãn chuyên đề."""
    s = prs.slides.add_slide(prs.slide_layouts[6])
    nen_trang(s)
    if tieu_de:
        chu(s, LE, Y_TIEU_DE, RONG, 70, tieu_de, size=52, dam=True, giua_doc=False)
    if chan:
        chu(s, LE, Y_CHAN, RONG, 36, chan, size=24, dam=True, mau=XAM_NHAN, giua_doc=False)
    return s


# ---------------------------------------------------------------- mười kiểu


def _cot_phai(slide, ds, x, y, w):
    if ds:
        danh_sach_gach(slide, x, y, w, ds)


def kieu_pheu(s, d):
    """Phễu thu hẹp dần. d: {"muc": [{"ten","phu"}...], "ds": [...]}"""
    muc = d["muc"]
    co_ds = bool(d.get("ds"))
    w_max = 940 if co_ds else 1200
    x_giua = LE + (w_max / 2 if co_ds else RONG / 2)
    cao = 118
    khoang = 46
    y = Y_NOI_DUNG + 30
    for i, m in enumerate(muc):
        w = w_max * (1 - i * (0.45 / max(1, len(muc) - 1)))
        x = x_giua - w / 2
        cuoi = i == len(muc) - 1
        hop_chu(s, x, y, w, cao, m["ten"], size=46, nen=VANG if cuoi else None, phu=m.get("phu"))
        if not cuoi:
            mt = s.shapes.add_shape(MSO_SHAPE.ISOSCELES_TRIANGLE, _e(x_giua - 16), _e(y + cao + 8), _e(32), _e(28))
            mt.rotation = 180
            mt.fill.solid()
            mt.fill.fore_color.rgb = DEN
            mt.line.fill.background()
            mt.shadow.inherit = False
        y += cao + khoang
    if co_ds:
        _cot_phai(s, d["ds"], LE + w_max + 70, Y_NOI_DUNG + 40, RONG - w_max - 70)


def kieu_cot(s, d):
    """Cột cao dần. d: {"muc": [{"nhan","cao":0..1}...], "ds": [...]}"""
    muc = d["muc"]
    co_ds = bool(d.get("ds"))
    vung_w = 960 if co_ds else RONG
    day = Y_NOI_DUNG + CAO_NOI_DUNG - 40
    khoang = 20
    w = (vung_w - khoang * (len(muc) - 1)) / len(muc)
    for i, m in enumerate(muc):
        h = 170 + (CAO_NOI_DUNG - 230) * float(m.get("cao", (i + 1) / len(muc)))
        x = LE + i * (w + khoang)
        cuoi = i == len(muc) - 1
        hop(s, x, day - h, w, h, nen=VANG if cuoi else None)
        chu(s, x, day - h, w, h, m["nhan"], size=64, canh="giua")
    if co_ds:
        _cot_phai(s, d["ds"], LE + vung_w + 80, Y_NOI_DUNG + 60, RONG - vung_w - 80)


def kieu_ty_le(s, d):
    """Thanh chia đúng tỷ lệ. d: {"muc": [{"nhan","phan": số}...], "tren": [...]}"""
    muc = d["muc"]
    tong = sum(float(m["phan"]) for m in muc)
    y = Y_NOI_DUNG + 60
    if d.get("tren"):
        danh_sach_gach(s, LE, y, RONG, d["tren"])
        y += 96 * len(d["tren"]) + 60
    cao = 150
    x = LE
    for i, m in enumerate(muc):
        w = (RONG - 6 * (len(muc) - 1)) * float(m["phan"]) / tong
        nen = VANG if i == 0 else (RGBColor(0xE9, 0xE9, 0xE4) if i == 1 else None)
        hop(s, x, y, w, cao, nen=nen)
        chu(s, x, y, w, cao, f"{m['phan']:g}%" if d.get("phan_tram", True) else str(m["phan"]), size=54, canh="giua")
        chu(s, x, y + cao + 14, w, 44, m["nhan"], size=26, canh="giua")
        x += w + 6


def kieu_cong(s, d):
    """A + B → C. d: {"muc": [{"ten","mo_ta"} × 3]}"""
    muc = d["muc"]
    y = Y_NOI_DUNG + 90
    cao = 300
    w = (RONG - 180) / 3
    for i, m in enumerate(muc):
        x = LE + i * (w + 90)
        cuoi = i == len(muc) - 1
        hop(s, x, y, w, cao, nen=VANG if cuoi else None)
        chu(s, x + 24, y + 30, w - 48, 90, m["ten"], size=44, canh="giua")
        if m.get("mo_ta"):
            chu(s, x + 24, y + 130, w - 48, 140, m["mo_ta"], size=28, dam=False, mau=XAM_CHU, canh="giua")
        if not cuoi:
            dau = "+" if i == 0 else "→"
            chu(s, x + w, y, 90, cao, dau, size=56, canh="giua")


def kieu_the_ngang(s, d):
    """Chuỗi thẻ ngang. d: {"muc": [{"ten","mo_ta"}...], "nhan_manh": chỉ số}"""
    muc = d["muc"]
    y = Y_NOI_DUNG + 80
    cao = 320
    khoang = 26
    w = (RONG - khoang * (len(muc) - 1)) / len(muc)
    for i, m in enumerate(muc):
        x = LE + i * (w + khoang)
        hop(s, x, y, w, cao, nen=VANG if i == d.get("nhan_manh", -1) else None)
        chu(s, x + 28, y + 36, w - 56, 110, m["ten"], size=36, canh="giua")
        if m.get("mo_ta"):
            chu(s, x + 28, y + 150, w - 56, 140, m["mo_ta"], size=26, dam=False, mau=XAM_CHU, canh="giua")


def kieu_buoc_doc(s, d):
    """Các bước xếp dọc, có đánh số. d: {"muc": [{"ten","mo_ta"}...]}"""
    muc = d["muc"]
    y = Y_NOI_DUNG + 20
    cao = min(150, (CAO_NOI_DUNG - 40) / len(muc) - 20)
    for i, m in enumerate(muc):
        yy = y + i * (cao + 20)
        hop(s, LE, yy, 90, cao, nen=VANG if i == d.get("nhan_manh", -1) else None)
        chu(s, LE, yy, 90, cao, f"{i + 1:02d}", size=40, canh="giua")
        chu(s, LE + 120, yy, RONG - 120, cao * 0.55, m["ten"], size=36, giua_doc=False)
        if m.get("mo_ta"):
            chu(s, LE + 120, yy + cao * 0.52, RONG - 120, cao * 0.45, m["mo_ta"], size=26, dam=False, mau=XAM_CHU, giua_doc=False)


def kieu_so_sanh(s, d):
    """Hai thẻ so sánh. d: {"trai": {...}, "phai": {...}}"""
    y = Y_NOI_DUNG + 60
    cao = 420
    w = (RONG - 80) / 2
    for i, khoa in enumerate(["trai", "phai"]):
        m = d[khoa]
        x = LE + i * (w + 80)
        hop(s, x, y, w, cao, nen=VANG if khoa == d.get("nhan_manh") else None)
        chu(s, x + 34, y + 40, w - 68, 60, m.get("nhan", ""), size=26, mau=XAM_CHU, giua_doc=False)
        chu(s, x + 34, y + 110, w - 68, 110, m["ten"], size=44, giua_doc=False)
        if m.get("mo_ta"):
            chu(s, x + 34, y + 230, w - 68, 160, m["mo_ta"], size=28, dam=False, mau=XAM_CHU, giua_doc=False)


def kieu_danh_sach(s, d):
    """Chỉ một danh sách gạch ngang, chữ to. d: {"muc": [...]}"""
    muc = d["muc"]
    cao_dong = min(130, (CAO_NOI_DUNG - 20) / len(muc))
    danh_sach_gach(s, LE, Y_NOI_DUNG + 30, RONG, muc, size=36, cao_dong=cao_dong)


def kieu_anh_chu(s, d):
    """Ảnh bên trái, danh sách bên phải. d: {"anh": "duong/dan.png", "ds": [...]}"""
    w_anh = d.get("rong_anh", 760)
    y = Y_NOI_DUNG + 30
    cao = CAO_NOI_DUNG - 80
    try:
        s.shapes.add_picture(d["anh"], _e(LE), _e(y), _e(w_anh), _e(cao))
    except Exception as loi:  # ảnh thiếu thì để khung trống, không gãy cả bộ
        hop(s, LE, y, w_anh, cao)
        chu(s, LE, y, w_anh, cao, f"[thiếu ảnh: {loi}]", size=24, mau=XAM_NHAN, canh="giua")
    _cot_phai(s, d.get("ds", []), LE + w_anh + 70, y + 30, RONG - w_anh - 70)


def kieu_bia(s, d):
    """Trang bìa: nhãn nhỏ, tiêu đề rất to, vạch vàng, một câu."""
    chu(s, LE, 286, RONG, 50, d.get("nhan", ""), size=28, mau=XAM_NHAN, giua_doc=False)
    # Hộp tiêu đề cao 300px đủ cho 2 dòng 112px — trước để 260 nên vạch vàng
    # đè lên đuôi chữ dòng hai, lộ ra khi xuất PPTX rồi nhìn lại bằng mắt.
    chu(s, LE, 356, RONG, 300, d["ten"], size=112, giua_doc=False)
    o = s.shapes.add_shape(MSO_SHAPE.RECTANGLE, _e(LE), _e(700), _e(220), _e(16))
    o.fill.solid()
    o.fill.fore_color.rgb = VANG
    o.line.fill.background()
    o.shadow.inherit = False
    if d.get("mo_ta"):
        chu(s, LE, 764, RONG * 0.6, 120, d["mo_ta"], size=36, dam=False, mau=XAM_CHU, giua_doc=False)


def kieu_mo_phan(s, d):
    """Trang mở một chuyên đề: số thứ tự to + tên phần."""
    chu(s, LE, 380, 300, 200, d.get("so", ""), size=160, mau=VANG, giua_doc=False)
    chu(s, LE, 600, RONG, 180, d["ten"], size=72, giua_doc=False)


KIEU = {
    "pheu": kieu_pheu,
    "cot": kieu_cot,
    "ty_le": kieu_ty_le,
    "cong": kieu_cong,
    "the_ngang": kieu_the_ngang,
    "buoc_doc": kieu_buoc_doc,
    "so_sanh": kieu_so_sanh,
    "danh_sach": kieu_danh_sach,
    "anh_chu": kieu_anh_chu,
    "bia": kieu_bia,
    "mo_phan": kieu_mo_phan,
}


def dung(du_lieu, duong_ra):
    prs = Presentation()
    prs.slide_width = _e(1920)
    prs.slide_height = _e(1080)
    for i, d in enumerate(du_lieu):
        kieu = d.get("kieu", "danh_sach")
        if kieu not in KIEU:
            raise SystemExit(f"Slide {i + 1}: kiểu '{kieu}' không có. Chọn một trong: {', '.join(KIEU)}")
        s = khung(prs, d.get("tieu_de"), d.get("chan"))
        KIEU[kieu](s, d)
        if d.get("ghi_nho"):
            ghi_nho(s, d["ghi_nho"])
    prs.save(duong_ra)
    print(f"Xong: {len(du_lieu)} slide → {duong_ra}")


if __name__ == "__main__":
    doi_so = [a for a in sys.argv[1:]]
    if "--font" in doi_so:
        i = doi_so.index("--font")
        FONT = doi_so[i + 1]
        del doi_so[i : i + 2]
    if len(doi_so) < 2:
        raise SystemExit('Dùng: python lam-slide.py noi-dung.json ket-qua.pptx [--font "Be Vietnam Pro"]')
    with open(doi_so[0], encoding="utf-8") as f:
        dung(json.load(f), doi_so[1])
```
