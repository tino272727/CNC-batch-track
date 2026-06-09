<div align="center">

<img src="https://www.sju.edu.in/assets/img/st-joseph-university-logo.png" height="80" style="background:white; padding:8px; margin:0 16px;" />
<img src="https://www.erafoundationindia.org/images/logo.svg" height="80" style="background:white; padding:8px; margin:0 16px;" />
<img src="https://comedkares.org/wp-content/uploads/2023/04/Comedkares-Logo-EPS.png" height="80" style="background:white; padding:8px; margin:0 16px;" />

</div>

---

# Integrated OEE Optimization and Batch Traceability System for CNC Manufacturing

**Eleena Aby, MSc BDA, 252BDA43·Tino C Jacob, MSc BDA, 252BDA26·Nandhana K M, MSc BDA, 252BDA20.Rohith Rameesh, MSc BDA, 252BDA41**

## Abstract

The manufacturing industry is rapidly transitioning towards Industry 4.0, where data-driven decision making plays a critical role in improving productivity, efficiency, and product quality. CNC (Computer Numerical Control) machines generate large volumes of operational data that are often underutilized in small and medium-scale manufacturing environments. This project proposes a Data-Driven Overall Equipment Effectiveness (OEE) Optimization and Batch Traceability System that integrates machine monitoring, production analytics, and batch-level tracking into a unified platform.

The proposed system captures machine operation data, tool status, production counts, downtime events, and batch information from CNC machining processes. Using real-time analytics and visualization, the platform computes OEE metrics including Availability, Performance, and Quality while identifying bottlenecks and efficiency losses. Additionally, batch traceability mechanisms provide complete visibility of component manufacturing history, enabling improved quality control and root-cause analysis.

A web-based dashboard developed using Streamlit provides real-time monitoring, KPI visualization, predictive insights, and historical reporting. The system supports production managers in making informed operational decisions while reducing downtime, increasing machine utilization, and improving manufacturing transparency. The proposed solution demonstrates how digital technologies can enhance competitiveness and operational excellence in modern manufacturing environments.

---

## Keywords

Industry 4.0, CNC Manufacturing, Overall Equipment Effectiveness (OEE), Batch Traceability, Machine Monitoring, Data Analytics, Streamlit Dashboard, Production Optimization, Manufacturing Intelligence, Digital Manufacturing.

---

# 1. Introduction

Manufacturing industries are increasingly adopting digital transformation strategies to improve operational efficiency and remain competitive in a rapidly evolving market. Computer Numerical Control (CNC) machines form the backbone of modern manufacturing systems, producing high-precision components for automotive, aerospace, electronics, and industrial applications.

Despite advancements in automation, many manufacturing facilities still face challenges such as unplanned downtime, inefficient machine utilization, lack of production visibility, and inadequate traceability of manufactured components. These issues directly impact productivity, operational costs, and product quality.

Overall Equipment Effectiveness (OEE) has emerged as one of the most widely accepted metrics for evaluating manufacturing performance. OEE combines three key dimensions:

- Availability
- Performance
- Quality

By analyzing these dimensions, manufacturers can identify production losses and opportunities for improvement.

Another critical challenge in manufacturing is batch traceability. In many facilities, tracking the complete history of a manufactured part remains difficult. When defects are identified, determining the responsible machine, operator, tool, or production batch can be time-consuming and costly.

The objective of this project is to develop a comprehensive system that integrates machine monitoring, OEE analysis, and batch traceability into a single platform. By leveraging data analytics and visualization techniques, the system aims to improve production efficiency, reduce downtime, and provide complete manufacturing visibility.

---

# 2. Literature Review

## 2.1 CNC Machine Monitoring and Data Acquisition

According to *Research and Development of Monitoring System and Data Acquisition of CNC Machine Tool in Intelligent Manufacturing* (DOI: 10.1177/1729881419898017), intelligent manufacturing systems require real-time monitoring frameworks capable of collecting machine status, operational parameters, and production data. The study highlights the importance of integrating sensors and communication technologies to enable smart manufacturing environments.

The authors demonstrate that continuous machine monitoring improves decision-making capabilities and supports predictive maintenance strategies.

---

## 2.2 OEE Improvement Using Data Analytics

The paper *Online Overall Equipment Effectiveness (OEE) Improvement Using Data Analytics Techniques for CNC Machines* (DOI: 10.1109/ICACCS48705.2020.9074408) presents a real-time OEE monitoring framework that leverages data analytics techniques to identify production inefficiencies.

The study shows that online monitoring of Availability, Performance, and Quality metrics significantly improves production visibility and enables proactive corrective actions.

---

## 2.3 Batch Traceability Systems

The research work *Towards Part Lifetime Traceability Using Machined Quick Response Codes* (DOI: 10.1016/j.procir.2018.03.175) emphasizes the importance of component-level traceability throughout the manufacturing lifecycle.

The authors propose embedding machine-readable identifiers directly into manufactured parts, enabling complete tracking from production to end-user deployment.

---

## 2.4 Bottleneck Identification

The paper *A Comprehensive Review of Theories, Methods, and Techniques for Bottleneck Identification and Management in Manufacturing Systems* (DOI: 10.3390/app14177712) discusses multiple techniques for identifying production bottlenecks.

The study concludes that real-time data analysis significantly improves bottleneck detection and resource utilization.

---

## 2.5 Digital Technologies in Manufacturing SMEs

The paper *How Digital Technologies Enhance Competitiveness in Manufacturing SMEs* (DOI: 10.1186/s13731-025-00576-8) highlights how data analytics, IoT systems, and digital monitoring platforms improve manufacturing performance, agility, and competitiveness.

The study provides evidence that digital transformation leads to measurable improvements in productivity and operational efficiency.

---

# 3. Problem Statement

Modern CNC manufacturing environments generate large amounts of operational data; however, this information is often fragmented across multiple systems and is not effectively utilized for performance optimization.

The primary challenges include:

### i. Lack of Real-Time Visibility

Production managers often lack real-time information regarding machine status, downtime events, and production efficiency.

### ii. Inefficient OEE Tracking

Many organizations calculate OEE manually or periodically, resulting in delayed identification of performance issues.

### iii. Poor Batch Traceability

Manufacturing records are often maintained separately, making it difficult to trace defective products back to specific machines, tools, operators, or production batches.

### iv. Bottleneck Identification Challenges

Production bottlenecks are frequently identified after significant losses have already occurred.

### v. Limited Data-Driven Decision Making

Without integrated analytics systems, manufacturers struggle to convert machine data into actionable insights.

This project addresses these challenges through an integrated monitoring and analytics platform.

---

# 4. Objectives

The primary objectives of this project are:

1. Develop a real-time CNC machine monitoring system.
2. Collect and store machine operational data.
3. Calculate OEE metrics automatically.
4. Monitor machine downtime and utilization.
5. Implement batch traceability for manufactured components.
6. Identify production bottlenecks using analytics.
7. Provide historical and real-time dashboards.
8. Improve production visibility and decision-making.
9. Support Industry 4.0 digital transformation initiatives.
10. Develop a user-friendly Streamlit-based web application.

---

# 5. Proposed System

The proposed system consists of four major modules:

## 5.1 Data Acquisition Module

This module collects data from CNC machines including:

- Machine Status
- Cycle Time
- Production Count
- Tool Usage
- Downtime Information
- Operator Details
- Batch Details

Data may be obtained through:

- Machine PLCs
- Sensors
- CSV Logs
- ERP/MES Systems
- Simulated Manufacturing Data

---

## 5.2  Overall Equipment Effectiveness (OEE)

### Availability
$$
Availability = \frac{Operating\ Time}{Planned\ Production\ Time}
$$

### Performance
$$
Performance = \frac{Ideal\ Cycle\ Time \times Total\ Count}{Operating\ Time}
$$

### Quality
$$
Quality = \frac{Good\ Parts}{Total\ Parts}
$$

### OEE
$$
OEE = Availability \times Performance \times Quality
$$
## 5.3 Batch Traceability Module

Each production batch contains:

- Batch ID
- Machine ID
- Employee ID
- Tool ID
- Employee Name
- Expected Time Minutes
- Start Time
- End Time
- Actual Duration Minutes
- Delay Minutes
- Inspection Status
- Batch Status
- Production Timestamp
- Product Type 

The system enables:

- Batch Search
- Production History Tracking
- Defect Investigation
- Root Cause Analysis

---

## 5.4 Visualization Dashboard

Developed using Streamlit, the dashboard provides:

- Real-Time Machine Status
- OEE Trends
- Production Analytics
- Downtime Analysis
- Bottleneck Identification
- Batch Tracking Interface
- Historical Reports

---

# 6. System Architecture

```text
+------------------+
| CNC Machines     |
+--------+---------+
         |
         v
+------------------+
| Data Acquisition |
+--------+---------+
         |
         v
+------------------+
| Database Layer   |
| PostgreSQL/MySQL |
+--------+---------+
         |
         v
+------------------+
| Analytics Engine |
+--------+---------+
         |
         v
+------------------+
| OEE Calculator   |
+--------+---------+
         |
         v
+------------------+
| Streamlit UI     |
+------------------+
```

---

# 7. Methodology

## Phase 1: Data Collection

Machine operational data is collected from CNC systems or simulated datasets.

## Phase 2: Data Storage

Data is stored in a relational database.

## Phase 3: Data Processing

Production records are cleaned and validated.

## Phase 4: OEE Calculation

Availability, Performance, and Quality metrics are computed automatically.

## Phase 5: Batch Mapping

Production records are linked to specific batches.

## Phase 6: Analytics

Data analytics techniques identify trends and bottlenecks.

## Phase 7: Visualization

Results are presented through interactive dashboards.

---

# 8. Implementation

## Frontend

- Streamlit

## Backend

- Python

## Database

- PostgreSQL / MySQL

## Libraries

- Pandas
- NumPy
- Plotly
- SQLAlchemy
- Streamlit

---

# 9. Results and Analysis

The proposed system provides:

### Real-Time OEE Monitoring

Continuous tracking of Availability, Performance, and Quality metrics.

### Downtime Analysis

Identification of:

- Machine Failures
- Tool Changes
- Maintenance Events
- Operator Delays

### Batch Traceability

Complete tracking of manufactured components throughout production.

### Bottleneck Detection

Machine-level performance comparison identifies production constraints.

### Decision Support

Managers can make data-driven decisions based on live operational insights.

---

# 10. Discussion

The integration of OEE analytics and batch traceability provides a holistic view of manufacturing performance. Unlike traditional reporting systems, the proposed solution offers near real-time visibility into production activities.

The use of Streamlit significantly reduces development complexity while enabling rapid deployment and interactive visualization. Furthermore, the modular architecture allows future integration with IoT devices, ERP systems, and predictive maintenance models.

---

# 11. Conclusion

This project presents a Data-Driven OEE Optimization and Batch Traceability System for CNC Manufacturing that combines machine monitoring, analytics, and traceability into a unified platform.

The proposed solution enables manufacturers to:

- Improve equipment utilization
- Reduce downtime
- Increase production efficiency
- Enhance product traceability
- Identify bottlenecks
- Support data-driven decision making

The implementation aligns with Industry 4.0 principles and demonstrates how digital technologies can transform modern manufacturing operations.

---

# 12. Future Scope

Future enhancements include:

- IoT Sensor Integration
- Predictive Maintenance Models
- AI-Based Bottleneck Prediction
- Digital Twin Integration
- QR Code Based Part Tracking
- Cloud Deployment
- Mobile Dashboard Support
- Automated Alert Systems
- Machine Learning Based OEE Forecasting

---

# Acknowledgements

The authors express their sincere gratitude to St. Joseph's University, ERA Foundation, COMEDKARES, project mentors, faculty members, and industry experts for their continuous support and guidance throughout this research and development work.

---

# References

[1] Research and Development of Monitoring System and Data Acquisition of CNC Machine Tool in Intelligent Manufacturing. DOI: 10.1177/1729881419898017

[2] Online Overall Equipment Effectiveness (OEE) Improvement Using Data Analytics Techniques for CNC Machines. DOI: 10.1109/ICACCS48705.2020.9074408

[3] Towards Part Lifetime Traceability Using Machined Quick Response Codes. DOI: 10.1016/j.procir.2018.03.175

[4] A Comprehensive Review of Theories, Methods, and Techniques for Bottleneck Identification and Management in Manufacturing Systems. DOI: 10.3390/app14177712

[5] How Digital Technologies Enhance Competitiveness in Manufacturing SMEs. DOI: 10.1186/s13731-025-00576-8
