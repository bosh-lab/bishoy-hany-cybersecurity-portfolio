# 🛡️ IBM QRadar SIEM — Custom Configs & Automation

A practical IBM QRadar SIEM project that includes custom action scripts, threat intelligence configurations, network hierarchy templates, and remote automation tools for SOC environments.

---

## 🛠️ Tools & Technologies
- IBM QRadar SIEM
- Python 3 (QRadar REST API)
- Bash / cURL (Custom Action Scripts)
- Twilio API (SMS Alerting)
- JSON / XML (Configuration files)

---

## 📁 Project Structure

```
qradar/
├── action_scripts/
│   └── sms.sh                    # Send SMS alerts via Twilio API
├── configs/
│   ├── arielRightClick.properties  # Threat intel right-click menu (12 sources)
│   ├── ip_context_menu.xml         # IP context menu (21 threat intel sources)
│   └── network_hierarchy.json      # Starter network hierarchy template
├── reference_sets/
│   └── cobaltstrike_ua.csv         # CobaltStrike user-agent reference set
└── remote_automation/
    └── qradar_check.py             # Python script for QRadar health status report
```

---

## 🔧 What's Inside

### 1. SMS Alert Script (`action_scripts/sms.sh`)
- Sends automated **SMS text alerts** directly from QRadar using the **Twilio API**
- Triggered via QRadar's **Custom Actions** feature
- Useful for high-severity offense notifications to on-call analysts

**Setup:**
1. Create a [Twilio](https://www.twilio.com) account and get your phone number, Account SID, and Auth Token
2. Add your credentials into `sms.sh`
3. In QRadar → Admin → Custom Actions → Define Actions → Upload the script

---

### 2. Threat Intelligence Right-Click Menus (`configs/`)

**arielRightClick.properties** — Adds 12 threat intel sources to the Ariel right-click menu:
> Bluecoat, Cisco Talos, DomainTools, Google Cached View, LOLBAS, Maclookup, Robtex, SpeedGuide, ThreatCrowd, URLVoid, Userstack, VeriSign

**ip_context_menu.xml** — Adds 21 threat intel sources to the IP right-click menu:
> Nmap, Ping, Traceroute, X-Force Exchange, AbuseIPDB, AlienVault OTX, Censys, Cisco Talos, DNSlytics, DShield, Google Safe Browsing, GreyNoise, IPVoid, MxToolBox, Project Honey Pot, Robtex, Shodan, Spamhaus, ThreatCrowd, ThreatMiner, VirusTotal

**To install:** Copy files to `/opt/qradar/conf/` and restart Tomcat

---

### 3. Network Hierarchy Template (`configs/network_hierarchy.json`)
- Starter template for QRadar's network hierarchy
- Includes Loopback, Multicast, and Unicast address methods (IPv4 & IPv6)
- Ready to customize with your own network subnets and geo coordinates

---

### 4. CobaltStrike Reference Set (`reference_sets/cobaltstrike_ua.csv`)
- A reference set of known **CobaltStrike user-agent strings**
- Import into QRadar to detect CobaltStrike beacons in network traffic
- Use with custom rules to trigger offenses on matching user agents

---

### 5. QRadar Health Check Script (`remote_automation/qradar_check.py`)
- Python script that queries **12 QRadar REST API endpoints**
- Collects: system info, users, licenses, log sources, backups, disaster recovery config, security data count, and more
- Generates a clean **HTML status report** for your QRadar deployment

**Endpoints queried:**
- `/api/system/about`
- `/api/usermanagement/users`
- `/api/system/notifications`
- `/api/config/deployment/licenses`
- `/api/config/event_retention_buckets`
- `/api/config/backup_and_restore/scheduled_backup_configurations`
- `/api/configuration/log_sources`
- `/api/health_data/security_data_count`
- and more...

**To run:**
```bash
pip install requests
# Edit qradar_check.py — add your QRadar IP and API token
python qradar_check.py
# Opens qradar_report.html with full status report
```

---

## 🎯 Skills Demonstrated
- IBM QRadar SIEM administration and customization
- Integrating third-party threat intelligence sources into SIEM workflows
- Writing automation scripts using QRadar REST API (Python)
- Building custom alerting pipelines (SMS via Twilio)
- Detecting known threat tools (CobaltStrike) using reference sets

---

## 👤 Author
**Bishoy Hany** — Aspiring SOC Analyst | Blue Team Enthusiast

🔗 [LinkedIn](https://www.linkedin.com/in/bishoy-hany-519baa373/) | 🎮 [TryHackMe](https://tryhackme.com/p/hanybishoy440) | 💼 [Portfolio](https://github.com/bosh-lab/bishoy-hany-cybersecurity-portfolio)
