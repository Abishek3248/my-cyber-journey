# Summary – Burp Suite Basics

**This room introduced Burp Suite (Community Edition) as a manual web‑application testing toolkit and covered how to configure and use its core features to intercept, inspect, modify, and replay HTTP(S) traffic.**

- Learned what Burp Suite is, the differences between Community / Professional / Enterprise editions, and when to use each.
- Understood the Dashboard and main navigation: modules and sub‑tabs (Proxy, Target, Repeater, Intruder, Decoder, Comparer, Extender).
- Configured Burp Proxy and browser integration (FoxyProxy or the built‑in Burp Browser) to route traffic through 127.0.0.1:8080.
- Installed and trusted the PortSwigger CA in the browser to proxy HTTPS traffic without certificate errors.
- Used the Proxy to intercept requests/responses, edit and forward or drop them, and send items to Repeater/Intruder/Decoder for deeper testing.
- Mapped applications with the Target → Site map and learned how Issue Definitions help identify common findings (useful reference even in Community Edition).
- Scoped targets to limit noise and control which URLs Burp logs and intercepts; enforced scope in proxy settings for cleaner workflows.
- Explored useful Proxy settings: Match & Replace, response interception rules, WebSocket capture, and logging options.
- Practiced manual testing workflows: intercept → modify → forward, send to Repeater for fine‑tuning, and use Intruder for automated payloads.
- Performed a basic example attack (bypassing client‑side filtering to trigger reflected XSS) and observed how interception + encoding enables manual exploit attempts.
- Learned operational best practices: always define scope, document requests/responses, import CA only on trusted test machines, and run Burp under non‑root where possible (or enable sandbox bypass only in lab).
- Practical skills gained: setting up Burp proxy, importing the CA cert, scoping targets, intercepting and modifying traffic, sending requests to Repeater/Intruder, mapping sites, and performing simple manual vulnerability verification.
- Overall takeaway: Burp Suite is an essential manual testing tool—mastering proxy setup, scoping, interception, and the Repeater/Intruder workflow provides a strong foundation for effective and responsible web application security testing.
