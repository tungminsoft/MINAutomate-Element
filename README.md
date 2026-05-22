# MinAutomate Helper — Knowledge Base

> Tổng hợp kiến thức về **XPath** và **CSS Selector** — hai công cụ định vị phần tử quan trọng nhất trong web automation, web scraping và UI testing.

## 📚 Nội dung

Mỗi chủ đề có **3 ngôn ngữ**: Tiếng Việt (`vi`), English (`en`), ไทย (`th`).

### XPath

| Ngôn ngữ / Language | File |
|---|---|
| 🇻🇳 Tiếng Việt | [xpath-summary.vi.md](xpath-summary.vi.md) |
| 🇬🇧 English | [xpath-summary.en.md](xpath-summary.en.md) |
| 🇹🇭 ไทย | [xpath-summary.th.md](xpath-summary.th.md) |

### CSS Selector

| Ngôn ngữ / Language | File |
|---|---|
| 🇻🇳 Tiếng Việt | [css-selector-summary.vi.md](css-selector-summary.vi.md) |
| 🇬🇧 English | [css-selector-summary.en.md](css-selector-summary.en.md) |
| 🇹🇭 ไทย | [css-selector-summary.th.md](css-selector-summary.th.md) |

## 🎯 Phạm vi

Mỗi file đều bao gồm:

- **Cú pháp cơ bản** — cấu trúc tổng quát của ngôn ngữ truy vấn
- **So khớp thuộc tính** — `=`, `contains`, `starts-with`, `ends-with`, …
- **Kết hợp điều kiện** — AND / OR / NOT
- **Case-insensitive matching** — bỏ qua hoa-thường
- **Chuẩn hóa khoảng trắng** — `normalize-space()` (XPath only)
- **So khớp theo text** — `text()`, `contains(text())` (XPath only)
- **Quan hệ giữa node** — con / cháu / cha / tổ tiên / anh em
- **Chọn theo thứ tự** — index, `last()`, `nth-child`, `nth-of-type`
- **Pseudo-class & `:has()`** — đặc thù CSS
- **Cheat Sheet đối chiếu** — bảng so sánh XPath ↔ CSS
- **Mẹo sử dụng** — test trong Chrome DevTools, khi nào nên chọn cái nào

## 🔧 Quy ước đặt tên file

Theo chuẩn **BCP 47 locale suffix** — pattern phổ biến cho framework đa ngôn ngữ (Docusaurus, Mintlify, i18next, Astro Content Collections):

```
{topic}-summary.{locale}.md
```

Ví dụ: `xpath-summary.vi.md`, `css-selector-summary.en.md`.

## 📖 Khi nào dùng XPath vs CSS Selector?

| Tình huống | Nên dùng |
|---|---|
| Lọc theo text content | **XPath** (CSS không hỗ trợ) |
| Đi ngược lên cha / tổ tiên | **XPath** (CSS không có `parent::`, `ancestor::`) |
| Tìm anh em đứng trước | **XPath** (CSS không có `preceding-sibling`) |
| Chọn phần tử chứa X | Cả hai — XPath `[./X]` hoặc CSS `:has(X)` (Level 4) |
| Selector ngắn gọn, hiệu năng cao | **CSS Selector** (nhanh hơn trong browser) |
| Tương thích trình duyệt cũ | **CSS Selector** (XPath không có trong CSS engine) |

## 🤝 Đóng góp

Pull request luôn được chào đón. Khi cập nhật một file, vui lòng **đồng bộ cả 3 bản dịch** (vi / en / th) để duy trì tính nhất quán.

## 📄 License

MIT
