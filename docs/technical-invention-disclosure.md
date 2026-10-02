# CellSense – Technical Invention Disclosure

## 1. Title of the Invention / Project

**Project Name:** CellSense – AI-Powered EV Battery State-of-Health Monitoring and Predictive Diagnostics System

**Framework / Challenge Identifier:** 3SVK Research Series Season 3 – National Student Cloud & AI Innovation Challenge

**Technical Domain:** Artificial Intelligence, Machine Learning, Electric Vehicle Battery Diagnostics, Edge AI, Embedded Systems, Battery Analytics, IoT

---

## 2. Applicant / Inventor Information

### Primary Applicant / Inventor

**Name:** [Enter Full Name]

**Institution:** K S Rangasamy College of Technology

**Department:** Computer Science and Engineering

**Role:** Student Researcher / Project Developer

### Additional Applicant / Team Member

**Name:** [Enter Team Member Name]

**Institution:** [Enter Institution]

**Role:** [Enter Role]

### Academic Mentor

**Name:** [Enter Mentor Name]

**Designation:** [Enter Designation]

**Institution:** K S Rangasamy College of Technology

---

## 3. Technical Abstract

CellSense is an AI-assisted electric vehicle battery State-of-Health monitoring and predictive diagnostics system designed to estimate battery health from measurable battery operating characteristics.

The proposed system combines vehicle battery/BMS data acquisition, OBD-II/CAN communication, preprocessing, statistical feature extraction, machine learning-based SOH estimation, edge inference, and wireless communication with a companion application.

The system is designed around an aftermarket-oriented architecture in which accessible battery and BMS-related measurements can be acquired through an appropriate vehicle interface and transformed into model-ready features.

A machine learning development pipeline was evaluated using publicly available NASA lithium-ion battery aging datasets. A multi-battery dataset containing 636 valid battery-cycle records was constructed using 14 engineered input features.

Battery-level holdout validation produced an average Mean Absolute Error (MAE) of approximately 3.36%, Root Mean Squared Error (RMSE) of approximately 3.79%, and R² of approximately 0.85 across four evaluation folds.

The proposed invention further provides an edge-AI deployment direction in which the trained model can be executed locally on an embedded device, reducing dependence on continuous cloud connectivity for SOH inference.

---

## 4. Problem Addressed

Electric vehicle batteries gradually degrade due to repeated charge-discharge cycles, temperature variation, electrical loading, aging, and operating conditions.

Although modern EVs contain Battery Management Systems, detailed battery-health information may not always be directly accessible to vehicle owners, aftermarket service providers, or independent diagnostic systems.

Existing battery monitoring approaches may also depend on:

- Proprietary vehicle diagnostic systems.
- Cloud-based processing.
- Specialized laboratory equipment.
- Battery-specific diagnostic infrastructure.
- Large computational resources.

The technical problem addressed by CellSense is:

**How can accessible battery operating information be transformed into useful battery State-of-Health estimates using machine learning while supporting future real-time edge deployment?**

---

## 5. Objectives of the Invention

The primary objectives are:

1. To estimate EV battery State-of-Health using measurable battery operating parameters.
2. To process voltage, current, temperature, cycle, and discharge-duration information.
3. To extract statistical and temporal features from battery measurements.
4. To develop a machine learning model for SOH estimation.
5. To evaluate model performance across multiple battery aging profiles.
6. To use battery-level validation for assessing generalization.
7. To prepare the trained model for embedded or edge inference.
8. To provide an architecture for OBD-II/CAN-based battery data acquisition.
9. To communicate estimated battery-health information through BLE or Wi-Fi.
10. To provide a foundation for aftermarket EV battery diagnostics.

---

## 6. Proposed System Architecture

The proposed CellSense architecture consists of the following stages:

```text
EV Battery / BMS
        |
        v
   OBD-II / CAN
        |
        v
CellSense Hardware
        |
        v
Data Acquisition
        |
        v
Data Preprocessing
        |
        v
Feature Extraction
        |
        v
Embedded / Edge ML Model
        |
        v
Real-Time SOH Prediction
        |
        +----------------+
        |                |
        v                v
       BLE              Wi-Fi
        |                |
        +-------+--------+
                |
                v
       Companion Application
       ---

## 7. Core Technical Innovation

The core technical approach combines:

1. Battery operating data acquisition.
2. Cycle-level feature engineering.
3. Battery-level machine learning validation.
4. SOH prediction using engineered features.
5. Edge-oriented model deployment.
6. Wireless communication of prediction results.

The system is designed so that the computationally intensive training process can be performed during development while the resulting lightweight inference model can subsequently be deployed closer to the battery data source.

---

## 8. Data Acquisition Module

The proposed system receives battery-related information from the vehicle through an appropriate diagnostic communication interface.

Potential data sources include:

- Battery voltage.
- Battery current.
- Battery temperature.
- BMS measurements.
- Charge/discharge information.
- Cycle-related information.
- Diagnostic parameters available through CAN/OBD-II.

The data acquisition layer provides the raw measurements required for subsequent preprocessing and feature extraction.

The exact parameters available depend on the vehicle platform and BMS implementation.

---

## 9. Data Preprocessing

Raw battery measurements may contain noise, missing values, inconsistent sampling intervals, and varying cycle lengths.

The preprocessing stage therefore performs operations such as:

- Data validation.
- Missing-value handling.
- Signal aggregation.
- Cycle identification.
- Statistical summarization.
- Unit normalization where required.
- Generation of cycle-level records.

The objective is to transform raw measurements into a consistent representation suitable for machine learning.

---

## 10. Feature Engineering

The evaluated CellSense model uses 14 engineered input features.

The feature set includes:

| Feature | Description |
|---|---|
| `cycle_number` | Battery cycle identifier |
| `voltage_mean` | Mean voltage |
| `voltage_min` | Minimum voltage |
| `voltage_max` | Maximum voltage |
| `voltage_std` | Voltage standard deviation |
| `current_mean` | Mean current |
| `current_min` | Minimum current |
| `current_max` | Maximum current |
| `current_std` | Current standard deviation |
| `temperature_mean` | Mean temperature |
| `temperature_min` | Minimum temperature |
| `temperature_max` | Maximum temperature |
| `temperature_std` | Temperature standard deviation |
| `discharge_duration_sec` | Discharge duration in seconds |

These features represent electrical, thermal, temporal, and operational characteristics of battery behavior.

---

## 11. Machine Learning Model

The machine learning component maps the engineered battery features to an estimated SOH value.

The prediction target is:

```text
SOH_percent
Battery Dataset
      |
      v
Data Cleaning
      |
      v
Cycle-Level Processing
      |
      v
Feature Engineering
      |
      v
Train ML Model
      |
      v
Battery-Level Validation
      |
      v
Performance Evaluation
      |
      v
Model Export
      |
      v
Embedded Deployment
---

## 12. Battery-Level Validation

A battery-level holdout strategy was used to evaluate model generalization.

Instead of relying only on random sample splitting, battery groups were separated so that evaluation could be performed on battery data not represented in the corresponding training partition.

This evaluation approach is intended to provide a stronger indication of whether the learned relationship can generalize across different battery aging profiles.

Four validation folds were evaluated.
---

## 13. Performance Metrics

The evaluated results were:

| Fold | MAE | RMSE | R² |
|---|---:|---:|---:|
| Fold 1 | 2.9300% | 3.1052% | 0.9078 |
| Fold 2 | 6.5170% | 7.0948% | 0.6698 |
| Fold 3 | 2.3461% | 2.9022% | 0.8830 |
| Fold 4 | 1.6335% | 2.0675% | 0.9382 |

Average performance:

| Metric | Average |
|---|---:|
| MAE | 3.3567% |
| RMSE | 3.7924% |
| R² | 0.8497 |

These results represent the evaluated experimental dataset and should not be interpreted as guaranteed performance on every commercial EV battery.

---

## 14. Feature Importance

Feature importance analysis identified the following important features in the evaluated model:

| Feature | Importance |
|---|---:|
| `voltage_mean` | 0.2560 |
| `discharge_duration_sec` | 0.1661 |
| `cycle_number` | 0.1401 |
| `temperature_std` | 0.1179 |
| `current_mean` | 0.1172 |

Voltage behavior contributed strongly to the evaluated prediction model, while discharge duration, cycle progression, temperature variation, and current behavior also contributed useful predictive information.

The importance values are model-specific and should not be interpreted as direct physical measurements of degradation mechanisms.

---

## 15. Ablation Study

An ablation study was performed to investigate the contribution of the `cycle_number` feature.

| Feature Configuration | Average MAE |
|---|---:|
| With `cycle_number` | 3.3567% |
| Without `cycle_number` | 3.2791% |

The experiment demonstrates the importance of empirically evaluating individual features rather than assuming that every available feature improves prediction performance.

---

## 16. Edge AI Deployment

A major design direction of CellSense is local inference.

The intended deployment architecture is:

```text
Battery/BMS Data
       |
       v
CellSense MCU
       |
       v
Signal Processing
       |
       v
Feature Extraction
       |
       v
Embedded ML Model
       |
       v
SOH Prediction
       |
       v
BLE / Wi-Fi
       |
       v
Companion Application
---

## 17. Communication and Monitoring

After SOH inference, the predicted health information can be transmitted through a wireless communication layer.

Potential communication technologies include:

- Bluetooth Low Energy (BLE).
- Wi-Fi.

The companion application can display information such as:

- Estimated SOH percentage.
- Battery-health status.
- Historical SOH values.
- Degradation trends.
- Diagnostic information.
- Model prediction timestamps.

The communication layer is separated from the machine learning inference layer so that the core prediction process can remain local to the device.

---

## 18. Novel System Combination

The proposed CellSense architecture combines several technical components into an integrated workflow:

```text
Vehicle Battery/BMS
        +
OBD-II/CAN Acquisition
        +
Cycle-Level Feature Engineering
        +
Machine Learning SOH Estimation
        +
Edge Inference
        +
Wireless Health Reporting
---

## 19. Potential Applications

The proposed system may be applicable to:

- EV battery health monitoring.
- Aftermarket battery diagnostics.
- Used-EV battery assessment.
- EV service centers.
- Fleet battery monitoring.
- Predictive maintenance.
- Battery degradation analysis.
- Research and educational battery analytics.
- Connected EV diagnostic systems.

The system requires additional real-world validation before being used for safety-critical battery decisions.

---

## 20. Advantages of the Proposed System

Potential technical advantages include:

1. Data-driven battery-health estimation.
2. Use of measurable battery operating parameters.
3. Battery-level validation methodology.
4. Modular architecture.
5. Edge-oriented inference design.
6. Reduced dependence on continuous cloud inference.
7. Wireless communication capability.
8. Potential aftermarket applicability.
9. Expandable machine learning architecture.
10. Compatibility with future embedded optimization.

---

## 21. Limitations

The current implementation has several limitations.

### Dataset Limitation

The evaluated model uses publicly available battery aging datasets rather than a large collection of real-world EV battery packs.

### Vehicle Compatibility

The exact battery parameters accessible through OBD-II/CAN vary between vehicle manufacturers and BMS implementations.

### Hardware Validation

The complete production-grade automotive hardware implementation requires additional testing.

### Generalization

Model performance may vary across different battery chemistries, pack configurations, temperatures, vehicles, and operating conditions.

### Safety

The current system should not be treated as a replacement for certified automotive battery safety systems or the vehicle's BMS.

---

## 22. Future Development

Future work includes:

1. Real-world EV battery data collection.
2. Additional battery chemistry support.
3. CAN/OBD-II hardware integration.
4. Target MCU selection and optimization.
5. Embedded model deployment.
6. Hardware-in-the-loop testing.
7. Real-world vehicle validation.
8. SOH trend prediction.
9. Battery anomaly detection.
10. Remaining Useful Life estimation.
11. Mobile application integration.
12. Large-scale fleet evaluation.

---

## 23. Technical Implementation Summary

The current CellSense implementation contains the following major software components:

```text
CellSense
|
+-- backend/
|     +-- Application-side processing
|
+-- frontend/
|     +-- User-facing monitoring interface
|
+-- embedded/
|     +-- Embedded deployment components
|
+-- tests/
|     +-- Validation and testing
|
+-- docs/
|     +-- Research and technical documentation
|
+-- Model
|     +-- Trained SOH prediction model
|
+-- export_model_embedded.py
|     +-- Model export/deployment workflow
|
+-- requirements.txt
|     +-- Python dependencies
---

## 24. Intellectual Property Considerations

The technical concept described in this document concerns the integration of battery data acquisition, feature engineering, machine learning-based SOH estimation, edge inference, and wireless health reporting.

Any future patent application or formal intellectual property filing should be preceded by:

- Prior-art search.
- Novelty assessment.
- Inventorship verification.
- Ownership review.
- Claim drafting.
- Patentability analysis.
- Legal review.

The present document is a technical invention disclosure and does not itself establish patentability or legal protection.

---

## 25. References

1. NASA Ames Prognostics Center of Excellence – Battery Aging Dataset.
2. Public research literature concerning lithium-ion battery State-of-Health estimation.
3. CellSense experimental datasets and validation records.
4. CellSense source-code repository and model-development artifacts.
5. Documentation associated with the CellSense embedded deployment workflow.

---

## 26. Declaration

The information presented in this technical invention disclosure describes the CellSense project architecture, experimental methodology, implementation direction, and intended technical applications.

The reported experimental results correspond to the evaluated datasets and validation procedures described in this document.

Further hardware, vehicle-level, and real-world validation is required before deployment in production or safety-critical automotive applications.
