# Elastic + Cowrie SSH Honeypot

An internet-facing SSH honeypot built with **Cowrie** and analyzed using the **Elastic Stack** to collect and visualize real attacker behavior.

This project simulates a real SOC telemetry pipeline by capturing SSH attack activity and ingesting it into Elastic for analysis, dashboards, and detection engineering.

---

## Project Goals

The goal of this project was to gain hands-on experience with:

- Security telemetry pipelines
- SIEM ingestion and normalization
- Detection engineering
- Threat analysis
- Honeypot deployment and containment

---

## Architecture

The honeypot runs on a cloud VPS and collects attacker activity which is forwarded to Elastic for analysis.

```
Internet
   │
   ▼
┌──────────────────────┐
│  VPS Honeypot        │
│  Cowrie SSH Server   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Elastic Agent        │
│ Log Collection       │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Elastic Stack        │
│ Elasticsearch        │
│ Kibana               │
└──────────┬───────────┘
           │
           ▼
     Dashboards &
     Detection Rules
```

---

## Technologies Used

- **Cowrie** – SSH/Telnet honeypot
- **Elastic Cloud** – SIEM and log storage
- **Elastic Agent** – telemetry ingestion
- **Kibana** – dashboards and visualization
- **GeoIP enrichment** – attacker geolocation
- **Ubuntu Linux** – honeypot host
- **UFW Firewall** – network access control

---

## Data Pipeline

1. Attackers connect to the Cowrie SSH honeypot
2. Cowrie logs attacker activity in JSON format
3. Elastic Agent collects and ships logs
4. Ingest pipelines normalize data fields
5. GeoIP enrichment adds geographic context
6. Kibana dashboards visualize attacker behavior

---

## Telemetry Captured

The honeypot collects several types of attacker activity:

### SSH Brute Force Attempts
- usernames attempted
- password guesses
- source IP addresses

### Attacker Commands
- reconnaissance commands
- malware download attempts
- privilege escalation attempts

### Geographic Data
- attacker country
- ASN / network provider
- geographic distribution of attacks

---

## Detection Engineering

Custom detection rules were implemented to identify suspicious behavior such as:

### Malware Download Attempts

```
cowrie.command : "CMD: wget*"
```

### Credential Brute Force

```
event.action : "cowrie.login.failed"
```

### Reconnaissance Commands

```
cowrie.command : "CMD: uname*"
```

These detections simulate the type of alerts commonly implemented in a SOC environment.

---

## Dashboards

Custom Kibana dashboards visualize:

- Attack timeline
- Most targeted usernames
- Most common attacker commands
- Geographic attack sources
- Top attacking IP addresses

---

## Security Considerations

To reduce the risk of honeypot escape:

- Cowrie runs as a **non-root user**
- SSH hardened with **key authentication**
- VPS isolated from home network
- Firewall restricts unnecessary services
- Cowrie emulates commands instead of executing them

---

## Future Improvements

Planned enhancements include:

- Self-hosted Elastic Stack
- Threat intelligence enrichment
- Automated malware analysis pipeline
- Additional honeypot services

---

## Author

**MrNagz**

Cybersecurity / SOC Analyst Candidate
