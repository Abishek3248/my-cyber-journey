# Cheatsheet - How Websites Work

## HTML Basics  
| Element | Purpose | Example |
|---------|---------|---------|
| `<h1>` – `<h6>` | Headings (largest → smallest) | `<h1>Main Title</h1>` |
| `<p>` | Paragraph text | `<p>Hello World</p>` |
| `<img>` | Embed image | `<img src="cat.jpg">` |
| `<a>` | Hyperlink | `<a href="https://site.com">Click</a>` |
| `<!-- comment -->` | Hidden note in source code | `<!-- developer note -->` |


## JavaScript Basics  
| Concept | Purpose | Example |
|---------|---------|---------|
| Change element content | Modify HTML dynamically | `document.getElementById("demo").innerHTML = "Hi";` |
| Inline event | Trigger JS by action | `<button onclick="alert('Hello')">Click</button>` |
| Script tag | Run or import JS | `<script src="script.js"></script>` |


## Sensitive Data Exposure  
| Where to Check | What to Look For |
|----------------|------------------|
| Page Source (`Ctrl+U`) | Comments, hidden credentials, links |
| Frame Source | Extra embedded HTML with credentials |
| DevTools → Network tab | Cookies, headers, hidden parameters |


## HTML Injection  
| Concept | Example |
|---------|---------|
| Unsanitized input displayed directly | User’s HTML renders in page |
| Inject link | `<a href="http://hacker.com">Link</a>` |
| Impact | Control appearance, mislead users |
| Prevention | Sanitize/escape all user input |

