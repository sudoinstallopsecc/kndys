# KNDYS Framework

KNDYS is a modular penetration testing framework written in Python 3. It provides 51 modules organized across 10 categories, covering the full scope of a security assessment: reconnaissance, scanning, exploitation, post-exploitation, password attacks, wireless analysis, social engineering, network attacks, web application testing, and reporting.

---

## Table of Contents

1. [Requirements](#requirements)
2. [Installation](#installation)
3. [Getting Started](#getting-started)
4. [Interface Overview](#interface-overview)
5. [Module Categories](#module-categories)
6. [Reconnaissance Modules](#1-reconnaissance-recon)
7. [Scanning Modules](#2-scanning-scan)
8. [Exploitation Modules](#3-exploitation-exploit)
9. [Post-Exploitation Modules](#4-post-exploitation-post)
10. [Password Attack Modules](#5-password-attacks-password)
11. [Wireless Modules](#6-wireless-wireless)
12. [Social Engineering Modules](#7-social-engineering-social)
13. [Network Attack Modules](#8-network-attacks-network)
14. [Web Application Modules](#9-web-application-testing-webapp)
15. [Reporting Modules](#10-reporting-report)
16. [Wordlists and Payloads](#wordlists-and-payloads)
17. [Global Configuration](#global-configuration)
18. [Legal Disclaimer](#legal-disclaimer)

---

## Requirements

- **Operating System:** Linux (Debian/Ubuntu, Fedora, Arch, Kali, or any distribution with Python 3)
- **Python:** 3.8 or higher
- **Privileges:** Root access is required for certain modules (wireless, network attacks, packet sniffing)
- **Network:** Internet connection required for dependency installation and wordlist downloads

### Python Dependencies

The following packages are installed automatically on first run. If automatic installation fails, install them manually:

| Package | Minimum Version |
|---------|----------------|
| requests | 2.31.0 |
| colorama | 0.4.6 |
| beautifulsoup4 | 4.12.0 |
| lxml | 4.9.0 |
| urllib3 | 2.0.0 |
| cryptography | 41.0.0 |
| pycryptodome | 3.19.0 |
| PyJWT | 2.8.0 |
| scapy | 2.5.0 |
| python-nmap | 0.7.1 |
| paramiko | 3.3.0 |
| dnspython | 2.4.0 |
| netifaces | 0.11.0 |
| selenium | 4.15.0 |
| webdriver-manager | 4.0.0 |
| qrcode | 7.4.0 |
| Pillow | 10.1.0 |
| twilio | 8.10.0 |
| pyyaml | 6.0.0 |
| tqdm | 4.66.0 |
| validators | 0.22.0 |

---

## Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/sudoinstallopsecc/kndys.git
cd kndys
```

### Step 2: Ensure Python 3 Is Installed

```bash
python3 --version
```

If Python 3 is not installed:

```bash
# Debian/Ubuntu/Kali
sudo apt update && sudo apt install python3 python3-pip -y

# Fedora
sudo dnf install python3 python3-pip -y

# Arch Linux
sudo pacman -S python python-pip
```

### Step 3: Run the Framework

```bash
python3 kndys.py
```

On the first execution, all required Python packages will be installed automatically. If automatic installation fails, install dependencies manually:

```bash
pip3 install requests colorama beautifulsoup4 lxml urllib3 cryptography pycryptodome PyJWT scapy python-nmap paramiko dnspython netifaces selenium webdriver-manager qrcode Pillow twilio pyyaml tqdm validators
```

On modern Linux distributions that restrict pip system-wide installs, use:

```bash
pip3 install --break-system-packages requests colorama beautifulsoup4 lxml urllib3 cryptography pycryptodome PyJWT scapy python-nmap paramiko dnspython netifaces selenium webdriver-manager qrcode Pillow twilio pyyaml tqdm validators
```

Alternatively, use a virtual environment:

```bash
python3 -m venv kndys-env
source kndys-env/bin/activate
pip install requests colorama beautifulsoup4 lxml urllib3 cryptography pycryptodome PyJWT scapy python-nmap paramiko dnspython netifaces selenium webdriver-manager qrcode Pillow twilio pyyaml tqdm validators
python3 kndys.py
```

### Step 4 (Optional): Make the Script Executable

```bash
chmod +x kndys.py
./kndys.py
```

---

## Getting Started

After launching the framework, you will see the KNDYS banner and a command prompt:

```
kndys >
```

### Basic Workflow

1. **Browse categories:** `show modules`
2. **View modules in a category:** `show modules recon`
3. **Select a module:** `use recon/port_scanner`
4. **View module options:** `options`
5. **Configure options:** `set target 192.168.1.1`
6. **Execute the module:** `run`
7. **Return to the main menu:** `back`

### Example Session

```
kndys > show modules recon
kndys > use recon/port_scanner
kndys(port_scanner) > set target 10.0.0.1
kndys(port_scanner) > set ports 1-1000
kndys(port_scanner) > run
kndys(port_scanner) > back
kndys >
```

---

## Interface Overview

### Command Reference

| Command | Description |
|---------|-------------|
| `help` | Display the full command reference |
| `clear` | Clear the screen and redisplay the banner |
| `exit` / `quit` | Exit the framework |
| `show modules` | List all module categories |
| `show modules <category>` | List modules within a specific category |
| `use <category/module>` | Select a module for configuration |
| `options` | Display the current module options |
| `set <option> <value>` | Set a module option |
| `run` | Execute the currently selected module |
| `back` | Deselect the current module |
| `show payloads` | List available payload generators |
| `generate payload` | Generate a payload interactively |
| `show wordlists` | Browse the wordlist catalog |
| `download wordlist <alias>` | Download a wordlist by its alias |
| `setg <option> <value>` | Set a global configuration option |
| `stats` | Display framework statistics |
| `metrics` | Display performance metrics |
| `sessions` | List active sessions |
| `search exploits <query>` | Search the exploit database |

---

## Module Categories

| Category | Modules | Description |
|----------|---------|-------------|
| recon | 5 | Reconnaissance and information gathering |
| scan | 6 | Vulnerability and security scanning |
| exploit | 6 | Exploitation and attack execution |
| post | 6 | Post-exploitation and persistence |
| password | 4 | Password attacks and credential recovery |
| wireless | 3 | Wireless network analysis and attacks |
| social | 9 | Social engineering and phishing |
| network | 5 | Network attacks and traffic manipulation |
| webapp | 5 | Web application security testing |
| report | 2 | Reporting and evidence management |

---

## 1. Reconnaissance (recon)

### recon/port_scanner

Performs TCP port scanning with service detection, banner grabbing, and vulnerability checks against a database of 90+ known services.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| target | 192.168.1.1 | Target IP address or hostname |
| ports | 1-1000 | Port range or comma-separated list |
| threads | 50 | Number of concurrent threads |
| timeout | 2 | Connection timeout in seconds |
| scan_type | tcp_connect | Scan method (tcp_connect) |
| aggressive | false | Enable aggressive scanning |

**Example:**

```
kndys > use recon/port_scanner
kndys(port_scanner) > set target 192.168.1.100
kndys(port_scanner) > set ports 1-65535
kndys(port_scanner) > set threads 100
kndys(port_scanner) > set aggressive true
kndys(port_scanner) > run
```

---

### recon/subdomain_scanner

Enumerates subdomains using DNS brute-force, zone transfer attempts, certificate transparency logs, and wildcard detection. Optionally verifies discovered subdomains via HTTP.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| domain | example.com | Target domain |
| wordlist | (empty) | Path to a subdomain wordlist file |
| threads | 20 | Number of concurrent threads |
| techniques | all | Enumeration techniques to use |
| verify_http | true | Verify subdomains via HTTP request |
| output | subdomains.txt | Output file for results |

**Example:**

```
kndys > use recon/subdomain_scanner
kndys(subdomain_scanner) > set domain targetsite.com
kndys(subdomain_scanner) > set wordlist /usr/share/wordlists/subdomains.txt
kndys(subdomain_scanner) > set threads 40
kndys(subdomain_scanner) > run
```

---

### recon/web_crawler

Crawls websites recursively, extracting links, JavaScript files, technologies, and potential vulnerabilities. Includes sensitive file detection.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com | Starting URL |
| depth | 3 | Maximum crawl depth |
| threads | 10 | Number of concurrent threads |
| max_pages | 100 | Maximum number of pages to crawl |
| respect_robots | true | Respect robots.txt |
| scan_vulns | false | Scan for vulnerabilities during crawl |
| extract_js | true | Extract JavaScript files |
| sensitive_scan | true | Scan for sensitive files |
| sensitive_timeout | 3 | Timeout for sensitive file checks |
| sensitive_workers | 5 | Workers for sensitive file scanning |

**Example:**

```
kndys > use recon/web_crawler
kndys(web_crawler) > set url https://targetsite.com
kndys(web_crawler) > set depth 5
kndys(web_crawler) > set scan_vulns true
kndys(web_crawler) > run
```

---

### recon/network_mapper

Discovers hosts on a network, resolves hostnames, detects operating systems, and optionally maps network topology.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| network | 192.168.1.0/24 | Target network in CIDR notation |
| scan_type | ping | Scan type: ping, tcp, udp, all |
| timeout | 1 | Response timeout in seconds |
| resolve_hostnames | true | Resolve hostnames via DNS |
| detect_os | true | Attempt OS detection |
| service_detection | false | Detect running services |
| topology_map | false | Generate network topology map |
| max_workers | 30 | Number of concurrent workers |

**Example:**

```
kndys > use recon/network_mapper
kndys(network_mapper) > set network 10.0.0.0/24
kndys(network_mapper) > set scan_type all
kndys(network_mapper) > set service_detection true
kndys(network_mapper) > run
```

---

### recon/os_detection

Identifies remote operating systems using TCP/IP stack fingerprinting, banner grabbing, and port analysis.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| target | 192.168.1.1 | Target IP address |
| deep_scan | false | Enable deep fingerprinting |
| port_scan | true | Perform port scan for analysis |
| banner_grab | true | Grab service banners |
| timing | normal | Scan timing: fast, normal, slow |
| custom_ports | (empty) | Custom ports to probe |
| max_ports | 60 | Maximum number of ports to scan |

**Example:**

```
kndys > use recon/os_detection
kndys(os_detection) > set target 192.168.1.50
kndys(os_detection) > set deep_scan true
kndys(os_detection) > run
```

---

## 2. Scanning (scan)

### scan/vuln_scanner

Comprehensive vulnerability scanner that performs 33 different security checks against a target, including header analysis, SSL/TLS issues, common misconfigurations, and known CVEs.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| target | http://example.com | Target URL |
| scan_type | full | Scan type: quick, web, api, full |
| threads | 5 | Number of concurrent threads |
| depth | 2 | Scan depth level |
| aggressive | false | Enable aggressive testing |
| stealth_mode | false | Minimize detection footprint |

**Example:**

```
kndys > use scan/vuln_scanner
kndys(vuln_scanner) > set target https://targetsite.com
kndys(vuln_scanner) > set scan_type full
kndys(vuln_scanner) > set aggressive true
kndys(vuln_scanner) > run
```

---

### scan/sql_scanner

Detects SQL injection vulnerabilities using time-based, error-based, and boolean techniques.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com/page.php?id=1 | URL with injectable parameter |
| technique | time_based,error_based,boolean | Detection techniques |
| threads | 5 | Number of concurrent threads |

**Example:**

```
kndys > use scan/sql_scanner
kndys(sql_scanner) > set url http://target.com/product.php?id=1
kndys(sql_scanner) > set technique time_based,error_based,boolean
kndys(sql_scanner) > run
```

---

### scan/xss_scanner

Detects Cross-Site Scripting (XSS) vulnerabilities, including reflected, stored, and DOM-based XSS.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com | Target URL |
| method | auto | HTTP method: get, post, both, auto |
| parameters | auto | Parameters to test (auto-detect) |
| scope | single | Scope: single, host, crawl |
| crawl_depth | 2 | Crawl depth when scope is crawl |
| max_pages | 15 | Max pages to test |
| threads | 12 | Number of concurrent threads |
| mode | balanced | Mode: fast, balanced, deep |
| include_forms | true | Test HTML forms |
| include_dom | true | Test for DOM-based XSS |
| stored_check | false | Check for stored XSS |
| stealth | false | Reduce detection footprint |

**Example:**

```
kndys > use scan/xss_scanner
kndys(xss_scanner) > set url http://target.com/search
kndys(xss_scanner) > set scope crawl
kndys(xss_scanner) > set mode deep
kndys(xss_scanner) > set include_dom true
kndys(xss_scanner) > run
```

---

### scan/csrf_scanner

Analyzes forms for CSRF (Cross-Site Request Forgery) protection, checking tokens, SameSite cookies, and Referer validation. Generates proof-of-concept payloads.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com | Target URL |
| scope | single | Scope: single, host, crawl |
| mode | balanced | Mode: fast, balanced, deep |
| crawl_depth | 2 | Crawl depth |
| max_pages | 12 | Max pages to analyze |
| form_limit | 40 | Max forms to test |
| method_filter | all | Filter by method: post, get, all |
| threads | 8 | Concurrent threads |
| check_samesite | true | Check SameSite cookie attribute |
| check_referer | true | Check Referer header validation |
| verify_tokens | true | Verify CSRF token implementation |
| generate_poc | true | Generate proof-of-concept payloads |

**Example:**

```
kndys > use scan/csrf_scanner
kndys(csrf_scanner) > set url https://target.com/admin
kndys(csrf_scanner) > set scope crawl
kndys(csrf_scanner) > set generate_poc true
kndys(csrf_scanner) > run
```

---

### scan/ssl_scanner

Analyzes SSL/TLS configurations, including protocol support, cipher suites, certificate validity, and security headers.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| target | example.com:443 | Target host:port |
| mode | balanced | Mode: fast, balanced, deep |
| protocol_scan | true | Scan supported protocols |
| cipher_scan | true | Enumerate cipher suites |
| http_headers | true | Check HTTP security headers |
| ocsp | true | Check OCSP stapling |
| resumption | false | Test session resumption |
| timeout | 8 | Connection timeout |

**Example:**

```
kndys > use scan/ssl_scanner
kndys(ssl_scanner) > set target targetsite.com:443
kndys(ssl_scanner) > set mode deep
kndys(ssl_scanner) > run
```

---

### scan/dir_traversal

Tests for directory traversal (path traversal) vulnerabilities using multiple encoding methods and platform-specific payloads.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com/download?file=FUZZ | URL with FUZZ marker |
| method | get | HTTP method |
| parameter | file | Vulnerable parameter name |
| marker | FUZZ | Placeholder in URL for payloads |
| depth | 6 | Traversal depth (../ levels) |
| payload_profile | balanced | Profile: balanced |
| encodings | standard,url,double,nullbyte,win | Encoding methods |
| platform | auto | Target platform: auto, linux, windows |
| threads | 10 | Concurrent threads |
| timeout | 6 | Request timeout |

**Example:**

```
kndys > use scan/dir_traversal
kndys(dir_traversal) > set url http://target.com/download?file=FUZZ
kndys(dir_traversal) > set depth 8
kndys(dir_traversal) > set platform linux
kndys(dir_traversal) > run
```

---

## 3. Exploitation (exploit)

### exploit/multi_handler

Listens for incoming reverse shell connections. Supports TCP transport, session management, and optional SSL encryption.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| lhost | (auto-detected) | Local IP address to listen on |
| lport | 4444 | Local port to listen on |
| transport | tcp | Transport protocol |
| payload | raw_reverse_shell | Expected payload type |
| max_sessions | 12 | Maximum concurrent sessions |
| idle_timeout | 900 | Session idle timeout (seconds) |
| record_sessions | true | Log session activity |
| ssl_cert | (empty) | Path to SSL certificate |
| ssl_key | (empty) | Path to SSL private key |

**Example:**

```
kndys > use exploit/multi_handler
kndys(multi_handler) > set lhost 192.168.1.10
kndys(multi_handler) > set lport 4444
kndys(multi_handler) > run
```

---

### exploit/sql_injection

Exploits SQL injection vulnerabilities using boolean, union, error-based, and time-based techniques.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com/vuln.php?id=1 | Vulnerable URL |
| method | auto | HTTP method: auto, get, post |
| parameters | auto | Parameters to inject |
| techniques | boolean,union,error,time | Injection techniques |
| max_depth | 6 | Maximum injection depth |
| threads | 8 | Concurrent threads |
| timeout | 8 | Request timeout |
| delay_threshold | 3 | Time-based delay threshold (seconds) |

**Example:**

```
kndys > use exploit/sql_injection
kndys(sql_injection) > set url http://target.com/login.php?user=admin
kndys(sql_injection) > set techniques boolean,union,error,time
kndys(sql_injection) > run
```

---

### exploit/xss_exploit

Exploits confirmed XSS vulnerabilities with cookie stealing, session hijacking, and optional callback listener.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com/search.php?q= | Vulnerable URL |
| method | auto | HTTP method |
| parameters | auto | Injectable parameters |
| payload_profile | balanced | Payload intensity |
| custom_payload | (empty) | Custom XSS payload |
| encoder | none | Payload encoder |
| auto_verify | true | Auto-verify injections |
| start_listener | false | Start callback listener |
| listener_host | (auto) | Listener IP address |
| listener_port | 9090 | Listener port |

**Example:**

```
kndys > use exploit/xss_exploit
kndys(xss_exploit) > set url http://target.com/search?q=
kndys(xss_exploit) > set start_listener true
kndys(xss_exploit) > set listener_host 192.168.1.10
kndys(xss_exploit) > run
```

---

### exploit/command_injection

Tests and exploits command injection vulnerabilities in web applications.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com/cmd.php?cmd=whoami | Vulnerable URL |
| method | auto | HTTP method |
| parameters | auto | Injectable parameters |
| os_profile | auto | Target OS: auto, linux, windows |
| attack_modes | detect,blind,enumeration | Attack modes |
| confirm_command | whoami | Command to confirm injection |
| blind_delay | 5 | Blind injection delay (seconds) |
| threads | 4 | Concurrent threads |

**Example:**

```
kndys > use exploit/command_injection
kndys(command_injection) > set url http://target.com/ping.php?host=127.0.0.1
kndys(command_injection) > set os_profile linux
kndys(command_injection) > run
```

---

### exploit/file_upload

Exploits unrestricted file upload vulnerabilities to upload web shells and verify execution.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com/upload.php | Upload endpoint URL |
| method | post | HTTP method |
| parameter | file | File parameter name |
| webshell_type | php | Shell type: php, asp, jsp |
| max_payloads | 6 | Number of bypass attempts |
| auto_shell_verify | true | Verify shell accessibility |
| shell_param | cmd | Web shell command parameter |
| shell_command | id | Command to verify shell |
| threads | 4 | Concurrent threads |

**Example:**

```
kndys > use exploit/file_upload
kndys(file_upload) > set url http://target.com/upload.php
kndys(file_upload) > set webshell_type php
kndys(file_upload) > set auto_shell_verify true
kndys(file_upload) > run
```

---

### exploit/buffer_overflow

Framework for testing buffer overflow vulnerabilities with progressive and cyclic pattern strategies.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| target | 192.168.1.100:9999 | Target host:port |
| protocol | tcp | Network protocol |
| command_template | TRUN /.:/{{PAYLOAD}}\r\n | Command template with payload placeholder |
| payload_strategy | progressive,cyclic | Buffer generation strategy |
| start_length | 256 | Initial buffer size |
| max_length | 4096 | Maximum buffer size |
| step_length | 256 | Buffer size increment |
| cyclic_length | 2048 | Cyclic pattern length |
| stop_on_crash | true | Stop when crash detected |

**Example:**

```
kndys > use exploit/buffer_overflow
kndys(buffer_overflow) > set target 192.168.1.50:9999
kndys(buffer_overflow) > set max_length 8192
kndys(buffer_overflow) > set step_length 512
kndys(buffer_overflow) > run
```

---

## 4. Post-Exploitation (post)

### post/shell

Provides an interactive shell on the target system within a session context.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| session | 1 | Session ID to use |
| command | whoami | Initial command |
| mode | interactive | Mode: interactive, oneshot, batch, script |
| timeout | 10 | Command execution timeout |
| history_limit | 50 | Maximum command history entries |
| record_transcript | true | Record all commands and output |
| allow_commands | (empty) | Whitelist of allowed commands |
| deny_commands | (empty) | Blacklist of denied commands |

**Example:**

```
kndys > use post/shell
kndys(shell) > set session 1
kndys(shell) > set mode interactive
kndys(shell) > run
```

---

### post/file_explorer

Explores the file system of a compromised target, listing files, searching by pattern, and previewing contents.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| session | 1 | Session ID |
| path | / | Starting path |
| root | / | Root boundary (cannot navigate above) |
| mode | list | Mode: list, search, tree |
| max_depth | 2 | Maximum recursion depth |
| max_entries | 200 | Maximum entries to display |
| include_hidden | false | Show hidden files |
| pattern | (empty) | File name pattern to match |
| file_types | all | Filter by type |
| hash_files | false | Calculate file hashes |
| preview | false | Preview file contents |

**Example:**

```
kndys > use post/file_explorer
kndys(file_explorer) > set session 1
kndys(file_explorer) > set path /etc
kndys(file_explorer) > set pattern *.conf
kndys(file_explorer) > set include_hidden true
kndys(file_explorer) > run
```

---

### post/privilege_escalation

Performs automated privilege escalation checks: SUID binaries, writable paths, cron jobs, sudo misconfigurations, Docker socket access, and kernel version analysis.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| session | 1 | Session ID |
| checks | suid,writable,path,cron,sudo,docker,kernel | Checks to perform |
| max_items | 50 | Maximum items per check |
| max_workers | 4 | Concurrent workers |
| include_home | true | Include home directories |
| suid_paths | /bin,/sbin,/usr/bin,/usr/sbin | Paths to search for SUID binaries |
| allow_sudo | false | Allow sudo checks (may trigger alerts) |

**Example:**

```
kndys > use post/privilege_escalation
kndys(privilege_escalation) > set session 1
kndys(privilege_escalation) > set checks suid,writable,cron,sudo,kernel
kndys(privilege_escalation) > run
```

---

### post/credential_dumper

Extracts stored credentials from the compromised system (registry, SAM, shadow files, browser stores).

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| session | 1 | Session ID |
| os | windows | Target OS: windows, linux |

**Example:**

```
kndys > use post/credential_dumper
kndys(credential_dumper) > set session 1
kndys(credential_dumper) > set os linux
kndys(credential_dumper) > run
```

---

### post/persistence

Establishes persistence mechanisms on a compromised system (services, scheduled tasks, registry entries).

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| session | 1 | Session ID |
| method | service | Persistence method |

**Example:**

```
kndys > use post/persistence
kndys(persistence) > set session 1
kndys(persistence) > set method service
kndys(persistence) > run
```

---

### post/pivot

Enables network pivoting and lateral movement from a compromised host to other internal networks.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| session | 1 | Session ID |
| target | 192.168.2.0/24 | Target network for pivoting |

**Example:**

```
kndys > use post/pivot
kndys(pivot) > set session 1
kndys(pivot) > set target 10.10.10.0/24
kndys(pivot) > run
```

---

## 5. Password Attacks (password)

### password/brute_force

Performs brute-force password attacks against network services (SSH, FTP, HTTP, etc.).

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| target | ssh://192.168.1.1:22 | Target in format protocol://host:port |
| username | admin | Username to attack |
| wordlist | passwords.txt | Password wordlist file |
| service | ssh | Target service type |

**Example:**

```
kndys > use password/brute_force
kndys(brute_force) > set target ssh://192.168.1.100:22
kndys(brute_force) > set username root
kndys(brute_force) > set wordlist /usr/share/wordlists/rockyou.txt
kndys(brute_force) > set service ssh
kndys(brute_force) > run
```

---

### password/hash_cracker

Cracks password hashes using dictionary attacks, rule-based mutations, and mask attacks. Supports MD5, SHA-1, SHA-256, SHA-512, bcrypt, and more.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| hash | 5f4dcc3b5aa765d61d8327deb882cf99 | Hash to crack |
| type | md5 | Hash algorithm |
| wordlist | rockyou.txt | Wordlist file |
| hash_file | (empty) | File with multiple hashes |
| password_profile | core | Password mutation profile |
| salt | (empty) | Salt value (if applicable) |
| salt_position | suffix | Salt position: prefix, suffix |
| mask | (empty) | Mask for mask attacks |
| max_workers | 8 | Concurrent worker threads |
| smart_rules | true | Enable smart mutation rules |

**Example:**

```
kndys > use password/hash_cracker
kndys(hash_cracker) > set hash 5f4dcc3b5aa765d61d8327deb882cf99
kndys(hash_cracker) > set type md5
kndys(hash_cracker) > set wordlist rockyou.txt
kndys(hash_cracker) > set smart_rules true
kndys(hash_cracker) > run
```

To crack from a file containing multiple hashes:

```
kndys(hash_cracker) > set hash_file hashes.txt
kndys(hash_cracker) > set type sha256
kndys(hash_cracker) > run
```

---

### password/spray_attack

Performs password spraying against a target, trying a small number of passwords across many user accounts with controlled delays to avoid lockouts.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| target | owa.example.com | Target host or service |
| usernames | users.txt | File containing usernames |
| passwords | passwords.txt | File containing passwords |
| delay | 10 | Delay between attempts (seconds) |

**Example:**

```
kndys > use password/spray_attack
kndys(spray_attack) > set target mail.company.com
kndys(spray_attack) > set usernames users.txt
kndys(spray_attack) > set passwords common_passwords.txt
kndys(spray_attack) > set delay 30
kndys(spray_attack) > run
```

---

### password/credential_stuffing

Tests leaked credential pairs (username:password) against a login endpoint.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| target | http://example.com/login | Target login URL |
| credentials | creds.txt | File with username:password pairs |
| threads | 5 | Concurrent threads |

**Example:**

```
kndys > use password/credential_stuffing
kndys(credential_stuffing) > set target https://target.com/api/login
kndys(credential_stuffing) > set credentials leaked_creds.txt
kndys(credential_stuffing) > set threads 10
kndys(credential_stuffing) > run
```

---

## 6. Wireless (wireless)

Note: Wireless modules require root privileges and a wireless adapter capable of monitor mode.

### wireless/wifi_scanner

Scans for nearby wireless networks, displaying SSIDs, BSSIDs, channels, signal strength, and encryption types.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| interface | wlan0 | Wireless interface |
| channel | all | Channel to scan (all or specific number) |

**Example:**

```
sudo python3 kndys.py
kndys > use wireless/wifi_scanner
kndys(wifi_scanner) > set interface wlan0
kndys(wifi_scanner) > set channel all
kndys(wifi_scanner) > run
```

---

### wireless/wifi_cracker

Cracks WPA/WPA2 handshakes using dictionary attacks against a captured PCAP file.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| handshake | capture.pcap | Path to handshake capture file |
| wordlist | rockyou.txt | Password wordlist |
| bssid | 00:11:22:33:44:55 | Target access point BSSID |

**Example:**

```
kndys > use wireless/wifi_cracker
kndys(wifi_cracker) > set handshake /tmp/capture.pcap
kndys(wifi_cracker) > set wordlist /usr/share/wordlists/rockyou.txt
kndys(wifi_cracker) > set bssid AA:BB:CC:DD:EE:FF
kndys(wifi_cracker) > run
```

---

### wireless/rogue_ap

Creates a rogue (fake) access point to intercept traffic from connecting clients.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| interface | wlan0 | Wireless interface |
| ssid | Free_WiFi | Name of the rogue network |
| channel | 6 | Broadcast channel |

**Example:**

```
kndys > use wireless/rogue_ap
kndys(rogue_ap) > set interface wlan0
kndys(rogue_ap) > set ssid Company_Guest
kndys(rogue_ap) > set channel 11
kndys(rogue_ap) > run
```

---

## 7. Social Engineering (social)

### social/phishing

Manages phishing email campaigns with built-in templates, tracking, and analytics.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| template | office365 | Email template |
| targets | emails.txt | File with target email addresses |
| smtp_server | smtp.gmail.com | SMTP server |
| smtp_port | 587 | SMTP port |
| smtp_user | (empty) | SMTP username |
| smtp_password | (empty) | SMTP password |
| from_email | (empty) | Sender email address |
| from_name | IT Support | Sender display name |
| campaign_name | phishing_campaign | Campaign identifier |
| subject | (empty) | Email subject line |
| phish_url | http://localhost:8080 | Phishing URL in email body |
| track_opens | true | Track email opens |
| track_clicks | true | Track link clicks |
| threads | 5 | Sending threads |
| rate_limit | 10 | Emails per minute |

**Example:**

```
kndys > use social/phishing
kndys(phishing) > set template office365
kndys(phishing) > set targets target_emails.txt
kndys(phishing) > set smtp_server smtp.gmail.com
kndys(phishing) > set smtp_user attacker@gmail.com
kndys(phishing) > set smtp_password app_password_here
kndys(phishing) > set from_email security@company.com
kndys(phishing) > set subject Urgent: Password Reset Required
kndys(phishing) > set phish_url http://192.168.1.10:8080
kndys(phishing) > run
```

---

### social/credential_harvester

Starts a local web server with a cloned login page to harvest credentials. Includes 15 built-in templates and browser fingerprinting.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| port | 8080 | Listening port |
| template | facebook | Login page template |
| redirect_url | https://facebook.com | URL to redirect after capture |
| redirect_delay | 3 | Redirect delay in seconds |
| db_path | harvester_creds.db | Credential database file |
| enable_ssl | false | Enable HTTPS |
| enable_fingerprinting | true | Browser fingerprinting |
| enable_geolocation | true | Geolocate visitors |
| max_attempts | 3 | Max capture attempts per session |

**Example:**

```
kndys > use social/credential_harvester
kndys(credential_harvester) > set port 8080
kndys(credential_harvester) > set template google
kndys(credential_harvester) > set redirect_url https://google.com
kndys(credential_harvester) > run
```

---

### social/website_cloner

Clones websites for phishing, with credential harvesting injection, form modification, anti-detection features, and built-in web server.

**Options (key options):**

| Option | Default | Description |
|--------|---------|-------------|
| url | https://facebook.com | URL to clone |
| output | phish_site | Output directory name |
| clone_depth | 2 | Recursion depth |
| inject_harvester | true | Inject credential harvesting |
| modify_forms | true | Redirect forms to harvester |
| form_action | /harvest | Form submission endpoint |
| start_server | true | Start local web server |
| server_port | 8080 | Web server port |
| bypass_csp | true | Remove Content Security Policy |
| template | none | Template: none, facebook, google, microsoft |

**Example:**

```
kndys > use social/website_cloner
kndys(website_cloner) > set url https://login.target.com
kndys(website_cloner) > set server_port 8080
kndys(website_cloner) > set inject_harvester true
kndys(website_cloner) > set modify_forms true
kndys(website_cloner) > run
```

---

### social/mass_mailer

Manages large-scale email campaigns with templates, personalization, A/B testing, scheduling, and delivery tracking.

**Options (key options):**

| Option | Default | Description |
|--------|---------|-------------|
| smtp_server | smtp.gmail.com | SMTP server |
| smtp_port | 587 | SMTP port |
| smtp_user | (empty) | SMTP username |
| smtp_password | (empty) | SMTP password |
| from_email | (empty) | Sender email |
| from_name | Newsletter Team | Sender name |
| subject | (empty) | Email subject |
| template | newsletter | Email template |
| targets | targets.csv | Target list (CSV) |
| personalize | true | Enable personalization |
| threads | 10 | Sending threads |
| rate_limit | 50 | Emails per minute |
| track_opens | true | Track opens |
| track_clicks | true | Track clicks |

**Example:**

```
kndys > use social/mass_mailer
kndys(mass_mailer) > set smtp_server smtp.gmail.com
kndys(mass_mailer) > set smtp_user account@gmail.com
kndys(mass_mailer) > set smtp_password app_password
kndys(mass_mailer) > set from_email newsletter@company.com
kndys(mass_mailer) > set subject Monthly Security Update
kndys(mass_mailer) > set targets employee_list.csv
kndys(mass_mailer) > run
```

---

### social/qr_generator

Generates QR codes for phishing campaigns. Supports URLs, vCards, WiFi credentials, email, SMS, geographic coordinates, and cryptocurrency addresses.

**Options (key options):**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://malicious-site.com | Destination URL |
| qr_type | url | Type: url, vcard, wifi, email, sms, phone, geo, text, crypto |
| output | qr_code.png | Output file name |
| size | 300 | QR code size in pixels |
| error_correction | M | Error correction level: L, M, Q, H |
| format | png | Output format: png, svg, pdf, eps |
| fill_color | black | QR code color |
| back_color | white | Background color |
| logo | (empty) | Logo image to embed |
| tracking | true | Enable scan tracking |
| batch_mode | false | Enable batch generation |
| batch_file | urls.txt | File with URLs for batch mode |

**Example:**

```
kndys > use social/qr_generator
kndys(qr_generator) > set url http://192.168.1.10:8080/phish
kndys(qr_generator) > set output company_wifi.png
kndys(qr_generator) > set size 500
kndys(qr_generator) > run
```

To generate a WiFi QR code:

```
kndys(qr_generator) > set qr_type wifi
kndys(qr_generator) > set wifi_ssid FreeInternet
kndys(qr_generator) > set wifi_password password123
kndys(qr_generator) > set wifi_encryption WPA
kndys(qr_generator) > run
```

---

### social/usb_payload

Generates payloads for USB attack devices (Rubber Ducky, Bash Bunny, Teensy, etc.) with encoding, obfuscation, and anti-detection features.

**Options (key options):**

| Option | Default | Description |
|--------|---------|-------------|
| payload_type | reverse_shell | Payload: reverse_shell, keylogger, exfiltration, persistence |
| target_os | windows | Target: windows, linux, macos, multi |
| device_type | rubber_ducky | Device: rubber_ducky, bash_bunny, teensy, digispark |
| lhost | (auto) | Callback IP address |
| lport | 4444 | Callback port |
| obfuscation_level | medium | Level: none, low, medium, high, extreme |
| anti_av | true | Anti-antivirus techniques |
| anti_sandbox | true | Anti-sandbox detection |
| execution_method | powershell | Method: powershell, cmd, wmi |
| window_style | hidden | Window: hidden, minimized, normal |
| keystroke_delay | 50 | Delay between keystrokes (ms) |

**Example:**

```
kndys > use social/usb_payload
kndys(usb_payload) > set payload_type reverse_shell
kndys(usb_payload) > set target_os windows
kndys(usb_payload) > set device_type rubber_ducky
kndys(usb_payload) > set lhost 192.168.1.10
kndys(usb_payload) > set lport 4444
kndys(usb_payload) > run
```

---

### social/fake_update

Generates a fake software update page that delivers a payload when the user clicks "Update."

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| software | chrome | Software to impersonate |
| payload | update.exe | Payload file to serve |
| port | 8080 | Web server port |

**Example:**

```
kndys > use social/fake_update
kndys(fake_update) > set software chrome
kndys(fake_update) > set payload /path/to/payload.exe
kndys(fake_update) > set port 8080
kndys(fake_update) > run
```

---

### social/sms_spoofing

Sends spoofed SMS messages using third-party providers (Twilio, Vonage, AWS SNS, etc.) for social engineering campaigns.

**Options (key options):**

| Option | Default | Description |
|--------|---------|-------------|
| provider | twilio | SMS provider |
| twilio_sid | (empty) | Twilio Account SID |
| twilio_token | (empty) | Twilio Auth Token |
| twilio_number | (empty) | Twilio phone number |
| message | Your package is ready. Track: {link} | SMS message body |
| sender | DHL | Sender ID (alphanumeric) |
| targets | phones.txt | File with phone numbers |
| template | custom | Template: custom, delivery, bank, security |
| link | http://track.example.com/123 | Link to include in message |
| delay | 2 | Delay between messages (seconds) |
| dry_run | false | Simulate without sending |

**Example:**

```
kndys > use social/sms_spoofing
kndys(sms_spoofing) > set provider twilio
kndys(sms_spoofing) > set twilio_sid ACXXXXXXXXXXXXX
kndys(sms_spoofing) > set twilio_token your_auth_token
kndys(sms_spoofing) > set twilio_number +15551234567
kndys(sms_spoofing) > set message Your account requires verification: {link}
kndys(sms_spoofing) > set sender SecureBank
kndys(sms_spoofing) > set targets phone_numbers.txt
kndys(sms_spoofing) > set link http://192.168.1.10:8080/verify
kndys(sms_spoofing) > run
```

---

### social/pretexting

Generates social engineering pretexting scenarios tailored to a target organization.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| scenario | it_support | Scenario type |
| company | TechCorp | Target company name |
| urgency | high | Urgency level: low, medium, high |

**Example:**

```
kndys > use social/pretexting
kndys(pretexting) > set scenario it_support
kndys(pretexting) > set company TargetCorp
kndys(pretexting) > set urgency high
kndys(pretexting) > run
```

---

## 8. Network Attacks (network)

Note: Network attack modules require root privileges and, in most cases, a properly configured network interface.

### network/arp_spoof

Performs ARP spoofing for Man-in-the-Middle (MITM) attacks with credential harvesting, SSL stripping, DNS spoofing, and traffic injection capabilities.

**Options (key options):**

| Option | Default | Description |
|--------|---------|-------------|
| interface | eth0 | Network interface |
| target_ip | 192.168.1.100 | Target IP address |
| gateway_ip | 192.168.1.1 | Gateway/router IP |
| mode | bidirectional | Mode: bidirectional, unidirectional, gateway_only |
| poison_interval | 2 | Seconds between ARP packets |
| restore_arp | true | Restore ARP tables on exit |
| enable_ssl_strip | true | Strip HTTPS to HTTP |
| enable_dns_spoof | true | Spoof DNS queries |
| enable_credential_harvest | true | Extract credentials from traffic |
| stealth_mode | true | Minimize detection |
| dry_run | false | Simulate attack without poisoning |

**Example:**

```
sudo python3 kndys.py
kndys > use network/arp_spoof
kndys(arp_spoof) > set interface eth0
kndys(arp_spoof) > set target_ip 192.168.1.50
kndys(arp_spoof) > set gateway_ip 192.168.1.1
kndys(arp_spoof) > set enable_credential_harvest true
kndys(arp_spoof) > run
```

---

### network/dns_spoof

Intercepts and spoofs DNS queries, redirecting domain requests to attacker-controlled IP addresses.

**Options (key options):**

| Option | Default | Description |
|--------|---------|-------------|
| interface | eth0 | Network interface |
| listen_port | 53 | DNS listening port |
| spoof_domains | (empty) | Domains to spoof (comma-separated) |
| spoof_ip | 192.168.1.100 | IP to redirect to |
| wildcard_mode | false | Spoof all subdomains |
| upstream_dns | 8.8.8.8 | Upstream DNS for non-spoofed queries |
| enable_cache | true | Cache DNS responses |
| log_queries | true | Log all DNS queries |
| stealth_mode | false | Minimize detection |
| dry_run | false | Simulate without spoofing |

**Example:**

```
sudo python3 kndys.py
kndys > use network/dns_spoof
kndys(dns_spoof) > set interface eth0
kndys(dns_spoof) > set spoof_domains login.company.com,mail.company.com
kndys(dns_spoof) > set spoof_ip 192.168.1.10
kndys(dns_spoof) > run
```

---

### network/dhcp_starvation

Exhausts DHCP server IP pools by flooding DISCOVER/REQUEST messages with spoofed MAC addresses.

**Options (key options):**

| Option | Default | Description |
|--------|---------|-------------|
| interface | eth0 | Network interface |
| target_network | 192.168.1.0/24 | Target network |
| attack_mode | starvation | Mode: starvation, dos, rogue, hybrid |
| request_count | 254 | Number of DHCP requests |
| request_rate | 100 | Requests per second |
| mac_generation | random | MAC generation: random, sequential, vendor |
| mac_vendor | cisco | Vendor to mimic |
| deploy_rogue_server | false | Deploy rogue DHCP server |
| dry_run | false | Simulate without attacking |
| auto_stop_timer | 600 | Auto-stop after N seconds |

**Example:**

```
sudo python3 kndys.py
kndys > use network/dhcp_starvation
kndys(dhcp_starvation) > set interface eth0
kndys(dhcp_starvation) > set target_network 192.168.1.0/24
kndys(dhcp_starvation) > set request_count 254
kndys(dhcp_starvation) > run
```

---

### network/ssl_strip

Performs SSL stripping to downgrade HTTPS connections to HTTP for traffic interception.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| interface | eth0 | Network interface |
| port | 8080 | Proxy port |

**Example:**

```
sudo python3 kndys.py
kndys > use network/ssl_strip
kndys(ssl_strip) > set interface eth0
kndys(ssl_strip) > set port 10000
kndys(ssl_strip) > run
```

---

### network/packet_sniffer

Captures and analyzes network packets with BPF filter support and PCAP output.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| interface | eth0 | Network interface |
| filter | tcp port 80 | BPF capture filter |
| output | capture.pcap | Output PCAP file |
| count | 100 | Number of packets to capture |

**Example:**

```
sudo python3 kndys.py
kndys > use network/packet_sniffer
kndys(packet_sniffer) > set interface eth0
kndys(packet_sniffer) > set filter tcp port 443
kndys(packet_sniffer) > set output https_traffic.pcap
kndys(packet_sniffer) > set count 500
kndys(packet_sniffer) > run
```

---

## 9. Web Application Testing (webapp)

### webapp/jwt_cracker

Tests JSON Web Tokens (JWT) for weak signing secrets using dictionary attacks.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| token | (empty) | JWT token to test |
| wordlist | secrets.txt | Wordlist of potential secrets |
| algorithm | HS256 | Expected signing algorithm |

**Example:**

```
kndys > use webapp/jwt_cracker
kndys(jwt_cracker) > set token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIn0.dozjgNryP4J3jVmNHl0w5N_XgL0n3I9PlFUP0THsR8U
kndys(jwt_cracker) > set wordlist /usr/share/wordlists/common_secrets.txt
kndys(jwt_cracker) > set algorithm HS256
kndys(jwt_cracker) > run
```

---

### webapp/api_fuzzer

Fuzzes REST API endpoints to discover hidden paths, test input validation, and find vulnerabilities.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | https://api.example.com | Base API URL |
| method | POST | HTTP method |
| endpoints | endpoints.txt | File with endpoint paths |

**Example:**

```
kndys > use webapp/api_fuzzer
kndys(api_fuzzer) > set url https://api.target.com
kndys(api_fuzzer) > set method GET
kndys(api_fuzzer) > set endpoints api_paths.txt
kndys(api_fuzzer) > run
```

---

### webapp/cors_scanner

Detects CORS (Cross-Origin Resource Sharing) misconfigurations that could allow unauthorized cross-origin access.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | https://example.com | Target URL |
| origin | https://evil.com | Origin header to test |

**Example:**

```
kndys > use webapp/cors_scanner
kndys(cors_scanner) > set url https://api.target.com
kndys(cors_scanner) > set origin https://attacker.com
kndys(cors_scanner) > run
```

---

### webapp/nosql_injection

Tests for NoSQL injection vulnerabilities in MongoDB, CouchDB, and other NoSQL databases through web endpoints.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | http://example.com/api | Target API endpoint |
| parameter | username | Parameter to test |
| technique | auth_bypass | Technique: auth_bypass |

**Example:**

```
kndys > use webapp/nosql_injection
kndys(nosql_injection) > set url http://target.com/api/login
kndys(nosql_injection) > set parameter username
kndys(nosql_injection) > set technique auth_bypass
kndys(nosql_injection) > run
```

---

### webapp/graphql_introspection

Performs GraphQL schema introspection to discover available queries, mutations, types, and fields.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| url | https://api.example.com/graphql | GraphQL endpoint |
| output | schema.json | Output file for schema |

**Example:**

```
kndys > use webapp/graphql_introspection
kndys(graphql_introspection) > set url https://api.target.com/graphql
kndys(graphql_introspection) > set output target_schema.json
kndys(graphql_introspection) > run
```

---

## 10. Reporting (report)

### report/report_generator

Generates professional penetration testing reports from collected data.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| format | html | Report format: html, json, txt |
| template | default | Report template |
| output | pentest_report | Output file name (without extension) |

**Example:**

```
kndys > use report/report_generator
kndys(report_generator) > set format html
kndys(report_generator) > set output final_report
kndys(report_generator) > run
```

---

### report/evidence_collector

Collects system information, network configuration, and other forensic data, then packages it into a ZIP archive.

**Options:**

| Option | Default | Description |
|--------|---------|-------------|
| session | 1 | Session ID |
| output | evidence.zip | Output archive file |

**Example:**

```
kndys > use report/evidence_collector
kndys(evidence_collector) > set session 1
kndys(evidence_collector) > set output evidence_2024.zip
kndys(evidence_collector) > run
```

---

## Wordlists and Payloads

### Built-in Wordlists

KNDYS ships with curated wordlists stored in the `wordlists/` directory:

- **kndys-passwords-core.txt** - Top multi-locale passwords
- **kndys-passwords-enterprise.txt** - Enterprise and seasonal passwords
- **kndys-passwords-webapp.txt** - Web administration passwords
- **kndys-passwords-spray.txt** - Spray-safe password set
- **kndys-passwords-iot.txt** - IoT and appliance default passwords
- **kndys-usernames-core.txt** - Enterprise administrator usernames
- **kndys-usernames-service.txt** - Service and daemon account names
- **kndys-credentials-defaults.txt** - Default credential pairs

### Downloading External Wordlists

Browse available wordlists:

```
kndys > show wordlists
```

Download a wordlist by alias:

```
kndys > download wordlist rockyou
kndys > download wordlist xato1m
kndys > download wordlist top-usernames
```

### Payload Generation

List available payload types:

```
kndys > show payloads
```

Generate a payload interactively:

```
kndys > generate payload
```

You will be prompted for the payload type (reverse_shell, bind_shell, web_shell), platform (bash, python, php, powershell), and connection parameters.

---

## Global Configuration

Set global options that persist across module selections:

```
kndys > setg lhost 192.168.1.10
kndys > setg lport 4444
kndys > setg output_dir /home/user/results
```

View framework statistics:

```
kndys > stats
```

View performance metrics:

```
kndys > metrics
```

View active sessions:

```
kndys > sessions
```

---

## Legal Disclaimer

KNDYS Framework is intended for authorized security testing and educational purposes only. Unauthorized access to computer systems is illegal. Always obtain explicit written permission before conducting any penetration testing activities. The developers assume no liability for misuse of this tool. Use responsibly and in compliance with all applicable laws and regulations.
