# CSS Selector — Knowledge Summary

## 1. General syntax

```
tag_name[condition]
```

- **`tag_name`**: HTML element name (`div`, `a`, `input`, …). Use `*` to match **any tag**.
- **`[condition]`**: filter by attribute / pseudo-class.
- Difference from XPath: CSS Selector **has no `//`** — by default it searches the whole document, and uses **space**, `>`, `+`, `~` to express relationships.

---

## 2. Tag name

| Syntax | Meaning |
|---|---|
| `div` | All `<div>` tags |
| `a` | All `<a>` tags |
| `*` | Any tag |

---

## 3. Basic selectors

| Syntax | Meaning | Example |
|---|---|---|
| `#id` | By `id` | `#username` |
| `.class` | By `class` | `.btn-primary` |
| `tag.class` | Tag + class | `button.btn-primary` |
| `tag#id` | Tag + id | `input#email` |
| `.c1.c2` | Has **both** classes `c1` and `c2` | `.btn.active` |

---

## 4. Attribute conditions

### 4.1. Attribute matchers

| Syntax | Meaning |
|---|---|
| `[attr]` | Has the attribute (any value) |
| `[attr="value"]` | **Exact** match |
| `[attr*="value"]` | **Contains** value (substring) |
| `[attr^="value"]` | **Starts with** value |
| `[attr$="value"]` | **Ends with** value |
| `[attr~="value"]` | Contains value as a **word** (whitespace separated) |
| `[attr\|="value"]` | Equals value, or starts with `value-` (for lang codes: `en-US`) |

**Examples:**
```css
input[required]
input[type="text"]
div[class*="btn"]
a[href^="https://"]
img[src$=".png"]
p[lang|="en"]
```

### 4.2. Case-insensitive matching

Add `i` before the closing `]`:

```css
a[title="login" i]
input[type="TEXT" i]
```

---

## 5. Pseudo-classes

### 5.1. Common state / position

| Syntax | Meaning |
|---|---|
| `:hover` | On mouse hover |
| `:focus` | When focused |
| `:checked` | Checkbox/radio is checked |
| `:disabled` / `:enabled` | Disabled / enabled |
| `:required` / `:optional` | Required / optional |
| `:empty` | No child nodes |
| `:not(...)` | Negation |

### 5.2. Position within parent (Index)

| Syntax | Meaning |
|---|---|
| `:first-child` | **First child** of parent |
| `:last-child` | **Last child** of parent |
| `:nth-child(n)` | `n`-th child (starts at 1) |
| `:nth-last-child(n)` | `n`-th child **counting from the end** |
| `:only-child` | Only child |
| `:first-of-type` | First element **of the same tag** in parent |
| `:last-of-type` | Last element **of the same tag** |
| `:nth-of-type(n)` | `n`-th element **of the same tag** |
| `:nth-last-of-type(n)` | Same, counting from the end |

**Expressions for `nth-child` / `nth-of-type`:**
- `2n` → even (2, 4, 6, …)
- `2n+1` or `odd` → odd elements
- `even` → even elements
- `3n+1` → 1, 4, 7, 10, …

**Examples:**
```css
li:first-child
li:last-child
li:nth-child(3)
li:nth-child(odd)
tr:nth-of-type(2n)
p:not(.hidden)
input:not([disabled])
```

### 5.3. Combining conditions

CSS has no explicit `and` / `or`, but:

| Goal | Syntax |
|---|---|
| **AND** (same element) | Chain directly: `input[type="text"][required]` |
| **OR** | Comma: `h1, h2, .title` |
| **NOT** | `:not(...)` |

**Examples:**
```css
input[type="text"][name="email"]      /* AND */
button#ok, button#submit               /* OR */
li:not(.active)                        /* NOT */
```

### 5.4. Match by text

> ⚠️ CSS Selector **has no** equivalent of XPath's `text()` / `contains(text())`. Use JavaScript or XPath if you must filter by text.

---

## 6. Combinators

| Syntax | Meaning | XPath equivalent |
|---|---|---|
| `A B` | `B` is a **descendant at any depth** of `A` | `//A//B` |
| `A > B` | `B` is a **direct child** of `A` | `//A/B` |
| `A + B` | `B` is the **immediate sibling after** `A` | `//A/following-sibling::B[1]` |
| `A ~ B` | `B` is **any sibling after** `A` (same parent) | `//A/following-sibling::B` |

**Examples:**
```css
form input              /* all <input> inside <form> */
ul > li                 /* <li> that is direct child of <ul> */
label + input           /* <input> right after <label> */
h2 ~ p                  /* all <p> after <h2> in same parent */
```

> ⚠️ CSS Selector **has no** combinator for **parent / ancestor / preceding sibling**. This is the major gap compared to XPath. (Level 4 adds `:has(...)` to express "element containing X" — see section 7.)

---

## 7. `:has()` — "contains" (Selectors Level 4)

`:has(...)` lets you select an element **containing** another element, equivalent to XPath's `//Xpath1[./Xpath2]`.

```css
div:has(> span.title)          /* <div> with a direct <span class="title"> child */
li:has(a[href^="https"])       /* <li> containing any https link */
tr:has(td.error)               /* <tr> with a <td class="error"> */
form:has(input:invalid)        /* <form> with any invalid input */
```

> ✅ Supported in modern browsers: Chrome/Edge ≥ 105, Safari ≥ 15.4, Firefox ≥ 121.

---

## 8. Pseudo-elements

| Syntax | Meaning |
|---|---|
| `::before` | Inject content **before** the element |
| `::after` | Inject content **after** the element |
| `::first-letter` | First letter |
| `::first-line` | First line |
| `::placeholder` | `<input>` placeholder text |
| `::selection` | Text selected by the user |

> Pseudo-elements use **double colon** `::`. Mostly for CSS styling, rarely used in automation.

---

## 9. Quick cheat sheet

| Goal | XPath | CSS Selector |
|---|---|---|
| By id | `//*[@id="x"]` | `#x` |
| By class | `//*[@class="x"]` | `.x` |
| By tag | `//div` | `div` |
| Any tag | `//*` | `*` |
| Exact attribute | `//a[@href="/"]` | `a[href="/"]` |
| Contains | `//a[contains(@class,"nav")]` | `a[class*="nav"]` |
| Starts with | `//a[starts-with(@id,"i-")]` | `a[id^="i-"]` |
| Ends with | `//img[ends-with(@src,".jpg")]` | `img[src$=".jpg"]` |
| AND | `[@a="1" and @b="2"]` | `[a="1"][b="2"]` |
| OR | `\|` (XPath 2.0) | `,` |
| NOT | `not(...)` | `:not(...)` |
| Case-insensitive | `translate(...)` | `[a="x" i]` |
| Direct child | `//A/B` | `A > B` |
| Any descendant | `//A//B` | `A B` |
| Immediate sibling after | `following-sibling::B[1]` | `A + B` |
| Any sibling after | `following-sibling::B` | `A ~ B` |
| Parent | `parent::A` | ❌ (not supported) |
| Ancestor | `ancestor::A` | ❌ (not supported) |
| Preceding sibling | `preceding-sibling::A` | ❌ (not supported) |
| By text | `[text()="X"]` | ❌ (not supported) |
| Contains child | `[./X]` | `:has(X)` (Level 4) |
| N-th element | `(//div)[N]` | `div:nth-of-type(N)` (per parent) |
| Last element | `(//tr)[last()]` | `tr:last-of-type` |

---

## 10. Tips

- **Prefer `id` > stable attribute > class** for resilient selectors.
- Avoid framework auto-generated classes (e.g. `css-1a2b3c` from styled-components, Tailwind JIT) — they change between builds.
- Quickly test CSS Selectors in **Chrome DevTools**:
  - Console: `document.querySelectorAll(".btn-primary")`
  - Elements tab: `Ctrl+F` → paste the selector into the search box.
- When you need to **filter by text** or **traverse to a parent/ancestor** → use XPath instead.
- When you need to **select an element containing X** → use `:has(...)` (CSS Level 4) or XPath `[./X]`.
- CSS Selectors are generally **faster than XPath** in the browser — prefer CSS when it is expressive enough.
