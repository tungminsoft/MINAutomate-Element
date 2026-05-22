# MinAutomate Helper — Knowledge Base

**🇬🇧 English** · **[🇻🇳 Tiếng Việt](../vi/README.md)** · **[🇹🇭 ไทย](../th/README.md)**

> A knowledge base for **XPath** and **CSS Selector** — the two most important element locator languages for web automation, web scraping, and UI testing.

## 📚 Contents

| Topic | File |
|---|---|
| XPath | [xpath.md](xpath.md) |
| CSS Selector | [css-selector.md](css-selector.md) |

## 🎯 Scope

Each summary covers:

- **Basic syntax** — overall structure of the query language
- **Attribute matching** — `=`, `contains`, `starts-with`, `ends-with`, …
- **Combining conditions** — AND / OR / NOT
- **Case-insensitive matching**
- **Whitespace normalization** — `normalize-space()` (XPath only)
- **Text matching** — `text()`, `contains(text())` (XPath only)
- **Node relationships** — child / descendant / parent / ancestor / sibling
- **Positional selection** — index, `last()`, `nth-child`, `nth-of-type`
- **Pseudo-classes & `:has()`** — CSS-specific
- **Cross-reference cheat sheet** — XPath ↔ CSS comparison table
- **Practical tips** — testing in Chrome DevTools, choosing between them

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
