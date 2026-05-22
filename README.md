# MinAutomate Helper — Knowledge Base

**🇬🇧 English** · **[🇻🇳 Tiếng Việt](README.vi.md)** · **[🇹🇭 ไทย](README.th.md)**

> A knowledge base for **XPath** and **CSS Selector** — the two most important element locator languages for web automation, web scraping, and UI testing.

## 📚 Contents

Each topic ships in **three languages**: English (`en`), Vietnamese (`vi`), Thai (`th`).

### XPath

| Language | File |
|---|---|
| 🇬🇧 English | [xpath-summary.en.md](xpath-summary.en.md) |
| 🇻🇳 Tiếng Việt | [xpath-summary.vi.md](xpath-summary.vi.md) |
| 🇹🇭 ไทย | [xpath-summary.th.md](xpath-summary.th.md) |

### CSS Selector

| Language | File |
|---|---|
| 🇬🇧 English | [css-selector-summary.en.md](css-selector-summary.en.md) |
| 🇻🇳 Tiếng Việt | [css-selector-summary.vi.md](css-selector-summary.vi.md) |
| 🇹🇭 ไทย | [css-selector-summary.th.md](css-selector-summary.th.md) |

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

## 🔧 File naming convention

Follows **BCP 47 locale suffix** — the standard used by major i18n frameworks (Docusaurus, Mintlify, i18next, Astro Content Collections):

```
{topic}-summary.{locale}.md
```

Examples: `xpath-summary.en.md`, `css-selector-summary.vi.md`.

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
