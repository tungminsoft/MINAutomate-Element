# MinAutomate Helper — Knowledge Base

**[🇬🇧 English](README.md)** · **[🇻🇳 Tiếng Việt](README.vi.md)** · **🇹🇭 ไทย**

> สรุปความรู้เรื่อง **XPath** และ **CSS Selector** — สองภาษาค้นหา element ที่สำคัญที่สุดในงาน web automation, web scraping และ UI testing

## 📚 เนื้อหา

แต่ละหัวข้อมี **สามภาษา**: English (`en`), ภาษาเวียดนาม (`vi`), ภาษาไทย (`th`)

### XPath

| ภาษา | ไฟล์ |
|---|---|
| 🇬🇧 English | [xpath-summary.en.md](xpath-summary.en.md) |
| 🇻🇳 Tiếng Việt | [xpath-summary.vi.md](xpath-summary.vi.md) |
| 🇹🇭 ไทย | [xpath-summary.th.md](xpath-summary.th.md) |

### CSS Selector

| ภาษา | ไฟล์ |
|---|---|
| 🇬🇧 English | [css-selector-summary.en.md](css-selector-summary.en.md) |
| 🇻🇳 Tiếng Việt | [css-selector-summary.vi.md](css-selector-summary.vi.md) |
| 🇹🇭 ไทย | [css-selector-summary.th.md](css-selector-summary.th.md) |

## 🎯 ขอบเขต

แต่ละไฟล์ครอบคลุม:

- **ไวยากรณ์พื้นฐาน** — โครงสร้างทั่วไปของภาษาค้นหา
- **การจับคู่แอตทริบิวต์** — `=`, `contains`, `starts-with`, `ends-with`, …
- **การรวมเงื่อนไข** — AND / OR / NOT
- **ไม่สนใจตัวพิมพ์ใหญ่-เล็ก**
- **การปรับช่องว่างให้เป็นมาตรฐาน** — `normalize-space()` (เฉพาะ XPath)
- **การจับคู่ตามข้อความ** — `text()`, `contains(text())` (เฉพาะ XPath)
- **ความสัมพันธ์ระหว่าง node** — ลูก / ลูกหลาน / พ่อแม่ / บรรพบุรุษ / พี่น้อง
- **การเลือกตามตำแหน่ง** — index, `last()`, `nth-child`, `nth-of-type`
- **Pseudo-class & `:has()`** — เฉพาะ CSS
- **ตารางเทียบ Cheat Sheet** — XPath ↔ CSS
- **เคล็ดลับการใช้งาน** — ทดสอบใน Chrome DevTools, เลือกใช้อย่างไร

## 🔧 มาตรฐานการตั้งชื่อไฟล์

ใช้รูปแบบ **BCP 47 locale suffix** — มาตรฐานที่ framework i18n ส่วนใหญ่ใช้ (Docusaurus, Mintlify, i18next, Astro Content Collections):

```
{topic}-summary.{locale}.md
```

ตัวอย่าง: `xpath-summary.en.md`, `css-selector-summary.th.md`

## 📖 เมื่อไหร่ควรใช้ XPath vs CSS Selector?

| สถานการณ์ | แนะนำ |
|---|---|
| กรองตามข้อความใน element | **XPath** (CSS ไม่รองรับ) |
| ย้อนขึ้นไปยังพ่อแม่ / บรรพบุรุษ | **XPath** (CSS ไม่มี `parent::`, `ancestor::`) |
| หาพี่น้องที่อยู่ก่อนหน้า | **XPath** (CSS ไม่มี `preceding-sibling`) |
| เลือก element ที่มี X อยู่ข้างใน | ทั้งสอง — XPath `[./X]` หรือ CSS `:has(X)` (Level 4) |
| selector สั้น เร็ว | **CSS Selector** (เร็วกว่าใน browser) |
| รองรับ browser รุ่นเก่า | **CSS Selector** (XPath ไม่ได้อยู่ใน CSS engine) |

## 🤝 ร่วมพัฒนา

ยินดีรับ Pull request เมื่อปรับปรุงไฟล์ใด กรุณา **อัปเดตทั้งสามภาษา** (en / vi / th) เพื่อให้สอดคล้องกัน

## 📄 License

MIT
