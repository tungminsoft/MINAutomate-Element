# CSS Selector — Tổng Hợp Kiến Thức

## 1. Cú pháp tổng quát

```
Tên_thẻ[Điều_kiện]
```

- **`Tên_thẻ`**: tên phần tử HTML (`div`, `a`, `input`, …). Có thể dùng `*` để khớp **mọi tag**.
- **`[Điều_kiện]`**: bộ lọc theo thuộc tính / pseudo-class.
- Khác với XPath: CSS Selector **không có `//`** — mặc định tìm trong toàn bộ document, dùng dấu **cách** (space), `>`, `+`, `~` để diễn tả quan hệ.

---

## 2. Tên thẻ

| Cú pháp | Ý nghĩa |
|---|---|
| `div` | Mọi thẻ `<div>` |
| `a` | Mọi thẻ `<a>` |
| `*` | Mọi thẻ bất kỳ |

---

## 3. Bộ chọn cơ bản (Basic Selectors)

| Cú pháp | Ý nghĩa | Ví dụ |
|---|---|---|
| `#id` | Theo `id` | `#username` |
| `.class` | Theo `class` | `.btn-primary` |
| `tag.class` | Tag + class | `button.btn-primary` |
| `tag#id` | Tag + id | `input#email` |
| `.c1.c2` | Có **cả** class `c1` và `c2` | `.btn.active` |

---

## 4. Điều kiện theo thuộc tính

### 4.1. So khớp thuộc tính

| Cú pháp | Ý nghĩa |
|---|---|
| `[Thuộc_tính]` | Có thuộc tính (không quan tâm giá trị) |
| `[Thuộc_tính="Giá_trị"]` | Bằng **chính xác** giá trị |
| `[Thuộc_tính*="Giá_trị"]` | **Chứa** giá trị (contains) |
| `[Thuộc_tính^="Giá_trị"]` | **Bắt đầu bằng** giá trị |
| `[Thuộc_tính$="Giá_trị"]` | **Kết thúc bằng** giá trị |
| `[Thuộc_tính~="Giá_trị"]` | Chứa giá trị như **một từ** (cách bởi khoảng trắng) |
| `[Thuộc_tính\|="Giá_trị"]` | Bằng giá trị, hoặc bắt đầu bằng `Giá_trị-` (cho lang code: `en-US`) |

**Ví dụ:**
```css
input[required]
input[type="text"]
div[class*="btn"]
a[href^="https://"]
img[src$=".png"]
p[lang|="en"]
```

### 4.2. Không phân biệt HOA-thường

Thêm `i` trước dấu `]`:

```css
a[title="login" i]
input[type="TEXT" i]
```

---

## 5. Pseudo-class (Lớp giả)

### 5.1. Trạng thái / vị trí phổ biến

| Cú pháp | Ý nghĩa |
|---|---|
| `:hover` | Khi rê chuột |
| `:focus` | Khi được focus |
| `:checked` | Checkbox/radio được chọn |
| `:disabled` / `:enabled` | Bị/không bị disable |
| `:required` / `:optional` | Bắt buộc / tùy chọn |
| `:empty` | Không có node con |
| `:not(...)` | Phủ định |

### 5.2. Theo vị trí trong cha (Index)

| Cú pháp | Ý nghĩa |
|---|---|
| `:first-child` | Là con **đầu tiên** của cha |
| `:last-child` | Là con **cuối cùng** của cha |
| `:nth-child(n)` | Con thứ `n` (bắt đầu từ 1) |
| `:nth-last-child(n)` | Con thứ `n` đếm **từ cuối** |
| `:only-child` | Là con duy nhất |
| `:first-of-type` | Phần tử đầu tiên **cùng tag** trong cha |
| `:last-of-type` | Phần tử cuối cùng **cùng tag** |
| `:nth-of-type(n)` | Phần tử thứ `n` **cùng tag** |
| `:nth-last-of-type(n)` | Như trên, đếm từ cuối |

**Biểu thức cho `nth-child` / `nth-of-type`:**
- `2n` → các phần tử chẵn (2, 4, 6, …)
- `2n+1` hoặc `odd` → các phần tử lẻ
- `even` → các phần tử chẵn
- `3n+1` → 1, 4, 7, 10, …

**Ví dụ:**
```css
li:first-child
li:last-child
li:nth-child(3)
li:nth-child(odd)
tr:nth-of-type(2n)
p:not(.hidden)
input:not([disabled])
```

### 5.3. Kết hợp nhiều điều kiện

CSS không có `and` / `or` rõ rệt, nhưng có thể:

| Mục đích | Cú pháp |
|---|---|
| **AND** (cùng phần tử) | Ghép trực tiếp: `input[type="text"][required]` |
| **OR** | Dấu phẩy: `h1, h2, .title` |
| **NOT** | `:not(...)` |

**Ví dụ:**
```css
input[type="text"][name="email"]      /* AND */
button#ok, button#submit               /* OR */
li:not(.active)                        /* NOT */
```

### 5.4. So khớp theo text

> ⚠️ CSS Selector **không có** hàm tương đương `text()` / `contains(text())` của XPath.

---

## 6. Quan hệ giữa các phần tử (Combinators)

| Cú pháp | Ý nghĩa | Tương đương XPath |
|---|---|---|
| `A B` | `B` là **con/cháu bất kỳ** (mọi cấp) của `A` | `//A//B` |
| `A > B` | `B` là **con trực tiếp** của `A` | `//A/B` |
| `A + B` | `B` là anh em **liền kề ngay sau** `A` | `//A/following-sibling::B[1]` |
| `A ~ B` | `B` là anh em **bất kỳ đứng sau** `A` (cùng cha) | `//A/following-sibling::B` |

**Ví dụ:**
```css
form input              /* mọi <input> trong <form> */
ul > li                 /* <li> là con trực tiếp của <ul> */
label + input           /* <input> nằm ngay sau <label> */
h2 ~ p                  /* mọi <p> đứng sau <h2> cùng cha */
```

> ⚠️ CSS Selector **không có** combinator cho **cha / tổ tiên / anh em trước** (`parent`, `ancestor`, `preceding-sibling`).
> Đây là giới hạn lớn so với XPath. (Selector Level 4 có `:has(...)` để mô phỏng "phần tử chứa X" — xem mục 7.)

---

## 7. `:has()` — "có chứa" (Selectors Level 4)

`:has(...)` cho phép chọn phần tử **chứa** một phần tử khác, tương đương `//Xpath1[./Xpath2]` của XPath.

```css
div:has(> span.title)          /* <div> có <span class="title"> là con trực tiếp */
li:has(a[href^="https"])       /* <li> chứa link https bất kỳ cấp nào */
tr:has(td.error)               /* <tr> nào có <td class="error"> */
form:has(input:invalid)        /* <form> có input không hợp lệ */
```

> ✅ Trình duyệt hiện đại (Chrome/Edge ≥ 105, Safari ≥ 15.4, Firefox ≥ 121) đã hỗ trợ.

---

## 8. Pseudo-element (Phần tử giả)

| Cú pháp | Ý nghĩa |
|---|---|
| `::before` | Chèn nội dung **trước** phần tử |
| `::after` | Chèn nội dung **sau** phần tử |
| `::first-letter` | Ký tự đầu tiên |
| `::first-line` | Dòng đầu tiên |
| `::placeholder` | Placeholder của `<input>` |
| `::selection` | Vùng text user bôi đen |

> Pseudo-element dùng **hai dấu hai chấm** `::`. Chủ yếu phục vụ styling CSS, ít dùng trong automation.

---

## 9. Bảng tóm tắt nhanh (Cheat Sheet)

| Mục đích | XPath | CSS Selector |
|---|---|---|
| Theo id | `//*[@id="x"]` | `#x` |
| Theo class | `//*[@class="x"]` | `.x` |
| Theo tag | `//div` | `div` |
| Mọi tag | `//*` | `*` |
| Thuộc tính chính xác | `//a[@href="/"]` | `a[href="/"]` |
| Chứa | `//a[contains(@class,"nav")]` | `a[class*="nav"]` |
| Bắt đầu bằng | `//a[starts-with(@id,"i-")]` | `a[id^="i-"]` |
| Kết thúc bằng | `//img[ends-with(@src,".jpg")]` | `img[src$=".jpg"]` |
| AND | `[@a="1" and @b="2"]` | `[a="1"][b="2"]` |
| OR | `\|` (XPath 2.0) | `,` |
| NOT | `not(...)` | `:not(...)` |
| Bỏ qua hoa/thường | `translate(...)` | `[a="x" i]` |
| Con trực tiếp | `//A/B` | `A > B` |
| Con/cháu bất kỳ | `//A//B` | `A B` |
| Anh em liền kề sau | `following-sibling::B[1]` | `A + B` |
| Anh em bất kỳ sau | `following-sibling::B` | `A ~ B` |
| Cha | `parent::A` | ❌ (không có) |
| Tổ tiên | `ancestor::A` | ❌ (không có) |
| Anh em trước | `preceding-sibling::A` | ❌ (không có) |
| Theo text | `[text()="X"]` | ❌ (không có) |
| Chứa con | `[./X]` | `:has(X)` (Level 4) |
| Phần tử thứ N | `(//div)[N]` | `div:nth-of-type(N)` (theo cha) |
| Phần tử cuối | `(//tr)[last()]` | `tr:last-of-type` |

---

## 10. Mẹo sử dụng

- **Ưu tiên `id` > thuộc tính ổn định > class** để selector bền vững.
- Tránh class do framework auto-generate (vd: `css-1a2b3c` của styled-components, Tailwind JIT) — đổi liên tục giữa các build.
- Test nhanh CSS Selector trong **DevTools** của Chrome:
  - Console: `document.querySelectorAll(".btn-primary")`
  - Elements tab: `Ctrl+F` → dán selector vào ô tìm kiếm.
- Khi cần **lọc theo text** hoặc **đi ngược lên cha/tổ tiên** → dùng XPath thay vì CSS.
- Khi cần **chọn phần tử chứa X** → dùng `:has(...)` (CSS Level 4) hoặc XPath `[./X]`.
- CSS Selector thường **nhanh hơn XPath** trong trình duyệt → ưu tiên CSS khi đủ biểu đạt.
