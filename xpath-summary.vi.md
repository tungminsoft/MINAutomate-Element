# XPath — Tổng Hợp Kiến Thức

## 1. Cú pháp tổng quát

```
//Tên_thẻ[Điều_kiện]
```

- **`//`**: tìm ở bất kỳ vị trí nào trong cây DOM (không bắt buộc bắt đầu từ root).
- **`Tên_thẻ`**: tên phần tử HTML/XML (`div`, `a`, `input`, …). Có thể dùng `*` để khớp **mọi tag**.
- **`[Điều_kiện]`**: bộ lọc (predicate) để chọn đúng phần tử mong muốn.

---

## 2. Tên thẻ

| Cú pháp | Ý nghĩa |
|---|---|
| `//div` | Mọi thẻ `<div>` |
| `//a` | Mọi thẻ `<a>` |
| `//*` | Mọi thẻ bất kỳ |

---

## 3. Điều kiện (Predicate)

### 3.1. So khớp theo thuộc tính

| Cú pháp | Ý nghĩa |
|---|---|
| `[@Thuộc_tính="Giá_trị"]` | Thuộc tính **bằng chính xác** giá trị |
| `[contains(@Thuộc_tính,"Giá_trị")]` | Thuộc tính **chứa** giá trị |
| `[starts-with(@Thuộc_tính,"Giá_trị")]` | Thuộc tính **bắt đầu bằng** giá trị |
| `[ends-with(@Thuộc_tính,"Giá_trị")]` | Thuộc tính **kết thúc bằng** giá trị |

**Ví dụ:**
```xpath
//input[@id="username"]
//div[contains(@class,"btn-primary")]
//a[starts-with(@href,"https://")]
//img[ends-with(@src,".png")]
```

### 3.2. Lọc theo XPath con (lồng XPath)

```xpath
//Xpath1[./Xpath2]
```
→ Chọn `Xpath1` mà **bên trong có chứa** `Xpath2`.

**Ví dụ:**
```xpath
//div[./span[@class="title"]]
```
→ Chọn `<div>` mà bên trong có `<span class="title">`.

### 3.3. Kết hợp nhiều điều kiện

| Toán tử | Ý nghĩa |
|---|---|
| `and` | Cả hai điều kiện đều đúng |
| `or` | Một trong hai đúng |
| `not(...)` | Phủ định |

**Ví dụ:**
```xpath
//input[@type="text" and @name="email"]
//button[@id="ok" or @id="submit"]
//div[not(@class="hidden")]
```

### 3.4. Không phân biệt HOA-thường

```xpath
//Tên_thẻ[translate(@Thuộc_tính,
    'ABCDEFGHIJKLMNOPQRSTUVWXYZ',
    'abcdefghijklmnopqrstuvwxyz')="giá_trị"]
```

**Ví dụ:**
```xpath
//a[translate(@title,'ABCDEFGHIJKLMNOPQRSTUVWXYZ','abcdefghijklmnopqrstuvwxyz')="login"]
```

### 3.5. Chuẩn hóa khoảng trắng (`normalize-space`)

Hàm `normalize-space()` sẽ:
- Cắt khoảng trắng **đầu và cuối** chuỗi.
- Rút gọn nhiều khoảng trắng liên tiếp (space, tab, xuống dòng) **về một dấu cách**.

Rất hữu ích khi text/thuộc tính bị thừa khoảng trắng do format HTML.

**Cú pháp:**
```xpath
//Tên_thẻ[normalize-space(text())="Giá_trị"]
//Tên_thẻ[normalize-space(@Thuộc_tính)="Giá_trị"]
```

**Ví dụ:**
```xpath
//button[normalize-space(text())="Đăng nhập"]
//a[normalize-space()="Trang chủ"]                  // gọn hơn, áp dụng cho text của node hiện tại
//div[contains(normalize-space(.),"Xin chào")]      // áp dụng cho toàn bộ text gộp của node
```

> 💡 `normalize-space(.)` (dấu chấm) lấy **toàn bộ text** của phần tử kể cả text trong các tag con — rất hữu ích khi text bị bọc trong `<span>` lồng nhau.

### 3.6. So khớp theo text

Thay `@Thuộc_tính` bằng `text()` để so với nội dung text của phần tử.

**Ví dụ:**
```xpath
//button[text()="Đăng nhập"]
//span[contains(text(),"Xin chào")]
//h1[starts-with(text(),"Welcome")]
```

---

## 4. Nhiều cấp (Quan hệ giữa các node)

### 4.1. Cấp con/cháu

| Cú pháp | Ý nghĩa |
|---|---|
| `//Xpath1/Xpath2` | `Xpath2` là **con trực tiếp** của `Xpath1` |
| `//Xpath1//Xpath2` | `Xpath2` là **con/cháu bất kỳ** (mọi cấp) của `Xpath1` |

### 4.2. Cấp cha/tổ tiên

| Cú pháp | Ý nghĩa |
|---|---|
| `//Xpath1/parent::Xpath2` | Cha trực tiếp của `Xpath1` (phải khớp `Xpath2`) |
| `//Xpath1/ancestor::Xpath2` | Mọi tổ tiên của `Xpath1` (khớp `Xpath2`) |

### 4.3. Anh em / phần tử kế trước - kế sau

| Cú pháp | Ý nghĩa |
|---|---|
| `//Xpath1/preceding::Xpath2` | Mọi node **đứng trước** `Xpath1` trong document |
| `//Xpath1/preceding-sibling::Xpath2` | Anh/chị **cùng cha**, đứng trước `Xpath1` |
| `//Xpath1/following::Xpath2` | Mọi node **đứng sau** `Xpath1` trong document |
| `//Xpath1/following-sibling::Xpath2` | Anh/em **cùng cha**, đứng sau `Xpath1` |

**Ví dụ:**
```xpath
//label[text()="Email"]/following-sibling::input
//td[@class="name"]/parent::tr
//div[@id="content"]/ancestor::section
```

---

## 5. Chọn theo thứ tự (Index)

```
(//Tên_thẻ[Điều_kiện])[index]
```

- `index` bắt đầu từ **1**.
- `last()` → phần tử **cuối cùng**.
- Có thể dùng phép tính: `last()-1` → phần tử áp chót.

**Ví dụ:**
```xpath
(//div[@class="item"])[1]          // Phần tử đầu tiên
(//div[@class="item"])[3]          // Phần tử thứ 3
(//div[@class="item"])[last()]     // Phần tử cuối
(//div[@class="item"])[last()-1]   // Phần tử áp chót
```

> ⚠️ **Lưu ý**: `(//div)[1]` khác `//div[1]`
> - `(//div)[1]`: phần tử `<div>` đầu tiên trong toàn bộ document.
> - `//div[1]`: mỗi `<div>` là con đầu tiên trong phạm vi cha của nó.

---

## 6. Bảng tóm tắt nhanh (Cheat Sheet)

| Mục đích | Cú pháp ví dụ |
|---|---|
| Khớp chính xác thuộc tính | `//a[@href="/home"]` |
| Chứa một phần | `//a[contains(@class,"nav")]` |
| Bắt đầu bằng | `//a[starts-with(@id,"item-")]` |
| Kết thúc bằng | `//img[ends-with(@src,".jpg")]` |
| Theo text | `//button[text()="OK"]` |
| Nhiều điều kiện | `//input[@type="text" and @required]` |
| Phủ định | `//li[not(@class="active")]` |
| Bỏ qua hoa/thường | `//*[translate(@id,'ABC...','abc...')="login"]` |
| Con trực tiếp | `//ul/li` |
| Con/cháu bất kỳ | `//form//input` |
| Cha | `//span/parent::div` |
| Tổ tiên | `//a/ancestor::section` |
| Anh em sau | `//label/following-sibling::input` |
| Anh em trước | `//input/preceding-sibling::label` |
| Phần tử thứ N | `(//div[@class="row"])[2]` |
| Phần tử cuối | `(//tr)[last()]` |

---

## 7. Mẹo sử dụng

- **Ưu tiên `id` > `name` > `class` > `text()`** để XPath bền vững khi DOM thay đổi.
- Hạn chế dùng `//` lồng nhau nhiều cấp → chậm và dễ vỡ khi UI cập nhật.
- Khi text **đa ngôn ngữ / có dấu**, ưu tiên `contains()` để giảm rủi ro.
- Test nhanh XPath ngay trong **DevTools** của Chrome:
  - Console: `$x("//div[@id='main']")`
  - Elements tab: `Ctrl+F` → dán XPath vào ô tìm kiếm.
