<div align="center">

<img src="https://www.sju.edu.in/assets/img/st-joseph-university-logo.png" height="80" style="background:white; padding:8px; margin:0 16px;" />
<img src="https://www.erafoundationindia.org/images/logo.svg" height="80" style="background:white; padding:8px; margin:0 16px;" />
<img src="https://comedkares.org/wp-content/uploads/2023/04/Comedkares-Logo-EPS.png" height="80" style="background:white; padding:8px; margin:0 16px;" />

</div>


# MachineIQ: AI-Powered Manufacturing Digital Twin for CNC Batch Traceability and OEE Optimization


## Authors
- Eleena Aby (252BDA43)
- Tino C Jacob (252BDA26)
- Nandhana K M (252BDA20)
- Rohith Rameesh (252BDA41)

---

# Abstract
Modern CNC manufacturing environments suffer from fragmented data, delayed reporting, and lack of real-time visibility into machine performance and production delays. MachineIQ is an AI-powered manufacturing digital twin that integrates batch tracking, machine activity monitoring, QR-based traceability, OEE analytics, anomaly detection, and an AI Copilot powered by LLaMA 3.3 via Groq.

# Keywords
Digital Twin, CNC Manufacturing, OEE, Industry 4.0, QR Traceability, AI Copilot, Groq, LLaMA 3.3, Streamlit

# 1. Introduction
Manufacturing facilities face challenges related to machine downtime, production delays, and fragmented operational data. MachineIQ provides a unified intelligence platform combining machine activity logs, operator actions, and batch tracking into a digital twin environment.

# 2. Problem Statement
- Lack of real-time production visibility
- Manual batch tracking
- Delayed downtime identification
- Difficulty in root-cause analysis
- Fragmented manufacturing data

# 3. Objectives
1. Develop a manufacturing digital twin.
2. Implement QR-based batch traceability.
3. Calculate OEE metrics automatically.
4. Detect manufacturing anomalies.
5. Provide AI-assisted factory insights.
6. Enable real-time monitoring through dashboards.

# 4. Methodology

## Data Sources
- Batch Dataset (~300 records)
- Machine Activity Dataset (~5000+ records)

## Processing Layer
- Data Cleaning
- Feature Engineering
- OEE Computation

## Intelligence Layer
- Rule-Based Anomaly Detection
- Statistical Analysis
- AI Copilot using Groq API

## Application Layer
- Streamlit Dashboard
- QR Scanner Interface
- AI Chat Interface

# 5. System Architecture

Data Sources → Processing Layer → Intelligence Layer → Application Layer

# 6. OEE Computation

OEE = Availability × Performance × Quality

- Availability = Operating Time / Planned Production Time
- Performance = Actual Output / Target Output
- Quality = Good Parts / Total Parts

# 7. QR-Based Traceability

Each batch receives a unique QR code.

Start Scan:
- Records batch start time
- Associates operator and machine

End Scan:
- Records completion time
- Calculates delay
- Stores inspection result

# 8. Anomaly Detection

The system detects:
- High vibration machines
- Delayed batches
- Idle machine states
- Failed inspections

# 9. AI Copilot

Example Questions:
- Which machine has highest delay?
- Why was Batch B001 delayed?
- What is the current factory OEE?

# 10. Technology Stack

| Component | Technology |
|------------|------------|
| Language | Python |
| Data Processing | Pandas, NumPy |
| Dashboard | Streamlit |
| AI Model | LLaMA 3.3 70B |
| AI Backend | Groq API |
| QR Generation | qrcode |
| Deployment | localhost.run |
| Environment | Google Colab |

# 11. Results

The platform provides:
- OEE Analytics
- Delay Analysis
- Machine Ranking
- Employee Performance Analysis
- Batch Traceability

# 12. Future Scope

- IoT Integration
- Predictive Maintenance
- Kafka/MQTT Streaming
- AWS Deployment
- Mobile Application
- Advanced Causal AI

# 13. Conclusion

MachineIQ demonstrates a complete Industry 4.0 prototype combining digital twins, AI-powered analytics, QR traceability, and manufacturing intelligence. The system improves transparency, efficiency, and decision-making in CNC manufacturing environments.

# References

1. Grieves, M. Digital Twin: Manufacturing Excellence through Virtual Factory Replication.
2. Tao et al. Digital Twin in Industry: State-of-the-Art.
3. Nakajima, S. Introduction to TPM.
4. Bokrantz et al. Maintenance in Digitalised Manufacturing.
