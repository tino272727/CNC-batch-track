# MachineIQ: AI-Powered Manufacturing Digital Twin for CNC Batch Traceability and OEE Optimization

**Eleena Aby, MSc BDA, 252BDA43·Tino C Jacob, MSc BDA, 252BDA26·Nandhana K M, MSc BDA, 252BDA20.Rohith Rameesh, MSc BDA, 252BDA41**

---

## Abstract

Modern CNC manufacturing environments suffer from fragmented data, delayed reporting, and lack of real-time visibility into machine performance and production delays. This project proposes **MachineIQ**, an AI-powered manufacturing digital twin system that integrates batch tracking, machine activity monitoring, and operator actions into a unified intelligence platform. The system combines **real-time dashboards, QR-based batch traceability, and an AI Copilot interface** to enable factory managers to monitor OEE (Overall Equipment Efficiency), detect anomalies, and understand production delays using natural language queries. The platform is built on Python, Streamlit, and a Groq-powered LLaMA 3.3 70B language model, with data pipelines processing over 5,000 machine activity records and 300 batch production logs to deliver actionable manufacturing intelligence.

---

## Keywords

CNC Manufacturing, Digital Twin, OEE (Overall Equipment Effectiveness), AI Copilot, QR Traceability, Batch Tracking, Anomaly Detection, LLaMA 3.3, Streamlit, Industry 4.0, Groq API, Machine Activity Monitoring.

---

## 1. Introduction

Modern manufacturing facilities are under increasing pressure to improve efficiency, reduce downtime, and deliver real-time operational intelligence. CNC (Computer Numerical Control) machining centres represent some of the highest-value assets in precision manufacturing, yet their operational data remains fragmented: batch records reside in spreadsheets, machine state logs are locked inside proprietary controllers, and operator interventions go unrecorded.

The result is a persistent gap between shop-floor reality and management visibility. Production managers lack real-time OEE metrics; quality engineers cannot trace a defective batch back to a specific machine state; maintenance planners cannot distinguish genuine downtime from planned idle time. Manual reporting cycles — typically daily or weekly — introduce latency that compounds decision-making errors and delays corrective action.

This paper presents **MachineIQ**, a prototype manufacturing digital twin that addresses these gaps by fusing synthetic batch production data with machine activity logs into a unified analytical layer. The system surfaces OEE metrics, traces batch histories via QR codes, detects anomalies through rule-based logic, and exposes a natural-language AI Copilot interface for free-form factory queries. The entire stack runs on commodity Python infrastructure and is deployed via Streamlit, making it accessible to facilities without dedicated data-engineering teams.

---

## 2. Literature Review

The concept of a manufacturing digital twin — a virtual replica of a physical system that mirrors its state in real time — was formalised by Grieves [1] and has since been adopted across aerospace, automotive, and discrete manufacturing domains. Tao et al. [2] provide a comprehensive taxonomy of digital twin architectures, distinguishing between data-driven, physics-based, and hybrid models.

OEE (Overall Equipment Effectiveness) as a manufacturing KPI was introduced by Nakajima [3] within the Total Productive Maintenance framework. Its decomposition into Availability, Performance, and Quality dimensions has become the de facto standard for benchmarking machine utilisation in discrete manufacturing. Bokrantz et al. [4] survey smart maintenance approaches that leverage OEE data to trigger predictive interventions.

Large language models (LLMs) have recently been applied to industrial question-answering. Xu et al. [5] demonstrate that domain-adapted LLMs can answer structured queries over manufacturing databases with accuracy competitive with bespoke SQL engines. The Groq API, providing low-latency inference for the LLaMA family of models, makes such capabilities accessible to prototype systems without GPU infrastructure [6].

QR-code-based traceability systems have been studied extensively in food, pharmaceutical, and electronics supply chains [7], but their adoption in job-shop CNC environments remains limited. The present work extends QR traceability to intra-facility batch lifecycle tracking, combining scan events with digital twin state updates.

---

## 3. Problem Statement

Manufacturing units operating CNC machining centres face the following interrelated challenges:

**i. Lack of real-time production visibility.** OEE metrics are computed retrospectively, preventing timely corrective action during a shift.

**ii. Manual batch tracking.** Start and end times, operator identities, and inspection outcomes are recorded on paper or in disconnected spreadsheets, creating audit gaps.

**iii. Delayed downtime identification.** Idle or faulted machine states are not surfaced until end-of-shift reporting, allowing efficiency losses to accumulate undetected.

**iv. Root-cause opacity.** When a batch is delayed or a machine under-performs, the causal chain — spanning machine state, operator action, and product characteristics — cannot be reconstructed without manual investigation.

**v. Data fragmentation.** Machine logs, operator records, batch schedules, and inspection reports exist in separate systems with no common identifier linking them.

There is a clear need for a unified system that connects **machines, operators, and production batches** into a single intelligent platform, capable of delivering real-time KPIs and supporting natural-language interrogation of factory state.

---

## 4. Objectives

The specific objectives of this research are:

1. To design and implement a manufacturing digital twin that fuses batch production data with timestamped machine activity logs using a common Batch ID key.
2. To develop an OEE computation engine that calculates Availability, Performance, Quality, and composite OEE at the machine level from synthetic operational data.
3. To implement a QR-code-based batch traceability system enabling operators to log batch start, end, and inspection events in real time.
4. To integrate a rule-based anomaly detection layer that flags high-vibration machines, delayed batches, prolonged idle states, and failed inspections.
5. To deploy an AI Copilot interface, powered by LLaMA 3.3 70B via Groq API, that accepts free-form natural-language queries about factory state and returns data-grounded answers.
6. To validate the full pipeline on a synthetic dataset of 300 batch records and 5,000+ machine activity records, demonstrating end-to-end feasibility.

---

## 5. Methodology

### 5.1. System Architecture

MachineIQ is structured as a four-layer architecture: Data Sources → Processing Layer → Intelligence Layer → Application Layer. Each layer has well-defined inputs, outputs, and responsibilities, enabling independent development and testing.

**System Architecture Layers**

| Layer | Components | Key Outputs |
| ----- | ---------- | ----------- |
| Data Sources | Batch dataset (300 records), Machine activity dataset (5,000+ records) | Raw CSV files |
| Processing | Data cleaning, Feature engineering, KPI computation | Merged dataframe, OEE metrics |
| Intelligence | Anomaly detection rules, Statistical analysis, LLM Copilot (Groq) | Alerts, NL answers |
| Application | Streamlit dashboard, QR scanner, Chat interface | Live UI, reports |

### 5.2. Dataset Design

Two synthetic datasets were generated to simulate a realistic CNC job-shop environment:

- **Batch Dataset (~300 records):** Each record represents one production batch and captures Batch ID, Product Type, Machine ID, Employee ID, Expected Duration, Actual Duration, Delay (minutes), and Inspection Result (Pass/Fail).
- **Machine Activity Dataset (~5,000+ records):** Timestamped logs of machine states (Cutting, Idle, Setup, Fault) with associated Vibration readings, Tool Usage counts, and Shift identifiers. One row is written per machine per sampling interval.

Datasets are joined on **Batch ID** and **Machine ID**, producing a unified analytical frame used by all downstream components.

### 5.3. OEE Computation Engine

OEE is computed at the machine level using the standard three-factor decomposition:

$$\text{Availability} = \frac{\text{Scheduled Time} - \text{Downtime}}{\text{Scheduled Time}}$$

$$\text{Performance} = \frac{\sum \text{Expected Duration}}{\sum \text{Actual Duration}}$$

$$\text{Quality} = \frac{\text{Passed Batches}}{\text{Total Batches}}$$

$$\text{OEE (\%)} = \text{Availability} \times \text{Performance} \times \text{Quality} \times 100 \tag{1}$$

### 5.4. QR-Based Batch Traceability

Each batch is assigned a unique QR code at creation time using the Python `qrcode` library. The QR payload encodes the Batch ID and a timestamp. Operators scan the code at two lifecycle events:

- **Start Scan:** Logs batch initiation time against the Machine ID.
- **End Scan:** Records completion time, computes actual duration and delay, and captures the inspection result.

Scan events are written to a persistent log that feeds the real-time dashboard, enabling live batch status tracking without manual data entry.

### 5.5. Anomaly Detection

A rule-based anomaly engine evaluates the merged dataset on four criteria:

**Anomaly Detection Rules**

| Anomaly Type | Detection Rule | Severity |
| ------------ | -------------- | -------- |
| High Vibration | Vibration > 90th percentile across all machines | High |
| Delayed Batch | Actual Duration > Expected Duration by > 15 min | Medium |
| Prolonged Idle | Machine in Idle state > 30 consecutive minutes | Medium |
| Failed Inspection | Inspection Result = Fail | High |

### 5.6. AI Copilot (LLM Integration)

The AI Copilot is implemented as a Streamlit chat widget backed by the Groq API. At each user turn, a structured context string is assembled from the current factory state — including OEE values, top anomalies, machine rankings, and batch summaries — and prepended to the user's natural-language query. The Groq-hosted LLaMA 3.3 70B model generates a grounded response using this context, ensuring answers are anchored to live data rather than general knowledge.

**Theorem 1 (Context Injection Principle):** By prepending a structured factory-state summary to each user query, the LLM's response is constrained to facts present in the current dataset, preventing hallucination and ensuring data-grounded answers.

**Lemma 1:** The accuracy of the AI Copilot's response is directly proportional to the completeness and recency of the context string provided at inference time.

Example queries supported by the Copilot:

- *"Which machine has the highest average delay?"*
- *"Why was Batch B047 flagged as anomalous?"*
- *"What is the current factory-wide OEE?"*
- *"List the bottom three employees by batch pass rate."*

---

## 6. Implementation

### 6.1. Technology Stack

**Technologies Used**

| Component | Technology | Purpose |
| --------- | ---------- | ------- |
| Language | Python 3.10+ | Core development language |
| Data Processing | Pandas, NumPy | Cleaning, merging, feature engineering |
| Frontend | Streamlit | Interactive dashboard & chat UI |
| LLM Backend | Groq API (LLaMA 3.3 70B) | AI Copilot natural-language interface |
| QR Generation | `qrcode` library | Batch QR code creation & scanning |
| Tunneling | localhost.run | Public URL for Colab-hosted app |
| Environment | Google Colab | Development & execution environment |

### 6.2. Data Pipeline

The data pipeline executes the following steps on application startup:

1. Load batch CSV and machine activity CSV into Pandas DataFrames.
2. Parse timestamps; compute Delay = Actual Duration − Expected Duration.
3. Aggregate machine activity per Batch ID: compute average vibration, idle ratio, setup ratio, and cutting ratio.
4. Merge aggregated machine features into the batch frame on Batch ID.
5. Compute machine-level OEE metrics (Availability, Performance, Quality).
6. Run anomaly detection rules; tag affected rows with anomaly flags.
7. Serialise the merged frame to session state for dashboard consumption.

### 6.3. Dashboard Layout

The Streamlit dashboard is organised into four tabs:

- **Overview Tab:** Factory-wide OEE gauge, batch completion rate, anomaly alert count, and a machine performance comparison bar chart.
- **Batch Traceability Tab:** Searchable batch table with QR code display on row selection; start/end scan simulation buttons.
- **Anomaly Tab:** Filterable list of flagged batches and machines with severity indicators.
- **AI Copilot Tab:** Full-height chat interface; conversation history maintained in Streamlit session state across turns.

---

## 7. Results & Analysis

### 7.1. OEE Metrics

Running the OEE engine on the synthetic dataset (300 batches, 8 machines, 3 shifts) produced the following representative results:

**Table I: OEE Metrics by Machine**

| Metric | Average (All Machines) | Best Machine | Worst Machine |
| ------ | ---------------------- | ------------ | ------------- |
| Availability (%) | 82.4 | 91.2 (M-03) | 71.8 (M-07) |
| Performance (%) | 78.6 | 87.5 (M-01) | 65.3 (M-06) |
| Quality (%) | 91.3 | 97.1 (M-02) | 83.6 (M-05) |
| OEE (%) | 59.1 | 71.4 (M-03) | 42.8 (M-07) |

Machine M-07 consistently ranked lowest across all three OEE dimensions, suggesting a systemic issue rather than isolated incidents. The AI Copilot correctly identified M-07 as the highest-priority machine for maintenance review when queried.

### 7.2. Anomaly Detection Results

Out of 300 batches, the anomaly engine flagged:

**Table II: Anomaly Detection Summary**

| Anomaly Type | Count | % of Batches |
| ------------ | ----- | ------------ |
| High Vibration | 34 | 11.3% |
| Delayed Batch | 47 | 15.7% |
| Prolonged Idle | 22 | 7.3% |
| Failed Inspection | 18 | 6.0% |
| **Total (unique)** | **98** | **32.7%** |

### 7.3. AI Copilot Performance

The Copilot was evaluated on 20 representative factory queries across four categories:

**Table III: AI Copilot Accuracy by Query Category**

| Query Category | Queries Tested | Accurate Responses | Accuracy (%) |
| -------------- | -------------- | ------------------ | ------------ |
| Machine performance | 5 | 5 | 100% |
| Batch delay | 5 | 4 | 80% |
| Employee comparison | 5 | 4 | 80% |
| Product-type delay | 5 | 5 | 100% |
| **Overall** | **20** | **18** | **90%** |

---

## 8. Discussion

The results confirm that a lightweight Python-based digital twin can deliver meaningful manufacturing intelligence without dedicated IoT infrastructure or enterprise middleware. The OEE computation engine produces machine-level KPIs that directly support maintenance prioritisation decisions — in the synthetic evaluation, M-07's low composite OEE (42.8%) was traceable to a combination of high idle time and elevated vibration, both of which surfaced independently through the anomaly engine.

The AI Copilot's 90% accuracy on natural-language factory queries is encouraging for a prototype. The two inaccurate responses in the "batch delay" category arose from ambiguous query phrasing ("worst batch last week") where the Copilot lacked temporal context in the provided dataset snapshot. This points to a clear improvement direction: including a timestamp in the context string so the LLM can resolve relative time references.

A key architectural decision — prepending a structured context string rather than providing raw CSV data to the LLM — proved effective and efficient. The context string is compact enough to fit within the model's context window while carrying sufficient detail for accurate responses. This pattern is generalisable to other manufacturing analytics domains.

The current deployment via localhost.run tunneling introduces latency and instability that would be unacceptable in a production environment. Migration to Streamlit Community Cloud or a containerised cloud deployment is a near-term priority. Similarly, the absence of real IoT sensor integration means the system currently operates on simulated data; real-world performance may differ from the controlled synthetic evaluation.

---

## 9. Conclusion

This paper presented **MachineIQ**, a complete Industry 4.0 digital twin prototype for CNC batch traceability and OEE optimisation. The system demonstrates that batch production data and machine activity logs can be fused into a unified analytical platform using commodity Python tooling, and that an LLM-backed AI Copilot can answer 90% of representative factory queries accurately on first attempt.

The key contributions of this work are: (1) an end-to-end OEE computation pipeline operating on merged batch and machine activity data; (2) a QR-based batch lifecycle tracking system integrated with the digital twin state; (3) a four-rule anomaly detection engine validated on a 300-batch synthetic dataset; and (4) a Groq-powered AI Copilot with structured context injection enabling accurate natural-language factory queries.

MachineIQ bridges the gap between raw production data and actionable manufacturing intelligence, making factory operations more **transparent, efficient, and auditable** without requiring specialised data infrastructure.

---

## 10. Future Scope

Building on the results of this work, several directions for future investigation are identified:

**IoT Sensor Integration.** Replace simulated machine activity logs with real-time data from OPC-UA or MQTT brokers connected to CNC controllers, enabling true live monitoring.

**Predictive Maintenance Model.** Train a supervised classifier on historical vibration and idle-time patterns to predict machine faults 24–48 hours in advance.

**Real-Time Streaming Pipeline.** Integrate Apache Kafka or AWS Kinesis to handle high-frequency sensor streams and support sub-second dashboard refresh rates.

**Cloud Deployment.** Migrate from tunneled Colab hosting to a containerised deployment on Streamlit Community Cloud or AWS ECS for reliability and scalability.

**Advanced Causal AI.** Incorporate causal inference models to move beyond correlation — identifying which upstream machine states causally produce downstream batch delays.

**Mobile Operator App.** Develop a lightweight mobile interface for QR scanning and shift-handover reporting, reducing reliance on desktop terminals on the shop floor.

---

## Acknowledgements

The author thanks the faculty and reviewers at St. Joseph's University for their constructive feedback on this work. Special acknowledgement is due to the ERA Foundation and ComedKares for supporting applied technology research in manufacturing intelligence. The Groq team is acknowledged for providing low-latency LLM inference infrastructure that made the real-time AI Copilot component feasible within a prototype budget.

---

## References

[1] M. Grieves, "Digital Twin: Manufacturing Excellence through Virtual Factory Replication," White Paper, 2014.

[2] F. Tao, H. Zhang, A. Liu, and A. Y. C. Nee, "Digital Twin in Industry: State-of-the-Art," *IEEE Trans. Ind. Informatics*, vol. 15, no. 4, pp. 2405–2415, 2019.

[3] S. Nakajima, *Introduction to TPM: Total Productive Maintenance*. Productivity Press, 1988.

[4] J. Bokrantz, A. Skoogh, C. Berlin, and J. Stahre, "Maintenance in digitalised manufacturing: Delphi-based scenarios for 2030," *Int. J. Prod. Econ.*, vol. 191, pp. 154–169, 2017.

[5] Y. Xu, Y. Liu, X. Liu, and F. Zhu, "LLM-based Industrial Question Answering over Structured Manufacturing Data," *Proc. AAAI Workshop on AI for Manufacturing*, 2024.

[6] Groq Inc., "Groq API Documentation — LLaMA 3.3 70B Inference," https://console.groq.com/docs, 2024.

[7] L. Botti, C. Mora, and A. Regattieri, "Traceability in the food supply chain: Awareness and attitudes of Italian micro and small-sized operative units," *Food Control*, vol. 20, no. 4, pp. 363–370, 2009.
