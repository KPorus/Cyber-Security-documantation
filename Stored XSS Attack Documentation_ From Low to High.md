# Stored XSS Attack Documentation: From Low to High Security Levels

## Preparation Before the Attack

Before starting the Stored Cross-Site Scripting (XSS) attack on DVWA, it is essential to prepare the environment and configure settings properly:

1. **DVWA Setup**:
    - Ensure DVWA application is properly installed and accessible, typically at `http://localhost/DVWA/login.php`.
    - Log in using valid credentials (default: admin/password).
    - Set DVWA security level; begin testing with **Low**, then progress to **Medium** and **High** to observe different filtering mechanisms.
2. **Understand Target Page**:
    - Navigate to the **XSS (Stored)** section within DVWA.
    - Identify input fields where malicious payloads can be submitted (e.g., message/comment box).
    - Review how submitted inputs are displayed on the page and whether they are stored persistently.
3. **Browser and Tools Setup**:
    - Use a modern browser with developer tools active.
    - Optionally, configure a proxy like Burp Suite for request/response inspection and modification.
    - Familiarize yourself with how the application behaves with benign inputs.

***

## Attack Procedure
The video demonstrates injecting malicious scripts into stored XSS vulnerable fields, observing how they are executed for all users visiting the page.

### 1. Stored XSS Attack at Low Security Level

- **Goal**: Inject JavaScript code that is stored and executed without sanitization.

**Steps**:

1. Set DVWA Security to **Low**.
2. In the input box (e.g., message/comment), enter a script payload like:

```html
<script>alert('Test XSS Low')</script>
```

3. Submit the form.
4. Reload or navigate to the page where comments/messages are displayed.
5. Observe the alert box popping up, confirming the payload is stored and executed for all visitors.
6. Test with multiple payloads to confirm persistent execution.

***

### 2. Stored XSS Attack at Medium Security Level

- **Goal**: Bypass input filtering that blocks direct `<script>` tags but may allow event handlers or alternative tags.

**Steps**:

1. Switch DVWA security to **Medium**.
2. Submit payloads that avoid `<script>` tags but use event handlers, e.g.:

```html
<img src=x onerror=alert('XSS Medium')>
```

3. Submit and reload the page to verify execution.
4. Try alternative SVG or other HTML-based payloads known to bypass filters:

```html
<svg onload=alert('XSS Bypass')>
```

5. Use proxy or browser dev tools to encode or obfuscate payloads if needed.

***

### 3. Stored XSS Attack at High Security Level

- **Goal**: Overcome strong filtering and sanitization mechanisms.

**Steps**:

1. Set DVWA Security to **High**.
2. Attempt advanced XSS payloads that leverage less common event handlers or encoded payloads, for example:

```html
<body onload=alert('XSS High')>
<iframe src="javascript:alert('XSS')"></iframe>
```

3. Experiment with encoding such as URL or Unicode to evade filters.
4. Submit payloads and check if alerts pop up when the page is viewed.
5. Use Burp Suite to manipulate requests on the fly to test payload variations and evasions.
6. Confirm successful attacks by alert prompts or unexpected script behavior.

***

## Recommendations

- Test incrementally from low to high security levels to understand filtering improvements.
- Use proxy tools to fine-tune payload delivery and observe server responses.
- Implement strict input validation and output encoding to mitigate stored XSS in production.
- Always conduct testing in legal and isolated environments to avoid unintended impact.

***

This document provides a clear methodology for conducting Stored XSS attacks on DVWA.
<span style="display:none">[^1]</span>

<div style="text-align: center">⁂</div>

[^1]: [Xss-Store.mp4](https://drive.google.com/file/d/1FebZG9ifq7tJwEFDc-iyHn10O9x9--xJ/view?usp=sharing)

