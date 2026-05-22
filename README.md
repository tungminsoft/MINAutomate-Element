# MinAutomate Helper — Knowledge Base

**🇬🇧 [English](en/README.md)** · **🇻🇳 [Tiếng Việt](vi/README.md)** · **🇹🇭 [ไทย](th/README.md)**

> A knowledge base for **XPath** and **CSS Selector** — the two most important element locator languages for web automation, web scraping, and UI testing.

## 📚 Contents

| Topic | 🇬🇧 English | 🇻🇳 Tiếng Việt | 🇹🇭 ไทย |
|---|---|---|---|
| **Landing / README** | [en/](en/README.md) | [vi/](vi/README.md) | [th/](th/README.md) |
| **XPath** | [en/xpath.md](en/xpath.md) | [vi/xpath.md](vi/xpath.md) | [th/xpath.md](th/xpath.md) |
| **CSS Selector** | [en/css-selector.md](en/css-selector.md) | [vi/css-selector.md](vi/css-selector.md) | [th/css-selector.md](th/css-selector.md) |

## 📁 Repository structure

```
.
├── README.md           ← you are here (language picker)
├── en/                 ← English
│   ├── README.md
│   ├── xpath.md
│   └── css-selector.md
├── vi/                 ← Tiếng Việt
│   ├── README.md
│   ├── xpath.md
│   └── css-selector.md
└── th/                 ← ไทย
    ├── README.md
    ├── xpath.md
    └── css-selector.md
```

## 📖 When to use XPath vs CSS Selector?

| Situation | Recommended |
|---|---|
| Filter by text content | **XPath** (CSS has no equivalent) |
| Traverse up to parent / ancestor | **XPath** (CSS lacks `parent::`, `ancestor::`) |
| Find preceding siblings | **XPath** (CSS lacks `preceding-sibling`) |
| Select element containing X | Either — XPath `[./X]` or CSS `:has(X)` (Level 4) |
| Short, performant selector | **CSS Selector** (faster in browsers) |
| Older browser compatibility | **CSS Selector** (XPath isn't part of CSS engines) |

## 🤝 Contributing

Pull requests welcome. When updating a file, please **sync all three translations** (en / vi / th) to keep them consistent.

## 📄 License

MIT
