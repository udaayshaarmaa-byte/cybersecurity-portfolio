# HTML Injection Notes (TryHackMe)

## What is HTML Injection?

HTML Injection is a type of injection attack where an attacker injects malicious HTML code into a web page.

Unlike XSS, it does NOT necessarily execute JavaScript — it manipulates the structure and content of the page.

---

## How It Happens

Occurs when:
- User input is not sanitized
- Input is directly rendered in HTML

Example vulnerable code:
```html
<p>Welcome, USER_INPUT</p>