# FortiGate Firewall & Security Profiles Lab

## 1. Project Overview
This project documents a hands-on lab where I configured a **FortiGate next-generation firewall (NGFW)** to control and inspect traffic between an internal LAN and the WAN. The goal was to build practical, job-ready skills in firewall policy creation, NAT, and layered traffic inspection using FortiGate security profiles — the kind of work a SOC/Network Security analyst does day to day.

## 2. Lab Objectives
- Configure a firewall policy to allow controlled LAN-to-WAN traffic
- Enable NAT so internal hosts can reach external networks
- Apply and test multiple security profiles (AntiVirus, Web Filter, DNS Filter, Application Control, IPS, File Filter, SSL/SSH Inspection)
- Validate connectivity and policy behavior using a Windows client

## 3. Lab Environment
| Component | Details |
|---|---|
| Firewall | FortiGate VM64, firmware v7.6.7 |
| Client | Windows (Command Prompt / ping used for testing) |
| Interfaces | LAN (port2), WAN (port1), DMZ (port3) |
| Access Method | FortiGate Web GUI |

## 4. Network Topology
```
[ Windows Client ] --- LAN (192.168.2.1/24, port2) --- [ FortiGate FW1 ] --- WAN (90.1.1.129/24, port1) --- [ Internet ]
                                                              |
                                                        DMZ (192.168.3.1/24, port3)
```

## 5. FortiGate Configuration
- Accessed the FortiGate GUI (Network > Interfaces) and reviewed all interface IP configurations
- Confirmed **LAN** (port2, 192.168.2.1/24, DHCP range 192.168.2.50-200), **WAN** (port1, 90.1.1.129/24), and **DMZ** (port3, 192.168.3.1/24)

## 6. Firewall Policies
- Created a policy named **LAN to WAN** (Policy ID 1)
- Incoming interface: **LAN (port2)**
- Outgoing interface: **WAN (port1)**
- Source: PC1, users group
- Destination: all
- Service: **ALL**
- Action: **ACCEPT**
- Inspection mode: **Flow-based**
- **NAT**: Enabled - Use Outgoing Interface Address, source port translation "When port conflicts"
- Logging: Log allowed traffic set to Security events

See `configurations/firewall-configuration.txt` for the full policy breakdown.

## 7. Security Profiles
Applied and tested the following custom profiles on top of the firewall policy:

- **AntiVirus** (`custom-antivirus`) - flow-based scanning across HTTP, SMTP, POP3, IMAP, FTP, CIFS; mobile malware protection enabled
- **Web Filter** (`custom-webfilter`) - FortiGuard category-based filtering (Potentially Liable categories set to Monitor), Safe Search enforced, YouTube access restricted to Moderate
- **DNS Filter** (`custom-dnsfilter`) - FortiGuard category-based DNS filtering, botnet C&C redirection to block portal, Safe Search enforced
- **Application Control** (`custom-appcontrol`) - category-based sensor covering all major app categories, with an override blocking the Facebook application
- **IPS** (`custom-ips`) - custom sensor covering server/client signatures across severity levels
- **File Filter** (`custom-filefilter`) - custom rule matching HTTP/FTP (and other) protocols, matching file types including 7z and bat, action set to Monitor
- **SSL/SSH Inspection** (`custom-deep-inspection`) - deep inspection profile with trusted-site exemptions (Finance and Banking, Health and Wellness categories, plus named services like Google, Microsoft, Apple, Dropbox) and Block action on expired, revoked, and validation-failed certificates

## 8. Testing & Validation
- Used Windows Command Prompt (`ping`) to confirm LAN-to-WAN connectivity after policy creation
- Verified that traffic matched the intended policy and security profiles

### Configured vs. Tested vs. Observed
To keep this an honest, recruiter-credible record of what was actually done:

| Area | Configured | Tested | Observed |
|---|---|---|---|
| LAN-to-WAN firewall policy (NAT, ACCEPT) | ✅ | ✅ (ping through the policy) | ✅ (hit count / bandwidth in GUI) |
| AntiVirus profile | ✅ | ❌ not tested with a live malware sample | — |
| Web Filter profile | ✅ | ❌ not tested against a live blocked category | — |
| DNS Filter profile | ✅ | ❌ not tested against a live blocked domain | — |
| Application Control (Facebook block) | ✅ | ❌ not tested by attempting Facebook access | — |
| IPS sensor | ✅ | ❌ not tested against a live attack signature | — |
| File Filter profile | ✅ | ❌ not tested with a live matching file transfer | — |
| SSL/SSH Inspection profile | ✅ | ❌ not tested against a live cert scenario | — |

In short: every security profile was **configured and attached to the policy**, and the base LAN-to-WAN connectivity was **tested and confirmed**. The individual security profiles themselves were not each put through a live pass/fail test in this session — that would be a good next step for this lab (e.g., trying to reach a blocked web category, attempting to download an EICAR test file, etc.).

## 9. Logs & Monitoring
- Reviewed FortiGate policy statistics (hit count, active sessions, total bytes) to confirm the policy was actively matching and processing traffic

## 10. Screenshots
See the `/screenshots` folder:
- `01-network-interfaces.jpeg` - LAN/WAN/DMZ interface configuration
- `02-firewall-policy-lan-to-wan.jpeg` - LAN to WAN policy (source, destination, NAT)
- `03-firewall-policy-security-profiles.jpeg` - security profiles attached to the policy
- `04-antivirus-profile.jpeg` - AntiVirus profile
- `05-web-filter-profile-1.jpeg` / `06-web-filter-profile-2.jpeg` - Web Filter profile
- `07-dns-filter-profile-1.jpeg` / `08-dns-filter-profile-2.jpeg` - DNS Filter profile
- `09-application-control-sensor.jpeg` - Application Control sensor
- `10-ips-sensor.jpeg` - IPS sensor
- `11-file-filter-profile.jpeg` - File Filter profile
- `12-ssl-ssh-inspection-1.jpeg` / `13-ssl-ssh-inspection-2.jpeg` - SSL/SSH Inspection profile

## 11. What I Learned
- How a firewall evaluates and enforces traffic rules between network zones
- How NAT allows internal clients to reach external networks
- How security profiles add layered inspection beyond simple allow/deny rules
- How SSL/SSH deep inspection and certificate validation settings affect encrypted traffic
- How to validate firewall behavior with real connectivity tests and policy statistics

## 12. Skills Demonstrated
`Network Security` - `FortiGate` - `Firewall Policy Configuration` - `NAT` - `AntiVirus` - `Web Filtering` - `DNS Filtering` - `Application Control` - `IPS` - `File Filtering` - `SSL/SSH Inspection` - `Traffic Inspection & Log Analysis`

---
Full write-up: [`reports/FortiGate-Lab-Report.txt`](reports/FortiGate-Lab-Report.txt)
