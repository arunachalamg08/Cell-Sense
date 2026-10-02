# CellSense: AI-Powered EV Battery State-of-Health Monitoring and Predictive Diagnostics System

## 1. Abstract

CellSense is an AI-assisted electric vehicle (EV) battery health monitoring and predictive diagnostics system designed to estimate battery State-of-Health (SOH) from measurable battery operating characteristics. The system combines battery data acquisition, preprocessing, feature engineering, machine learning-based SOH estimation, and a deployment architecture intended for edge or embedded inference.

The primary objective of CellSense is to provide an accessible approach for monitoring battery degradation without depending exclusively on proprietary battery management system diagnostics. The proposed architecture receives battery and BMS-related information through an OBD-II/CAN interface, processes the acquired measurements, extracts relevant features, and applies a trained machine learning model to estimate battery SOH. The predicted health information can subsequently be communicated to a companion application through wireless connectivity.

The machine learning development pipeline was evaluated using publicly available NASA lithium-ion battery aging datasets. Data from multiple battery cells were processed into cycle-level records containing electrical, thermal, temporal, and cycle-related characteristics. A total of 636 valid battery-cycle records were used in the evaluated multi-battery dataset, with 14 engineered input features and SOH percentage as the prediction target.

Battery-level holdout validation was used to evaluate generalization across different batteries. Across four evaluation folds, the developed baseline achieved an average Mean Absolute Error (MAE) of approximately 3.36%, Root Mean Squared Error (RMSE) of approximately 3.79%, and coefficient of determination (R²) of approximately 0.85.

The resulting system provides a foundation for real-time EV battery health monitoring and future deployment of lightweight machine learning inference on embedded hardware.

---

## 2. Introduction

Electric vehicles depend heavily on the condition of their battery packs for driving range, performance, reliability, and safety. Battery capacity gradually decreases as a result of charge-discharge cycles, operating temperature, electrical loading, aging, and other degradation mechanisms.

State-of-Health (SOH) is an important indicator used to represent the remaining health or usable capacity of a battery relative to an appropriate reference condition. Accurate estimation of SOH can help identify battery degradation and support predictive maintenance.

Conventional battery monitoring systems primarily rely on Battery Management Systems (BMS) and electrical measurements. However, advanced battery diagnostics and detailed health information may not always be directly accessible to vehicle owners or aftermarket service providers.

CellSense investigates an aftermarket-oriented architecture that combines accessible vehicle data, machine learning, and connected monitoring to estimate battery health.

---

## 3. Problem Statement

The project addresses the following problem:

How can measurable EV battery operating parameters be processed and used by a machine learning model to estimate battery State-of-Health and provide useful battery-health information through an accessible monitoring architecture?

The system focuses on:

- Battery degradation estimation.
- Cycle-level SOH prediction.
- Generalization across multiple battery datasets.
- Feature-based machine learning.
- Real-time monitoring architecture.
- Future embedded or edge inference.
- Communication of health information to a companion application.

---

## 4. Objectives

The main objectives of CellSense are:

1. To develop a data-driven approach for estimating EV battery SOH.
2. To process battery voltage, current, temperature, cycle, and discharge-duration information.
3. To engineer meaningful statistical features from battery operating data.
4. To evaluate machine learning performance across multiple batteries.
5. To investigate battery-level validation rather than relying only on random sample splitting.
6. To prepare a deployable machine learning model for future embedded inference.
7. To design an architecture connecting vehicle battery data, an edge device, and a companion application.
8. To provide a foundation for aftermarket EV battery health monitoring.

---

## 5. Proposed CellSense System

The proposed CellSense system consists of multiple functional layers:

1. Vehicle battery and Battery Management System.
2. OBD-II/CAN data interface.
3. CellSense data acquisition layer.
4. Data preprocessing and feature extraction.
5. Machine learning SOH prediction.
6. Edge/embedded inference layer.
7. Wireless communication.
8. Companion application.

The system is designed so that the machine learning component can eventually operate locally on the CellSense hardware rather than requiring continuous cloud connectivity for inference.

---

## 6. System Architecture

The high-level architecture is:

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
Preprocessing
       |
       v
Feature Extraction
       |
       v
Machine Learning Model
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

## 7. Data Acquisition

The research and model-development stage used publicly available lithium-ion battery aging data from NASA battery datasets.

The evaluated multi-battery dataset incorporated data from:

- B0005
- B0006
- B0007
- B0018

The raw battery measurements include electrical and thermal information recorded during battery operation and degradation cycles.

For model development, the raw measurements were transformed into cycle-level statistical representations.

---

## 8. Dataset Preparation

The processed multi-battery dataset contained:

- 636 valid battery-cycle records.
- 14 input features.
- SOH percentage as the target variable.

The processing pipeline converted raw cycle measurements into structured numerical features.

The reference battery capacity and degradation information were used to derive the SOH target.

SOH was represented as a percentage relative to the corresponding reference capacity.

---

## 9. Feature Engineering

The following 14 features were used in the evaluated model:

1. `cycle_number`
2. `voltage_mean`
3. `voltage_min`
4. `voltage_max`
5. `voltage_std`
6. `current_mean`
7. `current_min`
8. `current_max`
9. `current_std`
10. `temperature_mean`
11. `temperature_min`
12. `temperature_max`
13. `temperature_std`
14. `discharge_duration_sec`

These features capture multiple aspects of battery behavior.

### Electrical Characteristics

Voltage and current statistics represent the electrical operating behavior of the battery during a cycle.

### Thermal Characteristics

Temperature statistics provide information about the thermal behavior of the battery.

### Temporal Characteristics

Discharge duration represents the time required for the observed discharge process.

### Aging Characteristics

Cycle number provides an indication of the battery's position within its degradation history.

---

## 10. Machine Learning Methodology

The machine learning pipeline consists of:

```text
Raw Battery Data
       |
       v
Data Cleaning
       |
       v
Cycle Extraction
       |
       v
Feature Engineering
       |
       v
Feature Matrix
       |
       v
Model Training
       |
       v
Battery-Level Validation
       |
       v
SOH Prediction
---

## 11. Battery-Level Validation

A key part of the evaluation is battery-level holdout validation.

Instead of randomly distributing all cycles from every battery between training and testing sets, the evaluation separates battery groups so that the model is evaluated on battery data that is not represented in the corresponding training partition.

This approach provides a more meaningful test of generalization across different battery aging profiles.

Four evaluation folds were performed.

---

## 12. Experimental Results

The evaluated baseline produced the following battery-level validation results.

| Fold | MAE | RMSE | R² |
|---|---:|---:|---:|
| Fold 1 | 2.9300% | 3.1052% | 0.9078 |
| Fold 2 | 6.5170% | 7.0948% | 0.6698 |
| Fold 3 | 2.3461% | 2.9022% | 0.8830 |
| Fold 4 | 1.6335% | 2.0675% | 0.9382 |

### Average Performance

| Metric | Average |
|---|---:|
| MAE | 3.3567% |
| RMSE | 3.7924% |
| R² | 0.8497 |

These results indicate that the model can learn a meaningful relationship between battery operating characteristics and SOH across the evaluated datasets.

The variation between folds also demonstrates that model performance can change depending on the battery degradation profile represented in the held-out evaluation set.

---

## 13. Feature Importance

Feature importance analysis was performed to investigate the contribution of the input variables.

The observed importance values included:

| Feature | Importance |
|---|---:|
| `voltage_mean` | 0.2560 |
| `discharge_duration_sec` | 0.1661 |
| `cycle_number` | 0.1401 |
| `temperature_std` | 0.1179 |
| `current_mean` | 0.1172 |

Voltage-related behavior contributed strongly to the evaluated model, while discharge duration, cycle progression, temperature variation, and current behavior also provided useful predictive information.

Feature importance should be interpreted as model-specific evidence rather than a direct physical measure of battery degradation mechanisms.

---

## 14. Cycle Number Ablation Study

An ablation experiment was performed to investigate the effect of the cycle number feature.

The observed average validation results were:

| Feature Configuration | Average MAE |
|---|---:|
| With `cycle_number` | 3.3567% |
| Without `cycle_number` | 3.2791% |

In this evaluation, removing cycle number produced a slightly lower average MAE.

This result indicates that explicit cycle progression was not necessarily required for the evaluated feature set to estimate SOH and highlights the importance of validating feature usefulness empirically rather than assuming that every available feature improves performance.
---

## 15. Edge AI Deployment Architecture

A key design objective of CellSense is to move inference toward the edge.

The intended deployment architecture is:

```text
Vehicle Data
     |
     v
CellSense MCU
     |
     +--> Signal Processing
     |
     +--> Feature Extraction
     |
     +--> Embedded ML Model
     |
     v
SOH Prediction
     |
     v
BLE / Wi-Fi
     |
     v
Mobile Application
---

## 16. Software Architecture

The CellSense repository is organized into multiple functional components.

### Backend

The backend layer is responsible for application-side processing and service functionality.

### Frontend

The frontend provides the user-facing monitoring interface.

### Embedded

The embedded component represents the hardware-oriented deployment layer and supports the future execution of the trained model on resource-constrained hardware.

### Tests

The testing layer provides a location for validation and software quality checks.

### Archive

The archive component provides project and development artifacts.

The repository also contains the trained SOH model and model-export functionality used as part of the deployment workflow.

---

## 17. Real-Time Monitoring Concept

The intended operational flow is:

```text
1. Vehicle operates
        |
2. Battery/BMS data becomes available
        |
3. CellSense acquires measurements
        |
4. Data is preprocessed
        |
5. Features are extracted
        |
6. ML model performs inference
        |
7. SOH estimate is generated
        |
8. Result is transmitted
        |
9. User views battery-health information
---

## 18. Applications

Potential applications of the CellSense architecture include:

- EV battery health monitoring.
- Aftermarket battery diagnostics.
- Used-EV battery assessment.
- Battery maintenance support.
- Fleet battery monitoring.
- Predictive maintenance systems.
- Battery degradation trend analysis.
- EV service and inspection workflows.

### EV Battery Health Monitoring

CellSense can provide an estimated battery SOH value that can help users understand the general degradation state of an EV battery.

### Aftermarket Battery Diagnostics

The architecture is intended to support an aftermarket diagnostic approach using vehicle-accessible battery and BMS information.

### Used-EV Battery Assessment

Battery-health estimation could support technical assessment of used electric vehicles by providing an additional data-driven indicator of battery condition.

### Fleet Monitoring

A connected implementation could be extended to fleet environments where battery-health information from multiple vehicles can be collected and analyzed.

### Predictive Maintenance

Historical SOH estimates can potentially be used to identify degradation trends and support maintenance planning.

These applications require further validation using real-world EV battery systems before deployment in production or safety-critical environments.
---

## 19. Limitations

The current research has several limitations.

### Dataset Limitation

The evaluated model is based on publicly available battery aging datasets rather than a large collection of real-world EV battery packs operating across different vehicles.

### Hardware Limitation

The complete production-grade automotive hardware implementation requires additional validation.

### Generalization

Performance may vary for battery chemistries, pack configurations, vehicle platforms, temperatures, and operating conditions that are not represented in the training data.

### Real-World Validation

Additional testing on real EV battery packs is required before the system can be considered suitable for safety-critical or commercial battery diagnostics.

### Model Optimization

Further work is required to optimize inference for the computational, memory, and power constraints of the final target MCU.

---

## 20. Future Work

Future development of CellSense will focus on:

1. Collecting real-world EV battery and BMS data.
2. Supporting additional battery chemistries.
3. Expanding the training dataset.
4. Improving cross-vehicle generalization.
5. Implementing CAN/OBD-II acquisition on the target hardware.
6. Deploying the model directly on the MCU.
7. Optimizing model size and inference latency.
8. Adding battery degradation trend visualization.
9. Developing anomaly detection for abnormal battery behavior.
10. Integrating battery diagnostics with the companion application.
11. Performing hardware-in-the-loop testing.
12. Conducting real-world EV validation.

---

## 21. Research and Innovation Contribution

CellSense combines battery data analytics, machine learning, embedded inference, and connected monitoring into a single proposed architecture.

The research component focuses on transforming battery operating measurements into cycle-level features and evaluating SOH prediction across multiple battery datasets.

The engineering component focuses on translating the trained model toward an edge-deployed monitoring device.

The proposed combination provides a foundation for future research into accessible, data-driven EV battery diagnostics.

The project demonstrates an end-to-end development direction covering:

- Battery data acquisition
- Data preprocessing
- Feature engineering
- Machine learning
- Model evaluation
- Edge AI deployment
- Wireless communication
- User-facing monitoring

---

## 22. Conclusion

CellSense presents an AI-assisted approach for EV battery State-of-Health estimation and predictive monitoring.

The evaluated multi-battery dataset contained 636 cycle-level records and 14 engineered input features. Battery-level validation produced an average MAE of approximately 3.36%, RMSE of approximately 3.79%, and R² of approximately 0.85 across the four evaluated folds.

The project further explores an edge-oriented deployment architecture in which battery information is acquired through vehicle interfaces, processed locally, passed through an embedded machine learning model, and communicated to a companion application.

Although additional real-world validation is required, the current results demonstrate the feasibility of using machine learning and battery operating characteristics as a foundation for an EV battery-health monitoring platform.

---

## 23. References

1. NASA Ames Prognostics Center of Excellence, Battery Aging Dataset.
2. Battery State-of-Health estimation literature and research publications.
3. Documentation and experimental records maintained in the CellSense project repository.
