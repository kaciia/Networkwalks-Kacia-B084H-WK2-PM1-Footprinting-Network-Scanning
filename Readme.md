# PENETRATION TESTING REPORT
## Footprinting & Network Scanning Phases
### W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS

---

## Project Information

| Field | Details |
|---|---|
| Student Name | Kacia Rowe |
| Program | Cybersecurity & Penetration Testing |
| Institution | Networkwalks Academy |
| Batch | B084H |
| Report Date | 12 November 2026 |
| Project | Week 2 – Footprinting & Network Scanning |
| Modules Completed | W2-PM1 – Domain Footprinting (Kali Linux) |
| | W2-PM5 – Network Scanning (Zenmap) |
| Primary Target | networkwalks.com |
| Secondary Target | Personal Local Area Network (LAN) |
| Operating Systems | Kali Linux and Windows |
| Tools Used | WHOIS, WhatWeb, Nslookup, Curl, WAFW00F, DNSRecon and Zenmap |

---

# 1. LIABILITY DISCLAIMER

All activities documented in this report were conducted for educational and cybersecurity training purposes.

The domain reconnaissance activities were performed against `networkwalks.com` as part of the assigned Networkwalks Academy practical exercise. The network scanning activity was intended for my own local network.

Network scanning and penetration testing must only be conducted on systems, networks, and devices that are owned by the tester or for which explicit authorization has been granted.

No exploitation, unauthorized access, or intentional disruption of services was performed during these activities.

The information contained in this report is intended for educational and research purposes only. The author accepts responsibility for ensuring that all testing activities remain within the permitted scope.

---

# 2. INTRODUCTION

This report documents the practical cybersecurity activities completed as part of Week 2 of the Networkwalks Cybersecurity and Penetration Testing program.

The project focuses on two important stages of cybersecurity assessment:

1. Domain Footprinting and Reconnaissance using Kali Linux.
2. Local Network Discovery and Topology Mapping using Zenmap.

The first module involved gathering publicly available information about the target domain, `networkwalks.com`. Six Kali Linux tools were used to identify domain registration details, web technologies, DNS information, HTTP response headers, Web Application Firewall (WAF) protection, and additional DNS records.

The second module involved using Zenmap, the graphical interface for Nmap, to identify active devices on my local network. The objective was to determine the local network configuration, discover live hosts, identify their IP and MAC addresses where available, and produce a network topology diagram.

These activities demonstrate how reconnaissance and network discovery help cybersecurity professionals understand the structure and potential exposure of systems before conducting more advanced security assessments.

---

# 3. OBJECTIVES

The main objectives of this practical exercise were to:

- Identify domain registration information using WHOIS.
- Discover the technologies and web applications used by the target website.
- Resolve the target domain to its corresponding IP address.
- Examine HTTP response headers and identify security-related configurations.
- Determine whether a Web Application Firewall protects the target website.
- Enumerate DNS records associated with the target domain.
- Identify the local computer's IP address and subnet configuration.
- Discover active devices on the local network using Zenmap.
- Identify the IP and MAC addresses of discovered devices where available.
- Generate and document a network topology diagram.
- Understand the importance of responsible reconnaissance and network scanning.

---

# 4. TOOLS AND TECHNOLOGIES USED

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system used for reconnaissance activities. |
| WHOIS | Retrieves domain registration and registrar information. |
| WhatWeb | Identifies website technologies and server information. |
| Nslookup | Resolves domain names into IP addresses. |
| Curl | Retrieves HTTP response headers from a website. |
| WAFW00F | Identifies possible Web Application Firewall protection. |
| DNSRecon | Enumerates DNS records associated with a domain. |
| Windows Command Prompt | Identifies local network configuration using ipconfig. |
| Zenmap | Graphical interface for Nmap used for network discovery and topology mapping. |

---

# 5. MODULE 1 – DOMAIN FOOTPRINTING AND RECONNAISSANCE

## 5.1 Target Information

| Field | Details |
|---|---|
| Target Domain | networkwalks.com |
| Target URL | https://networkwalks.com |
| Assessment Type | Domain Footprinting and Passive Reconnaissance |
| Operating System | Kali Linux |
| Tools Used | WHOIS, WhatWeb, Nslookup, Curl, WAFW00F and DNSRecon |

The purpose of this module was to collect publicly accessible information about the target domain and its web infrastructure.

The following six tools were executed to gather information and analyze the results.

---

## 5.2 TASK 1 – WHOIS DOMAIN REGISTRATION LOOKUP

### Command Executed

```bash
whois networkwalks.com
```

### Objective

The WHOIS command was used to retrieve domain registration information, including the registrar, creation date, expiration date, domain status, name servers, and DNSSEC status.

### Findings

The WHOIS lookup returned the following information:

| Attribute | Result |
|---|---|
| Domain Name | NETWORKWALKS.COM |
| Registrar | GoDaddy.com, LLC |
| Registrar IANA ID | 146 |
| Domain Creation Date | 6 November 2019 |
| Last Updated | 12 November 2025 |
| Registry Expiration Date | 6 November 2027 |
| Registrant Organization | Domains By Proxy, LLC |
| Domain Status | Client Delete Prohibited |
| | Client Renew Prohibited |
| | Client Transfer Prohibited |
| | Client Update Prohibited |
| Name Servers | NS6135.HOSTGATOR.COM |
| | NS6136.HOSTGATOR.COM |
| Additional Name Servers Listed | NS29.DOMAINCONTROL.COM |
| | NS30.DOMAINCONTROL.COM |
| DNSSEC | Unsigned |

### Analysis

The WHOIS lookup identified GoDaddy.com, LLC as the domain registrar. The domain was originally registered on 6 November 2019 and has a registry expiration date of 6 November 2027.

The registrant information is protected through Domains By Proxy, LLC. This prevents the registrant's personal registration details from being publicly displayed.

Several domain status restrictions were also identified. These restrictions help prevent unauthorized domain deletion, renewal changes, transfers, and updates.

The WHOIS results reported that DNSSEC was unsigned. DNSSEC provides a mechanism for validating DNS responses and helping protect against certain DNS spoofing and cache-poisoning attacks. An unsigned domain does not benefit from DNSSEC validation.

The lookup also returned HostGator and DomainControl name server entries. These records were documented as returned by the WHOIS service.

### Evidence – Figure 1

**Insert WHOIS screenshot below.**

![Figure 1 – WHOIS Domain Registration Results](assets/whois.png)

---

## 5.3 TASK 2 – WEBSITE TECHNOLOGY FINGERPRINTING

### Command Executed

```bash
whatweb networkwalks.com
```

### Objective

WhatWeb was used to identify the technologies, content management system, web server, libraries, and other components associated with the target website.

### Findings

The successful WhatWeb scan returned the following information:

| Attribute | Result |
|---|---|
| Website | networkwalks.com |
| HTTP Response | 301 Moved Permanently |
| HTTPS Response | 200 OK |
| Web Server | Apache |
| IP Address | 192.232.216.135 |
| Country Identified | United States |
| Content Management System | WordPress |
| Reported WordPress Version | 7.1.4 |
| Reported Bootstrap Version | 7.1.4 |
| jQuery Version | 3.7.1 |
| WordPress Plugin | WordPress Download Manager 3.3.76 |
| Google Tag Manager | Detected |
| HTML5 | Detected |
| Cookie | __wpdm_client |
| Website Title | Networkwalks Academy |
| Email Identified | info@networkwalks.com |

### Analysis

The WhatWeb scan identified Apache as the web server and WordPress as the content management system.

Additional technologies included Bootstrap, jQuery, HTML5, Google Tag Manager, and the WordPress Download Manager plugin.

The initial HTTP request returned a 301 Moved Permanently response, redirecting traffic to the HTTPS version of the website. The HTTPS request returned a 200 OK response, indicating that the website successfully responded to the request.

The scan also identified the website's IP address as `192.232.216.135`.

Technology fingerprinting is useful because it helps security professionals understand the software components used by a website. Outdated or vulnerable software components can introduce security risks. However, the versions identified by WhatWeb should be independently verified before determining whether a vulnerability exists.

### Evidence – Figure 2

**Insert WhatWeb screenshot below.**

![Figure 2 – WhatWeb Technology Fingerprinting](assets/whatweb.png)

---

## 5.4 TASK 3 – DNS LOOKUP

### Command Executed

```bash
nslookup networkwalks.com
```

### Objective

Nslookup was used to resolve the target domain name into its corresponding IP address.

### Findings

The command returned the following information:

| Attribute | Result |
|---|---|
| DNS Server | 8.8.8.8 |
| DNS Server Provider | Google Public DNS |
| Domain | networkwalks.com |
| Resolved IP Address | 192.232.216.135 |
| Response Type | Non-authoritative answer |

### Analysis

The DNS lookup successfully resolved `networkwalks.com` to the IP address `192.232.216.135`.

The lookup was performed using Google's public DNS resolver at `8.8.8.8`.

The response was identified as non-authoritative because the answer was supplied by the recursive DNS resolver rather than directly by an authoritative DNS server.

The IP address obtained through Nslookup matched the IP address identified by WhatWeb. This consistency supports the accuracy of the observed domain resolution.

### Evidence – Figure 3

**Insert Nslookup screenshot below.**

![Figure 3 – Nslookup DNS Resolution](assets/nslookup.png)

---

## 5.5 TASK 4 – HTTP RESPONSE HEADER ANALYSIS

### Command Executed

```bash
curl -I https://networkwalks.com
```

### Objective

Curl was used to retrieve the HTTP response headers from the target website. These headers provide information about the web server, response status, cookies, content type, and certain security-related configurations.

### Findings

The command returned an HTTP 200 OK response.

The following headers and information were observed:

| Header / Attribute | Result |
|---|---|
| HTTP Status | 200 OK |
| Web Server | Apache |
| Content Type | text/html; charset=UTF-8 |
| Cookie | __wpdm_client |
| Secure Cookie Attribute | Present |
| HttpOnly Cookie Attribute | Present |
| Referrer-Policy | no-referrer-when-downgrade |
| Permissions-Policy | Present |
| WordPress REST API | /wp-json/ |
| WordPress Page API | /wp-json/wp/v2/pages/53 |
| Cache Information | X-Endurance-Cache-Level and X-nginx-cache |

### Analysis

The HTTP header inspection confirmed that the HTTPS version of the website returned a successful 200 OK response.

The response identified Apache as the web server and indicated that the website delivers HTML content using UTF-8 character encoding.

The `__wpdm_client` cookie included the Secure and HttpOnly attributes. The Secure attribute restricts the cookie to secure HTTPS connections, while HttpOnly helps prevent client-side JavaScript from accessing the cookie.

The response also included a Referrer-Policy header and a Permissions-Policy header. These headers provide browser-related privacy and security controls.

The WordPress REST API paths were also visible in the response headers. Their presence is not automatically a vulnerability, but publicly exposed endpoints should be reviewed to ensure that they do not disclose sensitive information or permit unauthorized actions.

The actual cookie value was not reproduced in this report to avoid exposing potentially sensitive session or client information.

### Evidence – Figure 4

**Insert Curl HTTP header screenshot below.**

![Figure 4 – Curl HTTP Response Headers](assets/curl.png)

---

## 5.6 TASK 5 – WEB APPLICATION FIREWALL DETECTION

### Command Executed

```bash
wafw00f https://networkwalks.com
```

### Objective

WAFW00F was used to determine whether the target website is protected by a Web Application Firewall.

### Findings

The tool returned the following result:

| Attribute | Result |
|---|---|
| Tool | WAFW00F |
| Version | 2.4.2 |
| Target | https://networkwalks.com |
| WAF Detected | ModSecurity |
| WAF Provider / Identification | SpiderLabs |
| Number of Requests | 2 |

### Analysis

The WAFW00F scan identified ModSecurity (SpiderLabs) as the Web Application Firewall protecting the target website.

A Web Application Firewall helps monitor and filter HTTP requests that may contain malicious activity, such as common web application attacks.

The presence of a WAF is a useful security measure because it can provide an additional layer of protection between incoming web traffic and the web application.

However, detecting a WAF does not confirm that the website is completely protected against attacks. Additional security testing would be required to evaluate the effectiveness of the WAF and the overall security of the application.

### Evidence – Figure 5

**Insert WAFW00F screenshot below.**

![Figure 5 – WAFW00F Detection Results](assets/wafw00f.png)

---

## 5.7 TASK 6 – DNS ENUMERATION

### Command Executed

```bash
dnsrecon -d networkwalks.com
```

### Objective

DNSRecon was used to enumerate DNS records associated with the target domain. The purpose was to identify DNS infrastructure, mail servers, name servers, and other publicly available DNS information.

### Findings

The DNSRecon scan reported eight records and returned the following information:

| Record Type | Finding |
|---|---|
| SOA | ns6135.hostgator.com |
| NS | ns6135.hostgator.com |
| NS | ns6136.hostgator.com |
| A | 192.232.216.135 |
| MX | mail.networkwalks.com |
| MX IP | 192.232.216.135 |
| TXT | SPF record identified |
| TXT | Google site verification record identified |
| SRV | cPanel email autodiscovery records identified |

Additional observations:

- The DNS server fingerprint returned BIND version `9.16.23-RH`.
- The SPF record included the authorized sender mechanisms `a`, `mx`, an IP address, and `websitewelcome.com`.
- The SPF record ended with `~all`, which represents a soft-fail policy for senders that do not match the listed mechanisms.
- The SRV records referenced cPanel email autodiscovery infrastructure.
- DNSRecon returned an error indicating that no answer was received for its DNSSEC query.

### Analysis

DNSRecon provided additional information about the domain's DNS infrastructure.

The results identified the domain's Start of Authority record, name servers, mail server, IPv4 address, TXT records, and service records.

The SPF TXT record provides information about which mail servers are authorized to send email on behalf of the domain. The `~all` mechanism indicates a soft-fail policy for other senders.

The SRV records revealed the presence of cPanel email autodiscovery services.

The tool also returned no answer for its DNSSEC query. This observation is consistent with the unsigned DNSSEC status reported by WHOIS.

The BIND version reported by DNSRecon is a tool-generated fingerprint and should not be treated as definitive proof of the exact DNS software version.

The DNS enumeration results provide useful information about the domain's infrastructure and potential areas for further security review.

### Evidence – Figure 6

**Insert DNSRecon screenshot below.**

![Figure 6 – DNSRecon DNS Enumeration](assets/dnsrecon.png)

---

# 6. MODULE 5 – LOCAL NETWORK SCANNING WITH ZENMAP

## 6.1 Introduction

The purpose of this module was to perform network discovery using Zenmap, the graphical user interface for Nmap.

Unlike the domain footprinting activities, which focused on gathering publicly available information about a website, this module involved scanning a local network to identify active devices.

Network discovery is an important part of cybersecurity because it allows security professionals to understand which devices are connected to a network and how those devices are positioned within the network environment.

The scan was intended for my own local network and was not intended to access or disrupt any third-party systems.

---

## 6.2 LOCAL NETWORK CONFIGURATION

### Tool Used

Windows Command Prompt

### Command Executed

```cmd
ipconfig
```

### Objective

The ipconfig command was used to identify the local computer's network configuration.

The information required included:

- IPv4 address.
- Subnet mask.
- Default gateway.
- Active network adapter.

### Findings

| Attribute | Result |
|---|---|
| Active Network Adapter | [Insert adapter name] |
| IPv4 Address | [Insert your IPv4 address] |
| Subnet Mask | [Insert subnet mask] |
| Default Gateway | [Insert default gateway] |
| Network Subnet | [Insert confirmed subnet] |

### Analysis

The `ipconfig` command was used to identify the computer's network configuration before performing the Zenmap scan.

The IPv4 address and subnet mask were used to determine the appropriate local network range for host discovery.

Identifying the correct subnet is important because scanning an incorrect network range may result in incomplete or unauthorized scanning activity.

### Evidence – Figure 7

**Insert Windows Command Prompt screenshot showing ipconfig results below.**

![Figure 7 – Windows IP Configuration](assets/ipconfig.png)

---

## 6.3 ZENMAP HOST DISCOVERY SCAN

### Tool Used

Zenmap (Nmap GUI)

### Objective

Zenmap was used to discover active devices connected to the local network.

The scan was configured to identify hosts that responded to network discovery probes.

### Scan Information

| Attribute | Result |
|---|---|
| Scanning Tool | Zenmap |
| Scan Type | Host Discovery / Ping Scan |
| Target Network | [Insert your confirmed subnet] |
| Scan Profile | [Insert selected Zenmap profile] |
| Scan Command | [Insert actual command displayed by Zenmap] |
| Scan Date | [Insert date] |

### Scan Results

| Attribute | Result |
|---|---|
| Total Live Hosts Discovered | [Insert number] |
| Host 1 IP Address | [Insert IP address] |
| Host 1 MAC Address | [Insert MAC address, if available] |
| Host 2 IP Address | [Insert IP address] |
| Host 2 MAC Address | [Insert MAC address, if available] |
| Host 3 IP Address | [Insert IP address] |
| Host 3 MAC Address | [Insert MAC address, if available] |
| Additional Hosts | [Add rows if required] |

### Analysis

The Zenmap scan was performed to identify active devices within the selected local network range.

The results were reviewed to determine the number of responding hosts and their corresponding IP addresses. MAC address information was also recorded where available.

Host discovery helps provide an overview of the devices that are visible on a network. This information can assist network administrators and cybersecurity professionals in identifying connected devices and understanding the network environment.

It is important to note that a host that does not respond to discovery probes is not necessarily offline. Some devices may block or restrict the probes used during a ping scan.

The results of this scan represent the devices that responded to the discovery activity at the time of testing.

### Evidence – Figure 8

**Insert Zenmap scan results screenshot below.**

![Figure 8 – Zenmap Host Discovery Results](assets/zenmap-scan.png)

---

## 6.4 NETWORK TOPOLOGY MAPPING

### Objective

The Zenmap Topology feature was used to generate a graphical representation of the discovered network hosts.

The topology view provides a visual overview of the scanning computer and the devices identified during the network discovery process.

### Topology Findings

| Attribute | Result |
|---|---|
| Network Scanned | [Insert confirmed subnet] |
| Total Hosts Displayed | [Insert number] |
| Scanning Computer | [Insert scanning computer IP or hostname] |
| Other Discovered Devices | [Insert discovered IP addresses] |
| Topology Export Format | PDF |
| Export Status | [Insert status after saving] |

### Analysis

The Zenmap Topology view provided a graphical representation of the network discovery results.

The diagram helped visualize the relationship between the scanning computer and the hosts identified during the scan.

This type of visualization is useful because it makes network discovery results easier to interpret than a list of IP addresses alone.

The topology diagram was exported to PDF format for documentation and evidence.

The diagram represents the results of the host discovery scan and should not be interpreted as a complete physical network diagram or a detailed map of every network connection.

### Evidence – Figure 9

**Insert Zenmap Topology screenshot below.**

![Figure 9 – Zenmap Network Topology](assets/zenmap-topology.png)

### Exported Topology PDF

**Insert the exported topology PDF in the repository's evidence folder.**

Suggested file location:

`assets/zenmap-topology.pdf`

---

# 7. CONSOLIDATED FINDINGS AND RISK ANALYSIS

The following table summarizes the main observations from the domain footprinting and network scanning activities.

| No. | Finding | Observation | Security Consideration |
|---|---|---|---|
| 1 | Domain Registration | GoDaddy registrar identified. | Registration information provides useful domain intelligence. |
| 2 | Registrant Privacy | Registrant details protected by Domains By Proxy. | Privacy protection reduces public exposure of registration details. |
| 3 | DNSSEC | WHOIS reported DNSSEC unsigned. | DNS responses do not benefit from DNSSEC signature validation. |
| 4 | Web Technologies | Apache and WordPress identified. | Software components should be kept updated and reviewed for known vulnerabilities. |
| 5 | Website Redirect | HTTP redirects to HTTPS. | HTTPS helps protect information transmitted between users and the website. |
| 6 | HTTP Headers | Security-related headers identified. | Header configurations should be reviewed to ensure appropriate browser protections. |
| 7 | Web Application Firewall | ModSecurity detected. | WAF provides an additional layer of web application protection. |
| 8 | DNS Records | SOA, NS, A, MX, TXT and SRV records identified. | DNS information can reveal infrastructure details useful for security assessments. |
| 9 | Local Network | Local network configuration identified using ipconfig. | Accurate network identification is necessary before scanning. |
| 10 | Live Hosts | [Insert Zenmap host count]. | Identifies devices responding to network discovery probes. |
| 11 | Network Topology | [Insert topology observation]. | Provides a visual overview of discovered network hosts. |

### Risk Assessment Notes

The observations in this report are reconnaissance findings and do not independently establish that a vulnerability exists.

The DNSSEC unsigned status is a configuration consideration that should be reviewed. The presence of WordPress and other identified technologies also warrants routine version verification and security maintenance.

The detection of ModSecurity is a positive observation, but it does not guarantee that all web application attacks will be blocked.

No exploitation or vulnerability validation was performed as part of these activities.

---

# 8. RECOMMENDATIONS

Based on the observations collected during the practical exercise, the following recommendations are provided:

### 8.1 Domain and DNS Security

- Consider enabling DNSSEC to provide DNS response validation.
- Regularly review domain registration and DNS configurations.
- Ensure that DNS records are accurate and only necessary services are exposed.
- Review SPF, DKIM, and DMARC configurations to strengthen email authentication.

### 8.2 Website and Application Security

- Keep WordPress, plugins, themes, and server software updated.
- Regularly review third-party plugins for security advisories.
- Review HTTP security headers and implement additional protections where appropriate.
- Ensure that HTTPS is enforced across the website.
- Regularly review publicly accessible API endpoints.
- Maintain and properly configure the Web Application Firewall.

### 8.3 Local Network Security

- Maintain an inventory of authorized devices connected to the local network.
- Use strong passwords for network equipment and connected devices.
- Disable unnecessary network services.
- Regularly review connected devices and investigate unknown hosts.
- Keep routers, computers, and other network devices updated.
- Restrict access to network management interfaces.

---

# 9. LIMITATIONS OF THE ASSESSMENT

This exercise was limited to domain footprinting and local network host discovery.

The following limitations should be considered:

- WHOIS information depends on the data made available by the registrar and registry.
- WhatWeb identifies technologies based on observable website responses; detected versions may require independent verification.
- DNS lookup results may vary depending on the resolver and DNS configuration.
- HTTP headers provide useful information but do not represent a complete security assessment.
- WAFW00F detection does not confirm the effectiveness of the detected firewall.
- DNSRecon findings depend on the DNS records visible during the enumeration process.
- Zenmap host discovery identifies hosts that respond to the selected probes. Devices that block discovery traffic may not appear.
- The topology diagram represents the discovery results and does not necessarily show every physical or logical network connection.
- No exploitation, password testing, or detailed vulnerability assessment was performed.

---

# 10. CONCLUSION

The Week 2 practical exercise provided an opportunity to apply fundamental cybersecurity reconnaissance and network discovery techniques using Kali Linux and Zenmap.

During the domain footprinting module, six Kali Linux tools were used to gather information about `networkwalks.com`. The WHOIS lookup provided domain registration details, WhatWeb identified the website's technologies, Nslookup resolved the domain to its IP address, Curl examined HTTP response headers, WAFW00F detected ModSecurity protection, and DNSRecon enumerated additional DNS records.

The results demonstrated how much information can be collected about a website through reconnaissance without attempting to exploit the target.

The Zenmap module focused on identifying devices connected to my local network. By using Windows Command Prompt and Zenmap, the objective was to identify the local network configuration, discover responding hosts, record available IP and MAC addresses, and generate a network topology diagram.

Overall, the exercise strengthened my understanding of the reconnaissance process and the importance of network visibility in cybersecurity.

It also reinforced the importance of conducting security assessments responsibly, documenting findings accurately, and ensuring that all scanning activities remain within an authorized scope.

---

# 11. EVIDENCE AND SCREENSHOT DIRECTORY

The following screenshots and files are included as supporting evidence for this practical exercise.

| Figure | Evidence Description | Suggested Filename |
|---|---|---|
| Figure 1 | WHOIS domain registration results | whois.png |
| Figure 2 | WhatWeb technology fingerprinting | whatweb.png |
| Figure 3 | Nslookup DNS resolution | nslookup.png |
| Figure 4 | Curl HTTP response headers | curl.png |
| Figure 5 | WAFW00F detection results | wafw00f.png |
| Figure 6 | DNSRecon DNS enumeration | dnsrecon.png |
| Figure 7 | Windows ipconfig results | ipconfig.png |
| Figure 8 | Zenmap host discovery scan | zenmap-scan.png |
| Figure 9 | Zenmap network topology | zenmap-topology.png |
| Appendix | Exported Zenmap topology | zenmap-topology.pdf |

---

# 12. REPOSITORY STRUCTURE

The GitHub repository should be organized as follows:

```text
week2-footprinting-network-scanning/
│
├── README.md
│
└── assets/
    ├── whois.png
    ├── whatweb.png
    ├── nslookup.png
    ├── curl.png
    ├── wafw00f.png
    ├── dnsrecon.png
    ├── ipconfig.png
    ├── zenmap-scan.png
    ├── zenmap-topology.png
    └── zenmap-topology.pdf
```

---

# END OF REPORT

**Prepared as part of the Networkwalks Cybersecurity and Penetration Testing Program.**

*Week 2 – Domain Footprinting and Network Scanning*
