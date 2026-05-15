DNS Log Analysis Using Splunk SIEM

Objective

This project focuses on analyzing DNS logs using Splunk SIEM to identify suspicious network activity, failed DNS requests, and abnormal traffic patterns. The project demonstrates basic SOC investigation and threat hunting techniques using DNS data.

---

Tools Used

- Splunk Enterprise
- Windows
- DNS Logs
- Git Bash
- GitHub

---

Dataset Information

The dataset contains DNS traffic logs including source IP addresses, destination IPs, DNS query types, NXDOMAIN responses, and refused DNS requests.

---

Queries Used

1. Top Queried Domains

index=main sourcetype="dns:log"
| stats count by domain
| sort - count

Explanation

This query identifies the most frequently requested domains in the environment.

Screenshot

Screenshot here:
soc-dns-analysis-project/screenshots/top-domains.png

---

2. Most Active Source IP Addresses

index=main sourcetype="dns:log"
| stats count by src_ip
| sort - count

Explanation

This query identifies systems generating the highest DNS traffic in the network.

Screenshot

Screenshot here:
soc-dns-analysis-project/screenshots/most-active-source-ips.png

---

3. NXDOMAIN Detection

index=main NXDOMAIN
| stats count by src_ip
| sort - count

Explanation

This query detects systems generating failed DNS requests (NXDOMAIN responses), which may indicate suspicious or malicious activity.

Screenshot

Screenshot here:
soc-dns-analysis-project/screenshots/nxdomain-analysis.png

---

4. REFUSED DNS Requests

index=main REFUSED
| stats count by src_ip

Explanation

This query identifies refused DNS requests that may indicate unauthorized or abnormal DNS activity.

Screenshot

Screenshot here:
soc-dns-analysis-project/screenshots/refused-analysis.png

---

5. Long Domain Detection

index=main
| where len(domain) > 40
| table _time src_ip domain

Explanation

This query detects unusually long domain names that may indicate DNS tunneling or suspicious communication.

Screenshot

Screenshot here:
soc-dns-analysis-project/screenshots/long-domain-detection.png

---

Findings

- Multiple NXDOMAIN responses were detected
- Several source IPs generated high DNS traffic
- Refused DNS requests were identified
- Long domain queries indicated potentially suspicious behavior
- DNS traffic patterns were successfully analyzed using Splunk SIEM

---

Detection Logic

- High NXDOMAIN traffic may indicate malware using Domain Generation Algorithms (DGA)
- Excessive DNS requests from one host may indicate beaconing activity
- Long domain names may suggest DNS tunneling attempts
- REFUSED responses may indicate unauthorized DNS activity

---

Skills Demonstrated

- Splunk SIEM
- DNS Log Analysis
- Threat Hunting
- Basic SOC Investigation
- Security Monitoring
- Query Writing
- Incident Analysis

---

Future Improvements

- Create Splunk dashboards
- Add automated alerting
- Analyze HTTP and firewall logs
- Detect DNS tunneling automatically
- Integrate additional log sources

---

Conclusion

This project demonstrates practical SOC analysis skills using Splunk SIEM and DNS logs. The investigation process included detecting suspicious DNS activity, analyzing network behavior, and identifying potentially malicious indicators using SIEM queries and log analysis techniques.
