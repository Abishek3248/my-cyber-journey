# Burp Suite - Basics

## Introduction
- Burp Suite is a Java-based framework designed to serve as a comprehensive solution for conducting web application penetration testing. It has become the industry standard tool for hands-on security assessments of web and mobile applications, including those that rely on application programming interfaces (APIs).
- Burp Suite captures and enables manipulation of all the HTTP/HTTPS traffic between a browser and a web server. This fundamental capability forms the backbone of the framework. By intercepting requests, users have the flexibility to route them to various components within the Burp Suite framework, which we will explore in upcoming sections. The ability to intercept, view, and modify web requests before they reach the target server or even manipulate responses before they are received by our browser makes Burp Suite an invaluable tool for manual web application testing.
- Although Burp Suite Community offers a more limited feature set compared to the Professional edition, it still provides an impressive array of tools that are highly valuable for web application testing. Let's explore some of the key features:
  - **Proxy:** The Burp Proxy is the most renowned aspect of Burp Suite. It enables interception and modification of requests and responses while interacting with web applications.
  - **Repeater:** Another well-known feature. Repeater allows for capturing, modifying, and resending the same request multiple times. This functionality is particularly useful when crafting payloads through trial and error (e.g., in SQLi - Structured Query Language Injection) or testing the functionality of an endpoint for vulnerabilities.
  - **Intruder:** Despite rate limitations in Burp Suite Community, Intruder allows for spraying endpoints with requests. It is commonly utilized for brute-force attacks or fuzzing endpoints.
  - **Decoder:** Decoder offers a valuable service for data transformation. It can decode captured information or encode payloads before sending them to the target. While alternative services exist for this purpose, leveraging Decoder within Burp Suite can be highly efficient.
  - **Comparer:** As the name suggests, Comparer enables the comparison of two pieces of data at either the word or byte level. While not exclusive to Burp Suite, the ability to send potentially large data segments directly to a comparison tool with a single keyboard shortcut significantly accelerates the process.
Sequencer: Sequencer is typically employed when assessing the randomness of tokens, such as session cookie values or


## Dashboard

### Concepts Learned
- Burp Suite interface and main dashboard layout.
- Understanding the four dashboard quadrants: Tasks, Event Log, Issue Activity, Advisory.
- How to use help resources within Burp Suite.

### Explanation
- Upon launching Burp Suite Community Edition, you are prompted to select a project type and configuration. The default settings are suitable for most users. Once started, the main interface displays the Burp Dashboard, which is divided into four quadrants (counter-clockwise from top-left):
**Tasks:**
  - Manages background activities performed by Burp Suite.
  - In Community Edition, the default “Live Passive Crawl” logs pages visited.
  - Professional Edition includes additional scanning options.
**Event Log:**
  - Tracks actions performed by Burp Suite, such as starting the proxy and connection details.
**Issue Activity (Professional Edition only):**
  - Displays vulnerabilities detected by the automated scanner, sortable by severity and certainty.
**Advisory (Professional Edition only):**
  - Provides detailed information about identified vulnerabilities, including references and remediation suggestions.
**Help Icons:**
  - Found as question mark icons throughout the interface.
  - Clicking them opens helpful explanations specific to the current section, aiding navigation and understanding.

### Notes
- Community Edition lacks automated vulnerability findings in Issue Activity and Advisory sections.
- Default tasks in Community Edition are sufficient for learning and basic testing.
- Exploring tabs and quadrants helps familiarize yourself with Burp Suite’s capabilities.
- Help icons are a quick way to get context-specific guidance while navigating the tool.


## Navigation

### Concepts Learned
- How to navigate between Burp Suite modules and sub-tabs.
- Using detached tabs for multi-window workflows.
- Keyboard shortcuts for quick access to key tabs.

### Explanation
- Burp Suite navigation is primarily handled through menu bars:
**Module Selection:**
  - The top menu bar displays all available modules (Proxy, Target, Repeater, Intruder, etc.).
  - Clicking a module switches the main view to that module.
**Sub-Tabs:**
  - Modules with multiple sub-tabs display them in a second menu bar directly below the main menu.
  - Sub-tabs provide module-specific settings and options, e.g., Proxy → Intercept sub-tab.
**Detaching Tabs:**
  - Tabs can be opened in separate windows for multitasking.
  - Use Window → Detach to separate a tab and reattach it via the same menu.
**Keyboard Shortcuts:**
  - Ctrl + Shift + D → Dashboard
  - Ctrl + Shift + T → Target tab
  - Ctrl + Shift + P → Proxy tab
  - Ctrl + Shift + I → Intruder tab
  - Ctrl + Shift + R → Repeater tab
- These navigation options allow efficient movement between Burp modules and sub-tabs, improving workflow and productivity during testing.

### Notes
- Detaching tabs is helpful when monitoring multiple modules simultaneously.
- Keyboard shortcuts speed up workflow and reduce reliance on mouse clicks.
- Familiarity with module layouts and sub-tabs enhances efficiency in manual web application testing.


## Options

### Concepts Learned
- Understanding Global (User) settings vs Project settings.
- How to access and navigate Burp Suite settings.
- Using search, filters, and category menus for efficient configuration.
- Shortcuts for module-specific settings.

### Explanation
**Burp Suite provides two types of configuration settings:**
**Global (User) Settings**
  - Affect the entire Burp Suite installation.
  - Apply every time Burp Suite starts.
  - Provide a baseline configuration for all projects.
**Project Settings**
  - Specific to the current project/session.
  - Only applied during the session; Community Edition cannot save projects, so these settings are lost upon closing Burp.
**Accessing Settings:**
  - Click the Settings button in the top navigation bar.
**This opens a separate Settings window, which has:**
  - Search bar: Quickly locate settings using keywords.
  - Type filter: Filter between User (Global) and Project options.
  - User settings: Settings affecting the entire Burp Suite installation.
  - Project settings: Settings specific to the current project/session.
  - Categories: Allows viewing settings by functional category (e.g., Proxy, Repeater, Intruder).
**Module-specific shortcuts:**
  - Many modules have buttons to open their related settings directly.
  - Example: Proxy module → Proxy settings button opens the settings window directly to the Proxy configuration section.
  - Exploring the settings helps in understanding Burp Suite’s flexibility and prepares you to configure it for different testing scenarios.

### Notes
- Familiarize yourself with both User and Project settings to streamline workflow.
- Use the search feature to quickly find specific configurations.
- Module-specific settings shortcuts reduce navigation time.
- Community Edition limitations: Project settings are temporary and not saved between sessions.


## Burp Proxy

### Concepts Learned
- Role and purpose of the Burp Proxy in web application testing.
- How to intercept, manipulate, and forward HTTP/S requests.
- Logging and reviewing HTTP and WebSocket traffic.
- Key Proxy-specific options like response interception and match & replace.

### Explanation
- The Burp Proxy is a core component of Burp Suite, acting as a man-in-the-middle for HTTP and HTTPS traffic between the browser (or client) and the target web server. It allows testers to observe, modify, and analyze requests and responses.
**Key Functions of Burp Proxy:**
  - Intercepting Requests
  - Requests are held before reaching the server.
  - Actions available: Forward, Drop, Edit, or Send to other Burp tools.
  - Interception can be turned off via Intercept is on/off.
**Taking Control**
  - Full control over web traffic allows manual testing and manipulation of parameters, headers, cookies, etc.
**Capture and Logging**
  - All traffic is logged in HTTP history and WebSockets history.
  - Useful for reviewing past requests, analyzing application behavior, or sending requests to other Burp modules.
**WebSocket Support**
  - Captures and logs WebSocket communication for applications using persistent connections.
**Proxy-specific Options**
  - Accessed via the Proxy settings button.
**Key features include:**
  - Response Interception: Control when server responses are intercepted using rules.
  - Match and Replace: Use regex to dynamically modify requests and responses, e.g., changing user-agent strings or cookies.
  - Exploring Proxy settings improves efficiency, allows dynamic traffic manipulation, and enhances testing flexibility.

### Notes
- Use Intercept to pause requests for inspection and editing.
- HTTP and WebSocket history store logged traffic for later analysis.
- Match and Replace is powerful for automated modifications of traffic.
- Practice adjusting Proxy settings to understand their effect on captured traffic.


## Connecting through the Proxy (FoxyProxy)

### Concepts learned
- How to route browser traffic through Burp using the FoxyProxy extension.
- The proxy endpoint used by Burp (127.0.0.1:8080) and how to enable/disable it from the browser.
- What happens when Intercept is on (requests are held) and common actions you can take on intercepted requests.

### Explanation
**Install FoxyProxy**
  - Add the FoxyProxy Basic extension to your browser (already installed on AttackBox).
**Create a Burp profile**
  - Open FoxyProxy → Options → Add a new proxy entry.
**Fill in:**
  - Title: Burp (or any name)
  - Proxy IP: 127.0.0.1
  - Port: 8080
  - Save the configuration.
**Activate FoxyProxy profile**
  - Click the FoxyProxy icon and select the Burp profile to route traffic to Burp.
**Enable interception in Burp**
  - In Burp → Proxy tab → ensure Intercept is on.
  - With FoxyProxy active, your browser requests will be sent to Burp and held for inspection.
**Test it**
  - Navigate to a site (e.g., http://10.201.85.230/). The browser will hang while Burp shows the intercepted request.
  - In Burp you can Forward, Drop, Edit, or Send to Repeater/Intruder, etc.

### Notes / Practical tips
- Don’t forget to turn intercept off when you want the browser to behave normally (Intercept on = browser waits).
- Right‑click menu on a captured request gives quick actions: send to Repeater, Intruder, Logger, drop, copy, etc. Use these frequently.
- Close unrelated tabs before enabling interception — background tabs (websockets, analytics) can flood Burp with non-target requests.
- HTTPS interception: to view/modify HTTPS content, import Burp’s CA certificate into the browser (Proxy → Options → Import CA certificate). Without this you’ll see TLS errors.
- Burp must be running for the FoxyProxy profile to work; otherwise the browser will fail to load pages.
- Use FoxyProxy to toggle proxying quickly (useful when switching between normal browsing and testing).


## Site Map and Issue Definitions

## Concepts learned
- The Target tab contains three useful sub-tabs: Site map, Issue definitions, and Scope settings.
- Site map automatically records every page/endpoint the proxy sees and displays the application as a navigable tree.
- Issue definitions lists the vulnerability types Burp’s scanner looks for, with descriptions and references — useful even in Community edition for reporting and reference.
- Scope settings let you include/exclude domains/IPs so Burp focuses only on targets you intend to test.

## Explanation
**Site map**
  - As you browse (with the proxy on), Burp builds a hierarchical map of the application showing hosts, paths, parameters and file types.
  - The site map is helpful for discovery: it reveals API endpoints, hidden paths, and resources you may otherwise miss.
  - You can inspect individual entries to view request/response pairs, view parameters, or send items to other Burp tools (Repeater, Intruder, Scanner in Pro, etc.).
**Issue definitions**
  - Even without the automated scanner, Burp exposes the same vulnerability definitions (what the scanner checks for) along with descriptions and remediation guidance.
  - This is a handy reference when manually validating suspected issues or writing findings in a report.
**Scope settings**
  - Use scope to reduce noise and to avoid accidental testing outside of permission: add domains/IPs you intend to test and exclude everything else.
  - When scope is set, many Burp features (like automated tasks, spidering in Pro, and some extensions) will respect it and only act on in-scope targets.

## Notes / Practical tips
- Build the site map by browsing the app (or by running spiders/crawlers in Pro). Manually trigger all functionality (forms, APIs, JS-driven endpoints) to capture as much as possible.
- Inspect unusual entries in the site map: hidden directories, unexpectedly-named endpoints, or resources with odd file extensions often merit further investigation.
- Use the Response tab in a site-map entry to quickly preview the server response without reissuing requests. This is useful for spotting interesting content, comments, or tokens.
- Keep scope tight: add only authorised hosts to scope. This prevents accidental testing of third-party hosts (analytics, CDNs) that the site may contact.
- Reference Issue definitions when documenting findings — they give concise explanations you can adapt for reports and remediation guidance.
- Challenge hint: when mapping http://10.201.85.230/, browse every link on the homepage. Watch the site map for any endpoint that looks out of place — that’s the one to inspect first.


## The Burp Suite Browser

### Concepts learned
- Burp includes a built-in Chromium-based Burp Browser pre-configured to route traffic through Burp Proxy.
- The Burp Browser removes the need to configure external browsers or extensions (e.g., FoxyProxy) for proxying.
- Running Burp Browser as root (common on some VMs/AttackBox) can cause sandbox errors; there are two remedies: run Burp under a non‑privileged user or disable the sandbox (risky).
- Burp Browser settings are available under project/user options for further customization.

### Explanation
- The Burp Browser is a standalone Chromium instance launched from Burp (Proxy → Open Browser).
- All HTTP(S) requests from this browser automatically pass through Burp Proxy, so interception, logging, and manipulation work out of the box.
- Because the browser is controlled by Burp, it respects scope and other proxy settings, which helps keep testing focused and reproducible.
- On Linux running as root, the Chromium sandbox may refuse to start. You can:
- Create and use a low-privilege user to run Burp (preferred, safer).
- Or enable Allow Burp’s browser to run without a sandbox in Settings → Tools → Burp’s browser (convenient but reduces process isolation).
- Burp Browser options (project/user) let you tweak privacy, certificate handling, and other behaviors—useful when dealing with client-side protections or JS-heavy apps.

### Notes / Practical tips
- Use Burp Browser for testing when you want a clean, proxy-ready browser that won’t leak traffic outside Burp. It’s especially helpful for JS-heavy apps or when you want reproducible captures.
- Prefer non-root: run Burp under a standard user account on your machine when possible — it avoids sandbox issues and improves security.
- If you disable sandbox, be mindful: an exploited web page could more easily escape the browser and affect the host. Only disable the sandbox in trusted lab environments.
- Certificates: Burp will install its CA into the Burp Browser session automatically; if you use an external browser, you may need to install Burp’s CA manually to avoid TLS errors.
- Scope & privacy: Burp Browser respects scope — still double-check you aren’t interacting with third-party hosts unintentionally (analytics, CDNs).
- Reproducibility: Use Burp Browser when you need consistent captures for demos, training, or bug reports since it reduces variations caused by browser plugins/extensions.


## Scoping and Targeting

### Concepts learned
- Scoping limits what Burp records and acts on so you focus only on the target application.
- You can add items to scope from the Target → Site map (right-click → Add to scope).
- Scope is configurable (include/exclude rules by domain/IP/path) under Target → Scope settings.
- Even with logging disabled for out-of-scope hosts, the proxy may still intercept unless you enable the “URL is in target scope” check in Proxy settings.
- Proper scoping reduces noise, speeds up testing, and prevents accidental testing of unintended targets.

### Explanation
- Purpose: scoping ensures Burp captures, logs, and processes only the hosts/paths you intend to test — essential for efficiency and for staying within legal/safe testing boundaries.
- Adding to scope: browse or locate the host in Site map → right-click → Add to scope. Burp will ask whether to stop logging out-of-scope traffic — usually select Yes.
- Scope rules: Target → Scope lets you add include/exclude rules with patterns (hostnames, ports, path regex). Use include rules for targets and exclude for third-party resources you don’t want captured (CDNs, analytics).
- Proxy intercept filtering: go to Proxy → Options → Intercept Client Requests and enable And URL is in target scope. This prevents the proxy from halting or even logging requests outside the scope.
- Workflow: define scope first → enable proxy filters → browse/crawl the target → use site map & HTTP history focused only on in-scope items.

### Notes / Practical tips
- Always set scope before heavy testing (crawling, active tests) to avoid accidental requests to unrelated systems and to keep logs manageable.
- Exclude common third-party domains (analytics, CDNs, ad networks) to reduce noise and false positives.
- Use specific path rules for APIs or subdirectories (e.g., include example.com/api/*) to narrow focus.
- Confirm intercept behaviour after changing settings — a mistaken proxy filter can make it look like requests “fail” when they were simply ignored.
- Legal/safety reminder: scoping is not just convenience — it helps you stay within authorized targets. Always ensure you have permission to test anything in scope.


## Proxying HTTPS

### Concepts learned
- Burp acts as a TLS man-in-the-middle by presenting its own site certificates signed by the PortSwigger CA.
- Browsers will reject those certificates unless you explicitly trust the Burp (PortSwigger) CA.
- Installing/importing the CA cert (cacert.der) into the browser or OS trust store allows Burp to intercept HTTPS without browser errors.
- Alternatives: use Burp’s built-in browser (pre-configured) or temporarily allow the browser to run without a sandbox (not recommended for normal use).

### Explanation
- Why the error appears: when Burp intercepts TLS, it generates a site cert on the fly signed by PortSwigger’s CA. Your browser doesn’t trust that CA by default → certificate warnings.
- Obtain the CA cert: with the proxy active visit http://burp/cert → download cacert.der.
**Import into Firefox (example):**
  - Open about:preferences → search certificates → View Certificates → Import.
  - Select cacert.der and check Trust this CA to identify websites → OK.
  - Result: the browser now trusts certificates Burp generates, so TLS sites load normally while traffic is proxied and visible to Burp.
**Alternatives:**
- Use Burp’s bundled Chromium browser (already trusts the PortSwigger CA).
- For Chrome/Chromium you may need to import the cert into the OS/system certificate store or the browser-specific store depending on platform.
- If running Burp as root on Linux, you may need to enable “Allow Burp’s browser to run without a sandbox” or run Burp under a non-privileged user to use the embedded browser.

**Notes / Practical tips**
- Only install the PortSwigger CA on machines you control (test VMs, lab boxes). Do not add it to your personal/production machine unless you understand the risks.
- Remove the CA after testing if you won’t be using Burp regularly on that machine. Leaving a testing CA trusted increases attack surface.
- If import fails or you still see warnings: restart the browser, clear HSTS cached entries if needed, and confirm the proxy is running and set correctly (FoxyProxy/OS proxy settings).
- Some apps use certificate pinning — these will still detect/intercept and may refuse the connection even after trusting the CA.
- When troubleshooting: confirm you downloaded the cert from http://burp/cert while the Burp proxy was active (and not from an attacker page).
- Never trust untrusted CA files from unknown sources — only use PortSwigger’s CA generated by your local Burp instance.


## Example Attack — Reflected XSS (Support Form)

### Concepts learned
- Reflected Cross-Site Scripting (XSS) occurs when attacker-supplied input is immediately returned by the server and executed in the victim’s browser.
- Client-side filters (e.g., form validation) can be bypassed by intercepting and modifying requests.
- Burp Proxy lets you capture a form submission, edit the parameter to contain a payload, URL-encode it, and forward it to trigger reflected XSS.

### Explanation
- Reflected XSS: attacker injects a script into a request (e.g., form field). The server reflects that input in the response unescaped, so the victim’s browser executes it.
- Client-side validation only (e.g., email format checks in browser JS) is insufficient — it can be modified or bypassed before submission.
**Using Burp:**
  - Enable proxy and turn Intercept on.
  - Submit the form with “valid” values so the HTTP request is captured.
  - Edit the intercepted request: replace the email (or other parameter) with a JS payload (e.g. <script>alert("Succ3ssful XSS")</script>).
  - URL-encode the payload (Ctrl+U in Burp) so it’s safe to transmit.
  - Forward the request; if the server reflects it unsafely, the browser will render/execute the payload and show the alert.
  - Impact: executed scripts can steal cookies, perform actions as the user, or load malicious content — severity depends on context (authenticated user, sensitive data, etc.).

### Notes
- Payload used: <script>alert("Succ3ssful XSS")</script> (simple proof-of-concept).
- Bypass method: Intercept + edit request → URL-encode payload (Ctrl+U) → forward.
- Why URL-encode: prevents request parsing issues and avoids client-side blocking of disallowed characters.
- Where to inject: any reflected parameter that is reflected in page content (email, name, query, etc.).
- Testing tip: if alert doesn’t appear, check response body (in Proxy → Response) to see if payload is present but HTML-escaped (e.g., &lt;script&gt;) — then it’s not exploitable as-is.
- Detection: monitor logs for suspicious parameters containing <script> or encoded equivalents; web app scanners and manual review of reflected inputs help find vulnerable endpoints.
- Mitigation: server-side input sanitisation/encoding on output (HTML-encode user input before rendering), use CSP, and avoid reflecting raw user input into responses.
- Ethics: test only in authorized lab/engagements. Do not run payloads against production/unauthorised systems.


## Key Takeaways
- Burp Suite is a proxy-based web-app testing platform (Community, Professional, Enterprise). Community is fine for manual testing; Pro adds scanning, project saving, and advanced automation.
- The Proxy is the core: intercept requests/responses, edit them, forward/drop, and send to other modules (Repeater, Intruder, Decoder, Scanner).
- Always configure browser -> proxy (FoxyProxy or Burp Browser). For HTTPS interception import PortSwigger CA (http://burp/cert) into the browser trust store.
- Use scope settings to limit logging/interception to target apps — this reduces noise and prevents accidental testing outside allowed targets.
- The Target (Site map) automatically maps pages as you browse; use it to find endpoints and to control scope. Issue definitions are a handy reference even in Community edition.
- Workflow pattern: Browse → Intercept → Inspect/Edit → Forward/Send to Repeater/Intruder → Analyze response → iterate.
- Use Match & Replace, proxy rules, and settings to automate safe modifications (user-agent, cookies) during testing.
- Burp Browser is a convenient, preconfigured Chromium; if running as root, you can allow it to run without sandbox (only in trusted lab). Better: run Burp under a low-privilege user.
- Document every manual test: request details, edits made, payloads, response artifacts, and any captured evidence (PCAP, response bodies).
- Practice ethical rules: test only in authorized labs/targets, and import CA certs only on machines dedicated to testing.
