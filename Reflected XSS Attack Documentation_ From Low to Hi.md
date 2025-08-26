# Reflected XSS Attack Documentation: From Low to High Security Levels

## Preparation Before the Attack

Before conducting the XSS attack on DVWA, the following setup and preparation steps should be followed:

1. **Environment Setup**:
    - Ensure DVWA is installed and accessible, typically at `http://localhost/DVWA/login.php`.
    - Login to DVWA with valid credentials (default: admin/password).
    - Verify the web server, database, and DVWA services are running properly.
2. **Configure Security Level**:
    - DVWA allows choosing security levels: Low, Medium, and High.
    - Begin with security level set to **Low** and progress gradually to higher levels for analysis.
3. **Browser Configuration**:
    - Use a modern web browser, preferably with developer tools enabled.
    - Optionally configure a proxy tool like Burp Suite to intercept and analyze requests and responses for deeper test control.
4. **Understand the Vulnerable Page**:
    - Navigate to the **XSS (Reflected)** section in DVWA.
    - Familiarize yourself with input fields where injection will be tested (e.g., Name input box).
    - Review response behavior by submitting benign inputs first.

***

## Attack Procedure

The video demonstrates injecting and exploiting reflected XSS vulnerabilities across security levels.

### 1. Attacking at the Low Security Level

- **Goal**: Inject and execute arbitrary JavaScript with no filtering.

**Steps**:

1. Ensure DVWA security is set to **Low**.
2. In the **Name** input field on the reflected XSS page, enter the following payload:

```html
<script>alert('Hello XSS Low')</script>
```

3. Submit the form.
4. Observe the pop-up alert box showing the message “Hello XSS Low,” confirming successful script execution.
5. This initial success shows that user input is reflected without sanitization or encoding.

***

### 2. Attacking at the Medium Security Level

- **Goal**: Bypass basic filtering that blocks direct script tags.

**Steps**:

1. Change the DVWA security level to **Medium**.
2. Enter an event-handler based payload that bypasses script tag filtering, for example:

```html
<img src=x onerror=alert('XSS Medium')>
```

3. Submit the payload.
4. Confirm that the alert box is displayed, indicating successful execution despite the blocking of `<script>` tags.
5. Experiment with SVG payloads known for filter evasion:

```html
<svg onload=alert('XSS Bypass')>
```

6. Adjust payloads incrementally, testing the effectiveness of different tags and event handler attributes.

***

### 3. Attacking at the High Security Level (Diorama)

- **Goal**: Find advanced payloads to bypass stricter input validation and filtering.

**Steps**:

1. Switch DVWA security to **High**.
2. Attempt more sophisticated payloads that avoid traditional script tags or use less common event attributes:

```html
<body onload=alert('XSS High')>
<iframe src="javascript:alert('XSS High')"></iframe>
```

3. Use encoding techniques such as URL encoding, Unicode characters, or alternate syntax to evade filters.
4. Submit payloads and observe the output for successful execution.
5. Leverage developer tools and proxy interceptors like Burp Suite to fine-tune inputs and identify bypasses.
6. Confirm popup alerts or other script behaviors to validate the injection.

***

## Summary

Key takeaways:

- **Low Level**: Direct script injections work flawlessly due to no protections.
- **Medium Level**: Blocking of `<script>` tags forces use of alternative HTML event handlers and tags.
- **High Level**: Requires sophisticated payloads, encoding, and evasion techniques to succeed.

***

## Important Notes

- Always conduct testing in a controlled, legal environment.
- Use proxy tools and browser consoles to enhance payload crafting and analysis.
- Understand filters in place to develop targeted bypass payloads.
- This attack flow helps in understanding how real-world web apps defend against reflected XSS and how attackers try to circumvent these defenses.

***

This documentation details the prerequisites, attack steps, and escalation approach observed in the referenced video, providing a clear methodology for conducting reflected XSS attacks on DVWA from basic to advanced security levels.
<span style="display:none">[^1]</span>

<div style="text-align: center">⁂</div>

[^1]: [Xss-Reflection.mp4](https://drive.google.com/file/d/1FebZG9ifq7tJwEFDc-iyHn10O9x9--xJ/view?usp=sharing)

