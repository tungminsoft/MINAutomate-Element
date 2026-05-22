# XPath — Knowledge Summary

## 1. General syntax

```
//tag_name[condition]
```

- **`//`**: searches anywhere in the DOM tree (not required to start from the root).
- **`tag_name`**: HTML/XML element name (`div`, `a`, `input`, …). Use `*` to match **any tag**.
- **`[condition]`**: predicate (filter) to pick the right element.

---

## 2. Tag name

| Syntax | Meaning |
|---|---|
| `//div` | All `<div>` tags |
| `//a` | All `<a>` tags |
| `//*` | Any tag |

---

## 3. Conditions (Predicate)

### 3.1. Match by attribute

| Syntax | Meaning |
|---|---|
| `[@attr="value"]` | Attribute **exactly equals** value |
| `[contains(@attr,"value")]` | Attribute **contains** value |
| `[starts-with(@attr,"value")]` | Attribute **starts with** value |
| `[ends-with(@attr,"value")]` | Attribute **ends with** value |

**Examples:**
```xpath
//input[@id="username"]
//div[contains(@class,"btn-primary")]
//a[starts-with(@href,"https://")]
//img[ends-with(@src,".png")]
```

### 3.2. Filter by nested XPath

```xpath
//Xpath1[./Xpath2]
```
→ Selects `Xpath1` that **contains** `Xpath2` inside.

**Example:**
```xpath
//div[./span[@class="title"]]
```
→ Selects `<div>` that has a `<span class="title">` inside.

### 3.3. Combining multiple conditions

| Operator | Meaning |
|---|---|
| `and` | Both conditions must be true |
| `or` | At least one condition true |
| `not(...)` | Negation |

**Examples:**
```xpath
//input[@type="text" and @name="email"]
//button[@id="ok" or @id="submit"]
//div[not(@class="hidden")]
```

### 3.4. Case-insensitive matching

```xpath
//tag_name[translate(@attr,
    'ABCDEFGHIJKLMNOPQRSTUVWXYZ',
    'abcdefghijklmnopqrstuvwxyz')="value"]
```

**Example:**
```xpath
//a[translate(@title,'ABCDEFGHIJKLMNOPQRSTUVWXYZ','abcdefghijklmnopqrstuvwxyz')="login"]
```

### 3.5. Normalize whitespace (`normalize-space`)

The `normalize-space()` function:
- Trims **leading and trailing** whitespace.
- Collapses consecutive whitespace (spaces, tabs, newlines) **into a single space**.

Very useful when text/attribute has extra whitespace due to HTML formatting.

**Syntax:**
```xpath
//tag_name[normalize-space(text())="value"]
//tag_name[normalize-space(@attr)="value"]
```

**Examples:**
```xpath
//button[normalize-space(text())="Sign in"]
//a[normalize-space()="Home"]                       // shorter, applies to current node's text
//div[contains(normalize-space(.),"Hello")]         // applies to entire merged text of node
```

> 💡 `normalize-space(.)` (the dot) reads **all text** of the element including text inside nested tags — handy when text is wrapped in nested `<span>` tags.

### 3.6. Match by text

Replace `@attr` with `text()` to match the element's text content.

**Examples:**
```xpath
//button[text()="Sign in"]
//span[contains(text(),"Hello")]
//h1[starts-with(text(),"Welcome")]
```

---

## 4. Multiple levels (Node relationships)

### 4.1. Child / descendant

| Syntax | Meaning |
|---|---|
| `//Xpath1/Xpath2` | `Xpath2` is a **direct child** of `Xpath1` |
| `//Xpath1//Xpath2` | `Xpath2` is a **descendant at any depth** of `Xpath1` |

### 4.2. Parent / ancestor

| Syntax | Meaning |
|---|---|
| `//Xpath1/parent::Xpath2` | Direct parent of `Xpath1` (must match `Xpath2`) |
| `//Xpath1/ancestor::Xpath2` | Any ancestor of `Xpath1` (matching `Xpath2`) |

### 4.3. Siblings / preceding-following

| Syntax | Meaning |
|---|---|
| `//Xpath1/preceding::Xpath2` | All nodes **before** `Xpath1` in the document |
| `//Xpath1/preceding-sibling::Xpath2` | Sibling **with the same parent**, before `Xpath1` |
| `//Xpath1/following::Xpath2` | All nodes **after** `Xpath1` in the document |
| `//Xpath1/following-sibling::Xpath2` | Sibling **with the same parent**, after `Xpath1` |

**Examples:**
```xpath
//label[text()="Email"]/following-sibling::input
//td[@class="name"]/parent::tr
//div[@id="content"]/ancestor::section
```

---

## 5. Selecting by position (Index)

```
(//tag_name[condition])[index]
```

- `index` starts from **1**.
- `last()` → the **last** element.
- Math is allowed: `last()-1` → second-to-last.

**Examples:**
```xpath
(//div[@class="item"])[1]          // first element
(//div[@class="item"])[3]          // third element
(//div[@class="item"])[last()]     // last element
(//div[@class="item"])[last()-1]   // second-to-last
```

> ⚠️ **Note**: `(//div)[1]` is different from `//div[1]`
> - `(//div)[1]`: the **first `<div>` in the whole document**.
> - `//div[1]`: each `<div>` that is the **first child within its own parent**.

---

## 6. Quick cheat sheet

| Goal | Example syntax |
|---|---|
| Exact attribute match | `//a[@href="/home"]` |
| Contains | `//a[contains(@class,"nav")]` |
| Starts with | `//a[starts-with(@id,"item-")]` |
| Ends with | `//img[ends-with(@src,".jpg")]` |
| By text | `//button[text()="OK"]` |
| Multiple conditions | `//input[@type="text" and @required]` |
| Negation | `//li[not(@class="active")]` |
| Case-insensitive | `//*[translate(@id,'ABC...','abc...')="login"]` |
| Direct child | `//ul/li` |
| Any descendant | `//form//input` |
| Parent | `//span/parent::div` |
| Ancestor | `//a/ancestor::section` |
| Following sibling | `//label/following-sibling::input` |
| Preceding sibling | `//input/preceding-sibling::label` |
| N-th element | `(//div[@class="row"])[2]` |
| Last element | `(//tr)[last()]` |

---

## 7. Tips

- **Prefer `id` > `name` > `class` > `text()`** for resilient XPaths when the DOM changes.
- Avoid deeply nested `//` — slow and fragile when UI updates.
- For **multilingual / accented text**, prefer `contains()` to reduce risk.
- Quickly test XPath in **Chrome DevTools**:
  - Console: `$x("//div[@id='main']")`
  - Elements tab: `Ctrl+F` → paste XPath into the search box.
