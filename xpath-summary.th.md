# XPath — สรุปความรู้

## 1. ไวยากรณ์ทั่วไป

```
//ชื่อแท็ก[เงื่อนไข]
```

- **`//`**: ค้นหาทุกตำแหน่งใน DOM tree (ไม่จำเป็นต้องเริ่มจาก root)
- **`ชื่อแท็ก`**: ชื่อ element ของ HTML/XML (`div`, `a`, `input`, …) ใช้ `*` เพื่อจับคู่ **ทุกแท็ก**
- **`[เงื่อนไข]`**: ตัวกรอง (predicate) เพื่อเลือก element ที่ต้องการ

---

## 2. ชื่อแท็ก

| ไวยากรณ์ | ความหมาย |
|---|---|
| `//div` | ทุกแท็ก `<div>` |
| `//a` | ทุกแท็ก `<a>` |
| `//*` | ทุกแท็ก |

---

## 3. เงื่อนไข (Predicate)

### 3.1. จับคู่ตามแอตทริบิวต์

| ไวยากรณ์ | ความหมาย |
|---|---|
| `[@attr="value"]` | แอตทริบิวต์ **เท่ากันพอดี** กับค่า |
| `[contains(@attr,"value")]` | แอตทริบิวต์ **มี** ค่านี้อยู่ |
| `[starts-with(@attr,"value")]` | แอตทริบิวต์ **ขึ้นต้นด้วย** ค่านี้ |
| `[ends-with(@attr,"value")]` | แอตทริบิวต์ **ลงท้ายด้วย** ค่านี้ |

**ตัวอย่าง:**
```xpath
//input[@id="username"]
//div[contains(@class,"btn-primary")]
//a[starts-with(@href,"https://")]
//img[ends-with(@src,".png")]
```

### 3.2. กรองด้วย XPath ซ้อน

```xpath
//Xpath1[./Xpath2]
```
→ เลือก `Xpath1` ที่ **มี** `Xpath2` อยู่ข้างใน

**ตัวอย่าง:**
```xpath
//div[./span[@class="title"]]
```
→ เลือก `<div>` ที่ข้างในมี `<span class="title">`

### 3.3. รวมหลายเงื่อนไข

| ตัวดำเนินการ | ความหมาย |
|---|---|
| `and` | ต้องเป็นจริงทั้งสองเงื่อนไข |
| `or` | เป็นจริงอย่างน้อยหนึ่งเงื่อนไข |
| `not(...)` | กลับค่า (negation) |

**ตัวอย่าง:**
```xpath
//input[@type="text" and @name="email"]
//button[@id="ok" or @id="submit"]
//div[not(@class="hidden")]
```

### 3.4. ไม่สนใจตัวพิมพ์ใหญ่-เล็ก

```xpath
//ชื่อแท็ก[translate(@attr,
    'ABCDEFGHIJKLMNOPQRSTUVWXYZ',
    'abcdefghijklmnopqrstuvwxyz')="value"]
```

**ตัวอย่าง:**
```xpath
//a[translate(@title,'ABCDEFGHIJKLMNOPQRSTUVWXYZ','abcdefghijklmnopqrstuvwxyz')="login"]
```

### 3.5. ปรับช่องว่างให้เป็นมาตรฐาน (`normalize-space`)

ฟังก์ชัน `normalize-space()` จะ:
- ตัดช่องว่าง **ต้นและท้าย** ข้อความ
- ยุบช่องว่างต่อเนื่อง (space, tab, newline) **ให้เหลือเพียงช่องว่างเดียว**

มีประโยชน์มากเมื่อข้อความ/แอตทริบิวต์มีช่องว่างเกินจากการจัดรูปแบบ HTML

**ไวยากรณ์:**
```xpath
//ชื่อแท็ก[normalize-space(text())="value"]
//ชื่อแท็ก[normalize-space(@attr)="value"]
```

**ตัวอย่าง:**
```xpath
//button[normalize-space(text())="เข้าสู่ระบบ"]
//a[normalize-space()="หน้าแรก"]                    // สั้นกว่า ใช้กับ text ของ node ปัจจุบัน
//div[contains(normalize-space(.),"สวัสดี")]        // ใช้กับ text ทั้งหมดของ node
```

> 💡 `normalize-space(.)` (จุด) จะอ่าน **ข้อความทั้งหมด** ของ element รวมทั้งข้อความใน tag ลูก — เหมาะมากเมื่อข้อความถูกห่อด้วย `<span>` ซ้อนกัน

### 3.6. จับคู่ตามข้อความ

แทน `@attr` ด้วย `text()` เพื่อเทียบกับข้อความใน element

**ตัวอย่าง:**
```xpath
//button[text()="เข้าสู่ระบบ"]
//span[contains(text(),"สวัสดี")]
//h1[starts-with(text(),"ยินดีต้อนรับ")]
```

---

## 4. หลายระดับ (ความสัมพันธ์ระหว่าง node)

### 4.1. ลูก / ลูกหลาน

| ไวยากรณ์ | ความหมาย |
|---|---|
| `//Xpath1/Xpath2` | `Xpath2` เป็น **ลูกโดยตรง** ของ `Xpath1` |
| `//Xpath1//Xpath2` | `Xpath2` เป็น **ลูกหลานที่ระดับใดก็ได้** ของ `Xpath1` |

### 4.2. พ่อแม่ / บรรพบุรุษ

| ไวยากรณ์ | ความหมาย |
|---|---|
| `//Xpath1/parent::Xpath2` | พ่อแม่โดยตรงของ `Xpath1` (ต้องตรงกับ `Xpath2`) |
| `//Xpath1/ancestor::Xpath2` | บรรพบุรุษทุกระดับของ `Xpath1` (ที่ตรงกับ `Xpath2`) |

### 4.3. พี่น้อง / ก่อน-หลัง

| ไวยากรณ์ | ความหมาย |
|---|---|
| `//Xpath1/preceding::Xpath2` | ทุก node ที่อยู่ **ก่อน** `Xpath1` ในเอกสาร |
| `//Xpath1/preceding-sibling::Xpath2` | พี่น้อง **พ่อแม่เดียวกัน** ที่อยู่ก่อน `Xpath1` |
| `//Xpath1/following::Xpath2` | ทุก node ที่อยู่ **หลัง** `Xpath1` ในเอกสาร |
| `//Xpath1/following-sibling::Xpath2` | พี่น้อง **พ่อแม่เดียวกัน** ที่อยู่หลัง `Xpath1` |

**ตัวอย่าง:**
```xpath
//label[text()="อีเมล"]/following-sibling::input
//td[@class="name"]/parent::tr
//div[@id="content"]/ancestor::section
```

---

## 5. เลือกตามลำดับ (Index)

```
(//ชื่อแท็ก[เงื่อนไข])[index]
```

- `index` เริ่มจาก **1**
- `last()` → element **สุดท้าย**
- ใช้คำนวณได้: `last()-1` → ก่อนสุดท้าย

**ตัวอย่าง:**
```xpath
(//div[@class="item"])[1]          // ตัวแรก
(//div[@class="item"])[3]          // ตัวที่ 3
(//div[@class="item"])[last()]     // ตัวสุดท้าย
(//div[@class="item"])[last()-1]   // ก่อนสุดท้าย
```

> ⚠️ **หมายเหตุ**: `(//div)[1]` ต่างจาก `//div[1]`
> - `(//div)[1]`: `<div>` **ตัวแรกในเอกสารทั้งหมด**
> - `//div[1]`: `<div>` แต่ละตัวที่เป็น **ลูกตัวแรกของพ่อแม่ตัวเอง**

---

## 6. ตารางสรุปเร็ว (Cheat Sheet)

| เป้าหมาย | ไวยากรณ์ตัวอย่าง |
|---|---|
| จับคู่แอตทริบิวต์พอดี | `//a[@href="/home"]` |
| มีบางส่วน | `//a[contains(@class,"nav")]` |
| ขึ้นต้นด้วย | `//a[starts-with(@id,"item-")]` |
| ลงท้ายด้วย | `//img[ends-with(@src,".jpg")]` |
| ตามข้อความ | `//button[text()="OK"]` |
| หลายเงื่อนไข | `//input[@type="text" and @required]` |
| กลับค่า | `//li[not(@class="active")]` |
| ไม่สน case | `//*[translate(@id,'ABC...','abc...')="login"]` |
| ลูกโดยตรง | `//ul/li` |
| ลูกหลานใดก็ได้ | `//form//input` |
| พ่อแม่ | `//span/parent::div` |
| บรรพบุรุษ | `//a/ancestor::section` |
| พี่น้องหลัง | `//label/following-sibling::input` |
| พี่น้องก่อน | `//input/preceding-sibling::label` |
| ตัวที่ N | `(//div[@class="row"])[2]` |
| ตัวสุดท้าย | `(//tr)[last()]` |

---

## 7. เคล็ดลับการใช้งาน

- **ลำดับความสำคัญ `id` > `name` > `class` > `text()`** เพื่อให้ XPath ทนทานต่อการเปลี่ยน DOM
- หลีกเลี่ยงการซ้อน `//` หลายระดับ — ช้าและเปราะเมื่อ UI เปลี่ยน
- สำหรับข้อความ **หลายภาษา / มีเครื่องหมายเสริม** ควรใช้ `contains()` เพื่อลดความเสี่ยง
- ทดสอบ XPath เร็ว ๆ ใน **DevTools** ของ Chrome:
  - Console: `$x("//div[@id='main']")`
  - แท็บ Elements: `Ctrl+F` → วาง XPath ในช่องค้นหา
