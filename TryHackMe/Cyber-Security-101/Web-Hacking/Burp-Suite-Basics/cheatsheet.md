# Cheatsheet — Burp Suite

## Essentials

| Action / Item | How / Notes |
|---|---|
| Launch Burp | Start Burp Suite (Community). Choose default project settings for labs. |
| Editions | Community (manual), Professional (scanner, project save, Collaborator), Enterprise (continuous scanning). |
| Dashboard panels | Tasks (background tasks), Event log, Issue Activity (Pro), Advisory (Pro). |

## Proxy — core operations

| Action | Command / Steps |
|---|---|
| Set browser proxy | Use FoxyProxy → add proxy `127.0.0.1:8080` → activate (or use **Burp Browser**). |
| Intercept on/off | `Proxy → Intercept → Intercept is on / off`. |
| Forward / Drop | In **Proxy → Intercept**: **Forward** sends request, **Drop** cancels. |
| Send to Repeater | Right-click request → **Send to Repeater** (modify & resend). |
| Send to Intruder | Right-click → **Send to Intruder** (fuzzing / brute forcing). |
| HTTP history | `Proxy → HTTP history` — review logged requests/responses. |
| WebSocket history | `Proxy → WebSockets history` — view WS frames. |

## HTTPS interception

| Step | Short guide |
|---|---|
| Get CA | With proxy active visit `http://burp/cert` → download `cacert.der`. |
| Import CA (Firefox) | Settings → Privacy & Security → Certificates → View Certificates → Import → trust CA for websites. |
| Result | Browser trusts Burp CA → no TLS errors while proxying HTTPS. |

## Scoping & Targeting

| Task | Tip |
|---|---|
| Add to scope | `Target` → right-click host/path → **Add to scope**. |
| Enforce scope in proxy | `Proxy → Options → Intercept Client Requests` → enable **And URL is in target scope**. |
| Reduce noise | Choose “stop logging anything that is not in scope” when prompted. |

## Useful Proxy settings

| Feature | Use |
|---|---|
| Match & Replace | Auto-change headers/body on the fly (regex supported). |
| Intercept response rules | Configure when to intercept responses (by rules). |
| Request/response tampering | Modify then forward; useful for bypassing client-side filters. |

## Burp Browser & sandbox

| Item | Note |
|---|---|
| Built-in browser | `Proxy → Open Browser` (pre-configured to use proxy). |
| Sandbox issue (root) | Option: Settings → Tools → Allow Burp's browser to run without a sandbox (only in lab). |
| Best practice | Run Burp as non-root user or use Burp Browser only in controlled VMs. |

## Common workflow (one-liner steps)

1. Configure browser → enable proxy.  
2. Add target to scope.  
3. Intercept a request (or browse).  
4. Modify request (params/headers/body).  
5. Forward / Send to Repeater / Intruder.  
6. Inspect response; log findings & evidence.

## Handy shortcuts & navigation

| Shortcut | Opens |
|---|---|
| `Ctrl+Shift+D` | Dashboard |
| `Ctrl+Shift+T` | Target |
| `Ctrl+Shift+P` | Proxy |
| `Ctrl+Shift+I` | Intruder |
| `Ctrl+Shift+R` | Repeater |

## Detection & logging — what to watch

| What to watch | Where |
|---|---|
| Captured endpoints | `Target → Site map` |
| SMB / other non-HTTP calls from browser | `Proxy → HTTP history` (or OS network monitor) |
| Suspicious responses | `Proxy → Response` / `Repeater` → save response |

## Tabs quick-reference

| Tab | Purpose |
|---|---|
| Proxy | Intercept, view and edit all HTTP(S) traffic |
| Target | Site map, scope, and issue definitions |
| Repeater | Manual request replay & modification |
| Intruder | Automated attacks (fuzzing / brute force) |
| Decoder | Encode/decode base64 / URL / hex, analyze transforms |
| Comparer | Diff two responses |
| Extender | Add extensions (Pro/Community limited) |
