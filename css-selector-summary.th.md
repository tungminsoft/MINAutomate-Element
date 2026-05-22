# CSS Selector — สรุปความรู้

## 1. ไวยากรณ์ทั่วไป

```
ชื่อแท็ก[เงื่อนไข]
```

- **`ชื่อแท็ก`**: ชื่อ element ของ HTML (`div`, `a`, `input`, …) ใช้ `*` เพื่อจับคู่ **ทุกแท็ก**
- **`[เงื่อนไข]`**: ตัวกรองตามแอตทริบิวต์ / pseudo-class
- ต่างจาก XPath: CSS Selector **ไม่มี `//`** — ค้นในเอกสารทั้งหมดโดยปริยาย และใช้ **ช่องว่าง (space)**, `>`, `+`, `~` แทนความสัมพันธ์

---

## 2. ชื่อแท็ก

| ไวยากรณ์ | ความหมาย |
|---|---|
| `div` | ทุกแท็ก `<div>` |
| `a` | ทุกแท็ก `<a>` |
| `*` | ทุกแท็ก |

---

## 3. Basic selectors

| ไวยากรณ์ | ความหมาย | ตัวอย่าง |
|---|---|---|
| `#id` | ตาม `id` | `#username` |
| `.class` | ตาม `class` | `.btn-primary` |
| `tag.class` | tag + class | `button.btn-primary` |
| `tag#id` | tag + id | `input#email` |
| `.c1.c2` | มี **ทั้ง** class `c1` และ `c2` | `.btn.active` |

---

## 4. เงื่อนไขตามแอตทริบิวต์

### 4.1. ตัวเทียบแอตทริบิวต์

| ไวยากรณ์ | ความหมาย |
|---|---|
| `[attr]` | มีแอตทริบิวต์ (ค่าใดก็ได้) |
| `[attr="value"]` | **เท่ากันพอดี** |
| `[attr*="value"]` | **มี** ค่านี้อยู่ (substring) |
| `[attr^="value"]` | **ขึ้นต้นด้วย** ค่านี้ |
| `[attr$="value"]` | **ลงท้ายด้วย** ค่านี้ |
| `[attr~="value"]` | มีค่านี้เป็น **คำ** (คั่นด้วยช่องว่าง) |
| `[attr\|="value"]` | เท่ากับ value หรือขึ้นต้นด้วย `value-` (สำหรับ lang code: `en-US`) |

**ตัวอย่าง:**
```css
input[required]
input[type="text"]
div[class*="btn"]
a[href^="https://"]
img[src$=".png"]
p[lang|="en"]
```

### 4.2. ไม่สนใจตัวพิมพ์ใหญ่-เล็ก

เพิ่ม `i` ก่อน `]` ปิด:

```css
a[title="login" i]
input[type="TEXT" i]
```

---

## 5. Pseudo-class

### 5.1. สถานะ / ตำแหน่ง ที่พบบ่อย

| ไวยากรณ์ | ความหมาย |
|---|---|
| `:hover` | เมื่อเอาเมาส์ชี้ |
| `:focus` | เมื่อ focus |
| `:checked` | Checkbox/radio ถูกเลือก |
| `:disabled` / `:enabled` | ปิด / เปิดใช้งาน |
| `:required` / `:optional` | บังคับกรอก / ไม่บังคับ |
| `:empty` | ไม่มี node ลูก |
| `:not(...)` | กลับค่า |

### 5.2. ตำแหน่งในพ่อแม่ (Index)

| ไวยากรณ์ | ความหมาย |
|---|---|
| `:first-child` | เป็น **ลูกตัวแรก** ของพ่อแม่ |
| `:last-child` | เป็น **ลูกตัวสุดท้าย** ของพ่อแม่ |
| `:nth-child(n)` | ลูกตัวที่ `n` (เริ่มจาก 1) |
| `:nth-last-child(n)` | ลูกตัวที่ `n` **นับจากท้าย** |
| `:only-child` | เป็นลูกเพียงตัวเดียว |
| `:first-of-type` | element ตัวแรก **ของ tag เดียวกัน** ในพ่อแม่ |
| `:last-of-type` | element ตัวสุดท้าย **ของ tag เดียวกัน** |
| `:nth-of-type(n)` | element ตัวที่ `n` **ของ tag เดียวกัน** |
| `:nth-last-of-type(n)` | เหมือนข้างบน นับจากท้าย |

**นิพจน์สำหรับ `nth-child` / `nth-of-type`:**
- `2n` → เลขคู่ (2, 4, 6, …)
- `2n+1` หรือ `odd` → เลขคี่
- `even` → เลขคู่
- `3n+1` → 1, 4, 7, 10, …

**ตัวอย่าง:**
```css
li:first-child
li:last-child
li:nth-child(3)
li:nth-child(odd)
tr:nth-of-type(2n)
p:not(.hidden)
input:not([disabled])
```

### 5.3. รวมหลายเงื่อนไข

CSS ไม่มี `and` / `or` ชัดเจน แต่ทำได้:

| เป้าหมาย | ไวยากรณ์ |
|---|---|
| **AND** (element เดียวกัน) | เชื่อมตรง ๆ: `input[type="text"][required]` |
| **OR** | คอมม่า: `h1, h2, .title` |
| **NOT** | `:not(...)` |

**ตัวอย่าง:**
```css
input[type="text"][name="email"]      /* AND */
button#ok, button#submit               /* OR */
li:not(.active)                        /* NOT */
```

### 5.4. จับคู่ตามข้อความ

> ⚠️ CSS Selector **ไม่มี** ฟังก์ชันที่เทียบเท่ากับ `text()` / `contains(text())` ของ XPath ถ้าต้องกรองตามข้อความให้ใช้ JavaScript หรือ XPath

---

## 6. Combinators (ความสัมพันธ์ระหว่าง element)

| ไวยากรณ์ | ความหมาย | เทียบเท่า XPath |
|---|---|---|
| `A B` | `B` เป็น **ลูกหลานทุกระดับ** ของ `A` | `//A//B` |
| `A > B` | `B` เป็น **ลูกโดยตรง** ของ `A` | `//A/B` |
| `A + B` | `B` เป็นพี่น้อง **ตัวถัดไปทันที** ของ `A` | `//A/following-sibling::B[1]` |
| `A ~ B` | `B` เป็นพี่น้อง **ตัวใดก็ได้ที่อยู่หลัง** `A` (พ่อแม่เดียวกัน) | `//A/following-sibling::B` |

**ตัวอย่าง:**
```css
form input              /* <input> ทุกตัวใน <form> */
ul > li                 /* <li> ที่เป็นลูกโดยตรงของ <ul> */
label + input           /* <input> ที่อยู่ติดหลัง <label> */
h2 ~ p                  /* <p> ทุกตัวหลัง <h2> ในพ่อแม่เดียวกัน */
```

> ⚠️ CSS Selector **ไม่มี** combinator สำหรับ **พ่อแม่ / บรรพบุรุษ / พี่น้องก่อนหน้า** (`parent`, `ancestor`, `preceding-sibling`) นี่เป็นข้อจำกัดสำคัญเทียบกับ XPath (Selector Level 4 มี `:has(...)` ช่วยจำลอง "element ที่มี X อยู่ข้างใน" — ดูข้อ 7)

---

## 7. `:has()` — "มีอยู่ข้างใน" (Selectors Level 4)

`:has(...)` ให้เลือก element ที่ **มี** element อื่นอยู่ข้างใน เทียบเท่า `//Xpath1[./Xpath2]` ของ XPath

```css
div:has(> span.title)          /* <div> ที่มี <span class="title"> เป็นลูกโดยตรง */
li:has(a[href^="https"])       /* <li> ที่มีลิงก์ https อยู่ในระดับใดก็ได้ */
tr:has(td.error)               /* <tr> ที่มี <td class="error"> */
form:has(input:invalid)        /* <form> ที่มี input ไม่ผ่านการตรวจสอบ */
```

> ✅ รองรับในเบราว์เซอร์รุ่นใหม่: Chrome/Edge ≥ 105, Safari ≥ 15.4, Firefox ≥ 121

---

## 8. Pseudo-element

| ไวยากรณ์ | ความหมาย |
|---|---|
| `::before` | แทรกเนื้อหา **ก่อน** element |
| `::after` | แทรกเนื้อหา **หลัง** element |
| `::first-letter` | ตัวอักษรตัวแรก |
| `::first-line` | บรรทัดแรก |
| `::placeholder` | placeholder ของ `<input>` |
| `::selection` | ส่วนข้อความที่ผู้ใช้ลากเลือก |

> Pseudo-element ใช้ **โคลอนสองตัว** `::` ส่วนใหญ่ใช้สำหรับการจัดสไตล์ CSS ไม่ค่อยใช้ใน automation

---

## 9. ตารางสรุปเร็ว (Cheat Sheet)

| เป้าหมาย | XPath | CSS Selector |
|---|---|---|
| ตาม id | `//*[@id="x"]` | `#x` |
| ตาม class | `//*[@class="x"]` | `.x` |
| ตาม tag | `//div` | `div` |
| ทุก tag | `//*` | `*` |
| แอตทริบิวต์พอดี | `//a[@href="/"]` | `a[href="/"]` |
| มีบางส่วน | `//a[contains(@class,"nav")]` | `a[class*="nav"]` |
| ขึ้นต้นด้วย | `//a[starts-with(@id,"i-")]` | `a[id^="i-"]` |
| ลงท้ายด้วย | `//img[ends-with(@src,".jpg")]` | `img[src$=".jpg"]` |
| AND | `[@a="1" and @b="2"]` | `[a="1"][b="2"]` |
| OR | `\|` (XPath 2.0) | `,` |
| NOT | `not(...)` | `:not(...)` |
| ไม่สน case | `translate(...)` | `[a="x" i]` |
| ลูกโดยตรง | `//A/B` | `A > B` |
| ลูกหลานใดก็ได้ | `//A//B` | `A B` |
| พี่น้องตัวถัดไปทันที | `following-sibling::B[1]` | `A + B` |
| พี่น้องตัวใดก็ได้หลัง | `following-sibling::B` | `A ~ B` |
| พ่อแม่ | `parent::A` | ❌ (ไม่มี) |
| บรรพบุรุษ | `ancestor::A` | ❌ (ไม่มี) |
| พี่น้องก่อนหน้า | `preceding-sibling::A` | ❌ (ไม่มี) |
| ตามข้อความ | `[text()="X"]` | ❌ (ไม่มี) |
| มีลูกเป็น | `[./X]` | `:has(X)` (Level 4) |
| ตัวที่ N | `(//div)[N]` | `div:nth-of-type(N)` (ต่อพ่อแม่) |
| ตัวสุดท้าย | `(//tr)[last()]` | `tr:last-of-type` |

---

## 10. เคล็ดลับการใช้งาน

- **ลำดับ `id` > แอตทริบิวต์ที่เสถียร > class** เพื่อให้ selector ทนทาน
- หลีกเลี่ยง class ที่ framework สร้างอัตโนมัติ (เช่น `css-1a2b3c` ของ styled-components, Tailwind JIT) — เปลี่ยนทุก build
- ทดสอบ CSS Selector เร็ว ๆ ใน **DevTools** ของ Chrome:
  - Console: `document.querySelectorAll(".btn-primary")`
  - แท็บ Elements: `Ctrl+F` → วาง selector ในช่องค้นหา
- เมื่อต้อง **กรองตามข้อความ** หรือ **ย้อนขึ้นไปยังพ่อแม่/บรรพบุรุษ** → ใช้ XPath แทน
- เมื่อต้อง **เลือก element ที่มี X อยู่ข้างใน** → ใช้ `:has(...)` (CSS Level 4) หรือ XPath `[./X]`
- โดยทั่วไป CSS Selector **เร็วกว่า XPath** ในเบราว์เซอร์ → ใช้ CSS ถ้าเพียงพอ
