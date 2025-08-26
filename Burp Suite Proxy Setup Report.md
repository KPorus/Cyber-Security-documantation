<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Burp Suite Proxy Setup Report

## Overview

This report documents the configuration process for setting up Burp Suite proxy integration with Firefox browser, enabling comprehensive web application security testing through traffic interception and analysis.

## Prerequisites

- Burp Suite Professional or Community Edition installed
- Firefox web browser
- Administrative access to modify browser security settings


## Setup Process

### 1. Burp Suite Proxy Configuration

**Objective**: Configure Burp Suite to listen for incoming proxy connections

**Steps**:

1. Launch Burp Suite application
2. Navigate to the **Proxy** tab in the main interface
3. Access **Options** sub-tab under Proxy settings
4. Configure proxy listener:
    - **Interface**: `127.0.0.1:8080`
    - **Protocol**: HTTP/HTTPS
    - Ensure the listener is set to "Running" status

### 2. Firefox Browser Proxy Configuration

**Objective**: Direct browser traffic through Burp Suite proxy

**Steps**:

1. Open Firefox browser
2. Access network settings:
    - Navigate to **Settings** → **General** → **Network Settings**
    - Click **Settings** button in the "Network Proxy" section
3. Configure manual proxy settings:
    - Select **Manual proxy configuration**
    - **HTTP Proxy**: `127.0.0.1` Port: `8080`
    - **HTTPS Proxy**: `127.0.0.1` Port: `8080`
    - Ensure "Use this proxy server for all protocols" is checked

### 3. SSL Certificate Installation

**Objective**: Install Burp Suite's CA certificate to handle HTTPS traffic

**Steps**:

1. **Download CA Certificate**:
    - Open new Firefox tab
    - Navigate to: `https://burp`
    - Download the CA certificate file from the Burp Suite certificate page
2. **Install Certificate in Firefox**:
    - Access Firefox **Settings**
    - Search for "certificate" in the settings search bar
    - Click **View Certificates** button
    - In the Certificate Manager popup window:
        - Select the **Authorities** tab
        - Click **Import** button
        - Browse and select the downloaded Burp CA certificate file
        - **Certificate Trust Settings**: Check all available options:
            - "Trust this CA to identify websites"
            - "Trust this CA to identify email users"
            - "Trust this CA to identify software developers"
        - Click **OK** to complete installation

### 4. Firefox Advanced Configuration

**Objective**: Enable localhost proxy connections for comprehensive testing

**Steps**:

1. Access Firefox advanced configuration:
    - Type `about:config` in the address bar and press Enter
    - Accept the warning message about advanced settings
2. Configure localhost proxy setting:
    - Use the search bar to locate: `network.proxy.allow_hijacking_localhost`
    - Double-click the preference name or click the toggle button
    - Change the value from `false` to `true`
    - This enables proxy interception of localhost traffic

## Verification and Testing

### 1. Connection Verification

- Navigate to any HTTPS website in Firefox
- Verify that requests appear in Burp Suite's **HTTP history** tab
- Confirm that HTTPS traffic is successfully decrypted and displayed


### 2. Localhost Testing

- Access local applications (e.g., `http://localhost/DVWA`)
- Verify that localhost traffic is captured in Burp Suite
- Test both HTTP and HTTPS local connections


## Configuration Summary

| Component | Setting | Value |
| :-- | :-- | :-- |
| Burp Suite Proxy | Interface | 127.0.0.1:8080 |
| Firefox HTTP Proxy | Address:Port | 127.0.0.1:8080 |
| Firefox HTTPS Proxy | Address:Port | 127.0.0.1:8080 |
| CA Certificate | Trust Level | Full (all options) |
| Localhost Hijacking | Status | Enabled (true) |

## Security Considerations

### Best Practices

- Use this configuration only in isolated testing environments
- Disable proxy settings when not performing security testing
- Regularly update Burp Suite to maintain current security features
- Store CA certificates securely and remove when testing is complete


### Important Notes

- The CA certificate installation allows Burp Suite to decrypt HTTPS traffic
- Localhost hijacking enables testing of local web applications
- All web traffic will be visible in Burp Suite when proxy is active
- Consider creating separate Firefox profiles for security testing vs. regular browsing


## Troubleshooting

### Common Issues

- **Connection refused**: Verify Burp Suite proxy listener is running
- **Certificate errors**: Ensure CA certificate is properly installed in Authorities tab
- **Localhost not intercepted**: Confirm `network.proxy.allow_hijacking_localhost` is set to true
- **Performance issues**: Consider adjusting Burp Suite memory allocation for large applications

This configuration establishes a comprehensive web application security testing environment, enabling detailed analysis of HTTP/HTTPS traffic for vulnerability assessment and penetration testing activities.

