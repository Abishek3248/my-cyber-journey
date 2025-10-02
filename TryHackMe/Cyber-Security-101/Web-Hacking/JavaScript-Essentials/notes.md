# JavaScript Essentials

## Introduction
- JavaScript (JS) is a popular scripting language that allows web developers to add interactive features to websites containing HTML and CSS (styling). Once the HTML elements are created, you can add interactiveness like validation, onClick actions, animations, etc, through JS. Learning the language is equally important as that of HTML and CSS. The JS scripts are used primarily with HTML.


## JavaScript Essentials

### Concepts Learned
- Variables store data values and can be referenced later; declared using var, let, or const.
- Data types define the kind of value a variable can hold: string, number, boolean, null, undefined, object (arrays/objects).
- Functions are reusable blocks of code that perform specific tasks and can accept arguments.
- Loops (for, while, do...while) execute a block of code repeatedly while a condition is true.
- Request-response cycle: the client (browser) sends a request to the server, and the server responds with data or content.

### Explanation
**Variables act as labeled containers for data:**
  - let and const are block-scoped; var is function-scoped.
  - Data types ensure proper handling and manipulation of values.
**Functions reduce code repetition:**
  - Example: PrintResult(rollNum) prints results for multiple students.
**Loops automate repetitive tasks:**
  - for loop iterates a known number of times.
  - while loop runs while a condition is true.
  - do...while ensures at least one execution before checking the condition.
**Request-response cycle:**
  - Client (browser) sends HTTP requests to the server.
  - Server responds with content (HTML, JSON, images, etc.).
  - JavaScript uses this cycle to fetch or send data dynamically.

### Notes
- Prefer let for mutable variables and const for constants; avoid var due to function-scoping issues.
- Use typeof to check variable types; arrays and objects are both of type object.
- Functions can be declared traditionally (function) or as arrow functions (() => {}).
- Loops simplify repetitive tasks efficiently.
- Asynchronous requests (AJAX, Fetch API) allow dynamic data fetching without reloading the page.


## JavaScript Overview

### Concepts Learned
- JavaScript (JS) is an interpreted language executed directly in the browser.
- JS enables dynamic, interactive web applications by manipulating HTML and handling events.
- Basic program structure includes variables, data types, control flow statements, and functions.
- The Chrome Console allows testing and running JS code without external tools.
- Expressions and operations can be executed directly, and results can be printed with console.log().

### Explanation
- JS is executed on the client side, making it easy to interact with web pages.
- Variables store values; let is used for mutable data.
- Data types include numbers, strings, and booleans.
- Control flow statements (if-else) help in decision-making based on conditions.
- Functions group reusable code blocks and can take parameters to perform tasks.
- Expressions evaluate to a value; in the example x + y, the result is 15.
- console.log() prints output to the browser console for testing and debugging.
- The Chrome Console can be accessed via Ctrl + Shift + I or right-click → Inspect → Console tab.
- Users can paste code directly into the console and see immediate results.

### Notes
- Start JS experimentation in the browser console before writing scripts in files.
- Always declare variables with let or const to avoid accidental global scope.
- Test small code snippets using console.log() to verify logic.
**Example program:**
  - let x = 5;
    let y = 10;
    let result = x + y;
    console.log("The result is: " + result); // Output: The result is: 15
- This code demonstrates variable declaration, arithmetic operations, and console output.
- Practicing in the console helps in understanding real-time execution and debugging.


## Integrating JavaScript in HTML

### Concepts Learned
- JavaScript can be integrated into HTML in two ways: internal and external.
- Internal JS is embedded directly in the HTML file using <script> tags.
- External JS is written in a separate .js file and linked using the src attribute in <script> tags.
- Internal JS executes when the HTML page loads, while external JS allows better organisation and maintainability.
- Inspecting a website’s source code helps identify if it uses internal or external JS.

### Explanation
**Internal JavaScript:**
  - JS code is placed directly inside <script> tags in the HTML <head> or <body>.
  - Ideal for small scripts or beginner experimentation.
**Example: adding two numbers and displaying result:**
  - "let x = 5;
    let y = 10;
    let result = x + y;
    document.getElementById("result").innerHTML = "The result is: " + result;"
- This updates the content of an HTML element using document.getElementById().innerHTML.
**External JavaScript:**
- JS code is stored in a separate .js file.
- Linked in HTML with <script src="script.js"></script>.
- Keeps HTML clean and improves maintainability.
- Browser loads and executes the JS when the page renders.
**Practical verification:**
- Right-click → View Page Source in Chrome.
- <script> tags without src indicate internal JS.
- <script src="..."> indicates external JS.
- Inspect live websites (e.g., TryHackMe) to observe real-world use.

## Notes
- Internal JS is simpler but can clutter HTML files if overused.
- External JS is preferred for larger projects for clarity and reusability.
- Both internal and external JS achieve the same functionality; the difference lies in organisation.
**Example HTML for internal JS:**
  - <p id="result"></p>
    <script>
    let x = 5, y = 10;
    document.getElementById("result").innerHTML = "The result is: " + (x + y);
    </script>
**Example HTML for external JS:**
  - <p id="result"></p>
    <script src="script.js"></script>
- Always test JS code by opening the HTML file in a browser (e.g., Chrome).
- Understanding internal vs external JS is important for web development and penetration testing.


## Abusing Dialogue Functions

### Concepts Learned
- alert, prompt, and confirm are built‑in JS dialogue functions used to interact with users.
- These functions can be abused to disrupt user experience or as part of client‑side attacks (e.g., XSS payloads or social‑engineering).
- Running untrusted JavaScript (e.g., from email attachments or unknown pages) can trigger these dialogues and cause nuisance or trick users into revealing data.
- Testing these functions is easy via the browser console (Chrome DevTools).

### Explanation
- alert(message) — shows a modal dialog with message and an OK button; used for notifications.
- prompt(message) — shows a dialog requesting input; returns the entered string (or null on cancel).
- confirm(message) — shows a dialog with OK and Cancel; returns true for OK, false for Cancel.
**Attack scenarios:**
  - Repeated alert() calls (loop) can flood the user with dialogs, causing denial of use or annoyance.
  - prompt() can be misused for phishing (ask for credentials) inside a seemingly legitimate page.
  - confirm() can be used to trick users into approving actions.
  - Practical testing: open Chrome → Inspect → Console and run alert("Hello THM"), prompt("What is your name?"), or confirm("Proceed?").
  - Malicious example: an emailed/attached HTML file containing
     - <script>
          for (let i = 0; i < 500; i++) { alert("Hacked"); }
       </script>
- will force the recipient to dismiss many dialogs or hang the browsing session.
### Notes
- Hands‑on: used Chrome console and local HTML files (e.g., invoice.html) to demonstrate and observe behaviors.
- Defenses / best practice: never run JS from untrusted sources; disable auto‑loading of external content where possible; use Content Security Policy (CSP) to restrict scripts; educate users to avoid entering secrets into unexpected prompts.
- As an analyst, expect to see dialogue functions used in trivial nuisance attacks and as components within larger XSS/social‑engineering payloads — treat them as indicators, not full exploits.


## Bypassing Control Flow Statements

### Concepts Learned
- JS control flow (if/else, switch, loops) determines what the page does based on conditions.
- Client‑side checks are easily bypassable — anything done only in the browser can be modified.
- Real security requires server‑side validation; client checks are for UX only.

### Explanation
- if/else and loops control logic; e.g., an age check if (age >= 18) { … } else { … }.
- prompt() returns a string — JS type coercion can affect comparisons ("18" >= 18 is true).
**Common bypass techniques (all performed from the client/browser):**
  - Edit values in the Console — set variables directly (age = 999;) before the check runs or after by re-running the check.
  - Modify DOM / remove checks — delete <script> or change event handlers in Elements panel so the check never executes.
  - Patch the script on the fly — open Sources, edit JS (or paste a modified function) and re-run logic.
  - Override functions — redefine a validation function in Console to always return true.
  - Use breakpoints / debugger — pause execution, change variables, then resume to force alternate branch.
  - Tamper with requests — intercept and modify outgoing requests (e.g., via DevTools Network tab or a proxy) to send forged data to the server.
  - Bypass login pages that do client‑side checks by creating a request that mimics a successful login (if server accepts it).
  - Defensive reminder: any authentication, authorization, or sensitive decision must be enforced server‑side because attackers control the client.

### Notes
**Hands‑on: created and tested age.html (age prompt) and the shipped login.html. Observed behavior and verified bypasses by:**
  - entering different prompt values,
  - setting age in the console,
  - editing the page script in DevTools to force the success branch.
  - Practical takeaway: treat client‑side checks as convenience only — always validate on the backend and use secure session tokens for auth.
  - For testing: use DevTools (Console, Elements, Sources, Network) or an intercepting proxy (Burp/OWASP ZAP) to manipulate and observe control flow changes.


## Exploring Minified & Obfuscated JavaScript

## Concepts Learned
- Minification removes whitespace, comments and shortens identifiers to reduce file size.
- Obfuscation transforms code (rename symbols, insert noise, control-flow tricks) to make it hard to read while remaining functional.
- Browsers execute minified/obfuscated JS normally — readability is the only thing lost.
- Deobfuscation/reformatting can recover human‑readable code for analysis.
- DevTools (Sources), online prettifiers/deobfuscators, and static analysis are essential when inspecting minified or obfuscated scripts.

### Explanation
**Minification vs Obfuscation**
  - Minification → size/latency optimization (strip spaces, shorten names).
  - Obfuscation → deliberate hardness for reverse‑engineering protection (encoded strings, computed indexes, opaque operations).
**How browsers run it**
  - Minified/obfuscated code is valid JS and runs the same as original code; only human readability changes.
**Common obfuscation features**
  - Encoded string arrays, index lookups (e.g. _0x33bf(0x88)), self‑invoking loops that rearrange arrays, meaningless identifiers.
**Tools & techniques to analyse**
  - Open DevTools → Sources to view loaded JS (even if minified/obfuscated).
  - Use a prettifier (format/pretty print) to add indentation and line breaks.
  - Use deobfuscators / online reversal tools to rename symbols and resolve computed strings.
  - Manually inspect key functions (string tables, index translation) to reconstruct intent.
**Workflow for investigation**
  - Load page / open the JS file in DevTools.
  - Pretty‑print to make structure visible.
  - Identify and expand string tables or index functions.
  - Use automated deobfuscators if available, then manually verify.
  - Run in a safe environment (local file or lab) to observe behavior.

**Notes (hands‑on)**
- Created hello.html + hello.js with simple hi() → alert("Welcome to THM") and verified behavior in Chrome.
- Replaced hello.js content with an obfuscated/minified variant from an online obfuscator; page still executed the alert.
- Used DevTools Sources to view obfuscated code and applied Pretty Print to improve structure.
- Used an online deobfuscator to reconstruct readable code and confirmed it matched original logic.
- Practical takeaway: even heavily obfuscated code can be analyzed using a combination of DevTools, prettifiers, and deobfuscators — always perform analysis in a controlled environment.


## Best Practices

### Concepts Learned
- Client-side JavaScript is convenient but never a substitute for server-side validation.
- Including third-party libraries carries risk — only use trusted, version-pinned sources.
- Secrets (API keys, tokens, credentials) must never be hardcoded into front-end code.
- Minification and obfuscation improve performance and raise the bar for casual inspection, but they are not a security guarantee.

### Explanation
**Server-side validation is mandatory**
  - Perform all security-relevant checks on the server (authentication, authorization, input validation, business rules).
  - Treat any client input as untrusted — users can tamper with or disable JS in their browser.
**Manage third-party scripts carefully**
  - Prefer vetted packages from official registries; pin exact versions to avoid supply-chain surprises.
  - Host critical libraries locally or via a proven CDN with Subresource Integrity (SRI) where possible.
  - Regularly scan dependencies for vulnerabilities and apply updates.
**Never embed secrets in front-end code**
  - Use the backend to store and use sensitive values. Expose only short-lived tokens or proxy requests through server endpoints when necessary.
  - Rotate keys regularly and apply least privilege to API credentials.
**Use minification and obfuscation appropriately**
  - Minify for performance (smaller payloads, faster load).
  - Obfuscate to deter casual inspection, but assume a determined attacker can reverse it — don’t rely on it for security.
**Extra hardening**
  - Apply Content Security Policy (CSP) to restrict where scripts/styles can be loaded from and to mitigate XSS.
  - Use secure cookie flags (HttpOnly, Secure, SameSite) to protect session tokens.
  - Disable or restrict features you don’t need (TRACE, permissive CORS, unnecessary third-party embeds).
**Development & deployment hygiene**
  - Keep separate configs for development and production; never leak dev/test credentials.
  - Automate dependency scanning, SAST/linters, and production builds (minify/strip debug).
  - Log and monitor unusual client behaviour; alert on suspicious patterns.

### Notes
**Quick checklist to follow:**
  - Validate on server; client checks only for UX.
  - Audit and pin third-party libs; use SRI or local hosting where feasible.
  - Move secrets to backend; use short-lived tokens for client needs.
  - Minify for performance; obfuscate only as a minor deterrent.
  - Enforce CSP, secure cookies, and strict CORS.
  - Automate scans and keep an inventory of front-end dependencies.
- Practical lab note: when testing or demonstrating JS behavior, run everything in isolated/dev environments — never expose real credentials or production endpoints.


## Key Takeaways
- JS runs in the browser (client-side) — easy to inspect and modify; never assume client code is private or trustworthy.
- Variables & types matter — use let/const for block scope, understand primitives vs objects, and avoid leaking state unintentionally.
- Functions are reusable logic — encapsulate behaviour, avoid duplicating logic, and keep side effects clear.
- Control flow is not security — if/else, loops, and client-side checks are for UX; enforce validation and authorisation on the server.
- Request–response fundamentals are critical — understand how requests, headers, bodies, and responses flow to avoid logic and data exposure mistakes.
- Integrate JS properly — prefer external scripts for maintainability; inspect source to discover inline vs external code during testing.
- Dialog APIs are interactive, not secure — alert, prompt, confirm can be abused (annoyance or XSS vectors); don’t rely on them for auth or gating.
- Minification/obfuscation ≠ security — they improve performance and raise the bar slightly for attackers but do not prevent inspection or reverse engineering.
- Third-party scripts are a supply-chain risk — only load trusted libraries, pin versions, and audit dependencies.
- Avoid hardcoding secrets — never store API keys, tokens, or credentials in client-side JS.
- Sanitise all user input — prevent XSS, injection, and path manipulation by validating and escaping on the server and using CSP on the client.
- Use best practices — combine server-side validation, secure cookie flags, CSP, dependency management, and minimal client privileges for defence-in-depth.
- Testing & inspection tools matter — use browser DevTools (Console, Sources) to debug, review, and audit JavaScript behaviour during pentesting or development.
