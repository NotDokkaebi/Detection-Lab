<h1>Honeypot / Local Detection Lab (OpenCanary + Splunk)</h1>

<p>
<b>Detection Lab Project</b> to simulate real-world attacker behavior using a honeypot installed on a Linux Ubuntu Server version 25.10, outputting information through rsyslog as well as a local Windows 11 machine outputting information through syslog to analyze information in Splunk.
</p>

<hr>

<h2>Project Overview</h2>

<ul>
  <li>Set up and deployed a Kali Linux machine to perform attacks from</li>
  <li>Set up and deployed a Windows 11 machine to act as a target, but also to ingest and feed info to Splunk</li>
  <li>Installed Syslog and created basic configuration to feed events into Windows Event Viewer</li>
  <li>Splunk Universal Forwarder to ingest Windows Event Logs (Security, System, Application) into SIEM for detection and analysis</li>  
  <li>Set up and configured a Linux Ubuntu Server running version 25.10 to host a honeypot</li>
  <li>SSH'd into Ubuntu Server from Kali Linux machine to install OpenCanary Honeypot</li>
  <li>Configured honeypot services (SSH, FTP, HTTP) on common attack ports (2222, 21, 8080) to capture brute force and reconnaissance activity</li>
  <li>Deployed a honeypot to capture attacker activity</li>
  <li>Forwarded logs using rsyslog into Splunk using UDP connection over port 514</li>
  <li>Ingested data into Splunk SIEM</li>
  <li>Built detections and alerts along with a basic dashboard</li>
</ul>

<hr>

<h2>Architecture</h2>


```mermaid
flowchart TD

A[Kali Linux\n192.168.64.2] -->|Attack Traffic| B[OpenCanary Honeypot\n192.168.64.4]
A -->|Attack Traffic| F[Windows 11 Machine\n192.168.64.3]

subgraph Linux Ubuntu Honeypot
B --> C[/var/tmp/opencanary.log/]
C --> D[rsyslog]
end

D -->|Syslog UDP 514| E[Splunk SIEM\n192.168.64.3]

subgraph Windows Host
F --> G[Event Viewer Logs]
end

G -->|Splunk Forwarder| E
```


<hr>

<h2>Detection Capabilities</h2>

<ul>
  <li>SSH brute force detection</li>
  <li>Port scanning detection</li>
  <li>GeoIP attack mapping</li>
  <li>Connection tracking by port</li>
</ul>

<hr>

<h2>Screenshots</h2>

<p><i>(Add your screenshots here)</i></p>

<h3>Splunk Dashboard and Alerts</h3>
<li>Custom Alerts for unusual port activity</li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/dd87f8894005af458a3e06d9f7e3a55a3efb2832/Splunk%20alerts.png" width="600"/>
<li>Dashboard showing basic Splunk dashboards, including HoneyPot logs</li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/c0b758b015a47d5d0e1dcd4e2427fc01168bb773/Splunk%20dashboard%20with%20honeypot%20logs.png" width="600"/>

<h3>OpenCanary</h3>
<li>OpenCanary startup interface showing ports used in HoneyPot</li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/dd87f8894005af458a3e06d9f7e3a55a3efb2832/OpenCanary%20interface.png" width="600"/>
<li>Logs accessed from Kali machine using SSH, showing brute force login attempts</li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/dd87f8894005af458a3e06d9f7e3a55a3efb2832/Opencanary%20honeypot%20logs.png" width="600"/>
<li>HoneyPot logs aggregating from rsyslogs into Splunk through UDP port 514</li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/c5593ce7d15f478ade767a4e4b3231467f056959/Honeypot%20logs%20agrigating%20into%20splunk.png" width="600"/>

<h3>Configurations</h3>
<li>Custom Sysmon configuration</li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/dd87f8894005af458a3e06d9f7e3a55a3efb2832/UpdatedSysmonconfig.png" width="600"/>
<li>Simple OpenCanary configuration</li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/ad1b0f518ebd1e7ffdbbf9592ec4c85c4e532dc8/Simple%20Opencanary%20Configuration.png" width="600"/>

<h3>Attack Logs</h3>
<li>Splunk logs showing unauthorized user creation </li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/dd87f8894005af458a3e06d9f7e3a55a3efb2832/splunk%20user%20add%20events.png"/>
<li>Splunk logs showing reverse shell attack over port 4444 on Windows machine </li>
<img src="https://github.com/NotDokkaebi/Detection-Lab/blob/dd87f8894005af458a3e06d9f7e3a55a3efb2832/Splunk%20Capture%20of%20shell%20event.png"/>

<hr>

<h2>Resume Highlights</h2>

<ul>
  <li>Built and deployed a <b>honeypot-based detection lab</b> using OpenCanary</li>
  <li>Engineered a <b>log pipeline</b> using rsyslog into Splunk SIEM</li>
  <li>Developed <b>SPL detection queries</b> for brute force and scanning activity</li>
  <li>Simulated attacks using Kali Linux to validate detections</li>
</ul>

<hr>

<h2>Tools & Technologies</h2>

<!-- Network -->
<h3>Network Analysis</h3>
<div>
  <img src="https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white"/>
</div>

<!-- Endpoint -->
<h3>Endpoint Security</h3>
<div>
  <img src="https://img.shields.io/badge/Microsoft_Defender-4CAF50?style=for-the-badge&logo=microsoft&logoColor=white"/>
  <img src="https://img.shields.io/badge/Windows_Event_Logs-0078D6?style=for-the-badge&logo=windows&logoColor=white"/>
</div>

<!-- SIEM -->
<h3>SIEM & Log Analysis</h3>
<div>
  <img src="https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white"/>
</div>

<!-- Log Pipeline -->
<h3>Log Pipeline</h3>
<div>
  <img src="https://img.shields.io/badge/rsyslog-Log%20Forwarder-orange?style=for-the-badge&logo=linux&logoColor=white"/>
  <img src="https://img.shields.io/badge/Syslog-Log%20Ingestion-purple?style=for-the-badge"/>
</div>

<!-- Platforms -->
<h3>Platforms</h3>
<div>
  <img src="https://img.shields.io/badge/Ubuntu_Linux-E95420?style=for-the-badge&logo=ubuntu&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kali_Linux-268BEE?style=for-the-badge&logo=kalilinux&logoColor=white"/>
  <img src="https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"/>
</div>

<hr>

<h2>Future Improvements</h2>

<ul>
  <li>Alerting and automation</li>
  <li>MITRE ATT&CK mapping</li>
  <li>Cloud/VPS deployment</li>
  <li>Threat scoring system</li>
</ul>

<hr>
