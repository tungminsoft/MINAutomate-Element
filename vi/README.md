# MinAutomate Helper — Knowledge Base

**[🇬🇧 English](../en/README.md)** · **🇻🇳 Tiếng Việt** · **[🇹🇭 ไทย](../th/README.md)**

> Tổng hợp kiến thức về **XPath** và **CSS Selector** — hai công cụ định vị phần tử quan trọng nhất trong web automation, web scraping và UI testing.

## 📚 Nội dung

| Chủ đề | File |
|---|---|
| XPath | [xpath.md](xpath.md) |
| CSS Selector | [css-selector.md](css-selector.md) |

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

Pull request luôn được chào đón. Khi cập nhật một file, vui lòng **đồng bộ cả 3 bản dịch** (en / vi / th) để duy trì tính nhất quán.

## 📄 License

MIT
