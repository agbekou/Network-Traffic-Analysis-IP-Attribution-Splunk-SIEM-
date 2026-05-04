# Network-Traffic-Analysis-IP-Attribution-Splunk-SIEM-

# Project Objective
The core goal of this project was to perform Statistical Analysis and Threat Triage on network traffic logs within Splunk. By identifying "Top Talkers" (high-volume connections), the objective was to validate the legitimacy of external communications and detect potential Command and Control (C2) or data exfiltration attempts through manual reputation cross-referencing.

# Skills Learned
•	SIEM Data Aggregation: Utilizing Splunk’s Search Processing Language (SPL) to summarize large datasets.
•	Statistical Baseline Analysis: Identifying outliers in network traffic through volume-based sorting.
•	OSINT Integration: Leveraging external threat intelligence tools (IPinfo, VirusTotal) for forensic validation.
•	Traffic Attribution: Mapping internal network flows to external geographical origins.
Tools Used
•	Splunk Enterprise / Splunk Cloud: For log indexing and search.
•	SPL (Search Processing Language): Specifically the stats and sort commands.
•	IPinfo: For geolocation and ASN (Autonomous System Number) lookup.
•	VirusTotal: For malware and malicious reputation scanning.

# Steps Taken
## 1. Data Aggregation via SPL
I targeted the main index to isolate network traffic logs. Using the stats count command, I aggregated the data to show the frequency of connections between specific Source IPs (src_ip) and Destination IPs (dest_ip).
Code snippet
index=main 
| stats count by src_ip, dest_ip 
| sort - count
## 2. Identifying "Top Talkers"
By sorting the results in descending order, I isolated the highest volume of traffic. High-frequency connections are often legitimate (e.g., cloud updates, backups), but they can also hide beaconing activity or massive data transfers.
## 3. External Geographic Attribution
I selected the top-volume external IPs and utilized IPinfo to determine their geographical origin. This step ensures that the physical location of the traffic aligns with the organization's expected business operations (e.g., identifying why a domestic server is sending high-volume traffic to a foreign data center).
## 4. Threat Reputation Cross-Referencing
To ensure the "Top Talkers" were benign, I cross-referenced the IPs with VirusTotal. I checked for:
•	Positive malware detections.
•	Historical association with known botnets or phishing campaigns.
•	Previous reports from the security community.
## 5. Disposition and Documentation
I documented the findings to establish a baseline for "known good" traffic. This workflow ensures that any future deviations from this baseline can be flagged as high-priority anomalies, allowing for faster incident response.
Final Takeaway: Effective threat hunting is about more than just finding "bad" IPs; it's about understanding the volume and context of your network's communication to ensure your defensive perimeter is holding.



