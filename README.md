# WEEK 2 – PENETRATION TESTING REPORT
## Footprinting, Reconnaissance & Network Scanning

**Prepared By:** Muhammad Haris  
**Platform:** Kali Linux  
**Assessment Target:** networkwalks.com  
**Week:** 02  
**Assessment Category:** Information Gathering & Network Scanning

---

# 1. Liability Disclaimer

This report has been prepared for educational and cybersecurity training purposes as part of a Week 2 penetration testing internship assignment.

The activities documented in this report focus on footprinting, reconnaissance, DNS information gathering, web technology identification, and network scanning.

The findings represent observations collected during the assessment and should not be interpreted as confirmation of exploitable vulnerabilities.

Any testing against systems must be conducted with appropriate authorization from the system owner. The author accepts no responsibility for unauthorized use of the techniques described in this report.

# 2. Introduction

Footprinting and reconnaissance are important initial phases of penetration testing. These activities help security professionals collect publicly available information about a target before performing deeper security assessments.

During Week 2 of the cybersecurity internship, I performed footprinting and reconnaissance activities using multiple tools available in Kali Linux.

The primary objective was to understand how information about a website and its infrastructure can be collected through different reconnaissance techniques.

The assessment focused on the domain networkwalks.com.

The activities included domain registration information gathering, web technology identification, DNS resolution, HTTP response analysis, Web Application Firewall detection, and DNS record enumeration.

Additionally, Zenmap-based network scanning is a required part of this week's assignment and is documented separately below.

# 3. Tools Used

The following tools were selected for the assessment:

| Tool | Purpose |
|---|---|
| WHOIS | Collect domain registration information. |
| WhatWeb | Identify website technologies and server information. |
| Nslookup | Resolve domain names into IP addresses. |
| cURL | Examine HTTP response headers. |
| WAFW00F | Identify Web Application Firewall technology. |
| DNSRecon | Enumerate DNS records and infrastructure information. |
| Zenmap | Graphical interface for network scanning using Nmap. |

**Operating System:** Kali Linux

# 4. Activities Performed

## 4.1 Footprinting & Reconnaissance

### Activity 1: WHOIS Information Gathering

**Tool:** WHOIS

WHOIS was used to collect publicly available registration information about the target domain.

Command:

`whois networkwalks.com`

**Observations:**

- Domain Name: networkwalks.com
- Registrar: GoDaddy.com, LLC
- Creation Date: November 6, 2019
- Expiration Date: November 6, 2027
- Name Servers: NS6135.HOSTGATOR.COM and NS6136.HOSTGATOR.COM
- DNSSEC: Unsigned
- Registrant Information: Privacy protected.

**Result:**

The WHOIS lookup successfully retrieved domain registration details, registrar information, name servers, and domain status.

### Activity 2: Website Technology Identification

**Tool:** WhatWeb

WhatWeb was used to identify the technologies and server information associated with the target website.

Command:

`whatweb networkwalks.com`

**Observations:**

- Web Server: Apache
- Content Management System: WordPress
- WordPress Version Detected: 7.1.4
- Bootstrap: 7.1.4
- jQuery: 3.7.1
- Website Title: Networkwalks Academy
- Country Identification: United States
- Website IP: 192.232.216.135
- HTTPS: Supported
- Email Information: info@networkwalks.com

**Result:**

The tool successfully identified several technologies used by the website, including Apache and WordPress.

### Activity 3: DNS Resolution

**Tool:** Nslookup

Nslookup was used to resolve the target domain into its corresponding IP address.

Command:

`nslookup networkwalks.com`

**Observations:**

- DNS Server: 8.8.8.8
- Domain: networkwalks.com
- Resolved IP Address: 192.232.216.135

**Result:**

The DNS lookup successfully resolved the domain name to its associated IP address.

### Activity 4: HTTP Header Analysis

**Tool:** cURL

cURL was used to examine the HTTP response headers returned by the target website.

Command:

`curl -I https://networkwalks.com`

**Observations:**

- HTTP Response: 200 OK
- Server: Apache
- Content-Type: text/html; charset=UTF-8
- HTTPS Connection: Active
- WordPress REST API reference identified in response headers.
- Cookie information was also observed.

**Result:**

The server successfully returned an HTTP 200 response, indicating that the requested webpage was accessible.

### Activity 5: Web Application Firewall Detection

**Tool:** WAFW00F

WAFW00F was used to identify whether a Web Application Firewall was detected in front of the target website.

Command:

`wafw00f networkwalks.com`

**Observations:**

- WAF Detection: Successful
- Identified WAF: ModSecurity (SpiderLabs)
- Number of Requests: 2

**Result:**

The tool identified ModSecurity as the Web Application Firewall protecting the website.

This indicates that a web application protection mechanism is present.

### Activity 6: DNS Enumeration

**Tool:** DNSRecon

DNSRecon was used to collect additional DNS information associated with the target domain.

Command:

`dnsrecon -d networkwalks.com`

**Observations:**

The following information was identified:

- SOA Record
- Name Server Records
- Mail Exchange Record
- A Record
- TXT Records
- SPF Information
- SRV Records
- DNS Server Information

The enumeration identified eight SRV records.

The DNSSEC query also returned an error indicating that no answer was received for the DNSSEC query.

**Result:**

DNSRecon successfully collected several DNS records and provided additional information about the target's DNS infrastructure.

## 4.2 Network Scanning with Zenmap

**Tool:** Zenmap

Zenmap is the graphical interface for Nmap and is commonly used for network discovery and security assessment.

The purpose of this module is to understand network scanning, identify accessible hosts, and observe network services.

**Required Activities:**

- Open Zenmap in Kali Linux.
- Select an authorized scanning target.
- Perform an appropriate network discovery scan.
- Review the scan results.
- Document discovered hosts, open ports, and detected services where available.

**Assessment Status:**

Zenmap scan output and screenshots were not included in the supplied evidence. Therefore, actual network scanning findings cannot be confirmed in this report.

**Note:** Add the actual Zenmap scan results and screenshots before submitting the final report.

# 5. Risk Analysis / Impact

Based on the footprinting activities, the following observations were identified:

| Observation | Potential Impact | Priority |
|---|---|---|
| Public WHOIS information | Provides domain registration and infrastructure details. | Informational |
| Technology identification | May help attackers identify software and potential outdated components. | Low |
| Public DNS records | Exposes information about domain infrastructure. | Informational |
| HTTP response headers | May disclose server and application information. | Low |
| WAF detection | Reveals the presence and type of web protection technology. | Informational |
| DNSSEC unsigned status | DNS responses lack DNSSEC-based authenticity validation. | Review recommended |

These observations do not independently confirm exploitable vulnerabilities.

The main security consideration is the amount of publicly available information that can assist an attacker during the reconnaissance phase.

# 6. Recommendations

Based on the observations, the following security recommendations are suggested:

1. **Protect Domain Information:** Review publicly exposed domain registration information and maintain appropriate privacy protection.

2. **Update Software:** Keep WordPress, plugins, themes, and server software updated to supported and secure versions.

3. **Secure DNS Configuration:** Review DNS configuration and evaluate the implementation of DNSSEC where appropriate.

4. **Review HTTP Headers:** Configure appropriate security headers to improve browser-side protection.

5. **Maintain WAF Protection:** Keep ModSecurity rules updated and regularly review security events.

6. **Monitor DNS Records:** Regularly review DNS records to identify unexpected or unauthorized changes.

7. **Perform Regular Security Assessments:** Conduct authorized vulnerability assessments and network security reviews.

# 7. Conclusion

During Week 2 of the cybersecurity internship, I performed several footprinting and reconnaissance activities using Kali Linux.

I successfully used six different tools: WHOIS, WhatWeb, Nslookup, cURL, WAFW00F, and DNSRecon.

These activities helped me understand how domain registration details, DNS records, website technologies, HTTP headers, and Web Application Firewall information can be collected during the reconnaissance phase.

I also learned the importance of identifying publicly exposed information and understanding its potential security impact.

Zenmap-based network scanning is included as a required module, but its findings still need to be added using actual scan evidence.

Overall, this week's activities improved my practical understanding of information gathering, footprinting, reconnaissance, and the initial stages of penetration testing.

**End of Report**

👤 Author
Muhammad Haris
Cybersecurity Professional B082


📌 Project Information
Program Name: Cybersecurity program at Networkwalks | Week: 02 | Repository: GitHub

