# Command Injection Attack Documentation: From Low to High Security Levels

## Introduction

This document describes the procedure followed to conduct command injection attacks on DVWA, progressing through security levels from **Low** to **High**.

***

## Prerequisites

- DVWA installed and accessible locally or in a lab environment
- Command Injection module in DVWA available for testing
- Basic Linux command line knowledge
- Video reference: "Command-Injection.mp4" for real-time demonstration

***

## Setup

1. Access DVWA through `http://localhost/DVWA/login.php`
2. Log in with default user credentials (admin/password)
3. Navigate to the **Command Injection** vulnerability page
4. Adjust DVWA's security level to start from **Low** and progress upward to **High**

***

## Attack Execution Steps

### 1. Command Injection Attack at Low Security Level

- **Goal**: Exploit the vulnerability without any input sanitization or validation.

**Procedure**:

1. Set security level to **Low** in DVWA.
2. On the Command Injection page, input a simple payload such as:

```
127.0.0.1; ls -l
127.0.0.1; cd /etc/php
```

The semicolon (`;`) allows command chaining on Linux systems.
3. Submit the form; observe the output displaying a list of files indicating command execution.
4. Test additional commands like:

```
127.0.0.1; whoami
```

to confirm remote command execution.
5. Use various Linux commands to explore the system's response.

***

### 2. Command Injection Attack at Medium Security Level

- **Goal**: Bypass basic input filtering mechanisms.

**Procedure**:

1. Change DVWA security to **Medium**.
2. Retry known commands; observe if special characters like `;` or `&&` are filtered or blocked.
3. Use bypass techniques such as:
    - URL encoding special characters
    - Using alternative shell syntax:

```
127.0.0.1|ls
127.0.0.1`ls`
```

4. Observe the results to confirm if command execution is achievable despite restrictions.
5. Iterate testing with encoded payloads or obfuscated input to bypass sanitization.

***

### 3. Command Injection Attack at High Security Level

- **Goal**: Test advanced filtering that blocks common injection characters.

**Procedure**:

1. Set DVWA to **High** security.
2. Attempt commands that avoid classic delimiters (`;`, `|`, `&&`).
3. Experiment with:
    - Using backticks or command substitution mechanisms:

```
127.0.0.1 $(ls)
```

    - Chained commands using pipes or redirections.
4. Use encoding tricks like double URL encoding or Unicode representations.
5. Supplement testing with proxy tools (e.g., Burp Suite) to manipulate and fine-tune input payloads.
6. Confirm any successful command execution by output displayed on the webpage.

***

## Video Demonstration Summary ("Command-Injection.mp4")

- Duration: Approximately 32 minutes
- Demonstrates each stage of command injection directly on DVWA
- Shows low-level exploits working out-of-the-box with basic payloads
- Progresses through medium-level where input sanitization starts challenging attackers
- Features advanced evasion techniques used at high-security level for successful injection
- Visual confirmation of results after each input submitted
- Emphasizes the importance of understanding input filtering and escaping mechanisms

***

## Considerations and Recommendations

- Always perform command injection testing in a legal, controlled environment.
- Use automated tools and manual testing in parallel for comprehensive coverage.
- Learn how different security settings on DVWA simulate real-world defenses.
- Study the filtering rules to develop custom payloads for evasion.
- Protect live environments by implementing input validation, output encoding, and least privilege principles.

***

This approach provides a full walkthrough from initial exploitation on the lowest security setting to advanced bypass techniques on the highest, as visually demonstrated in the provided video.
<span style="display:none">[^1]</span>

<div style="text-align: center">⁂</div>

[^1]: Command-Injection.mp4

