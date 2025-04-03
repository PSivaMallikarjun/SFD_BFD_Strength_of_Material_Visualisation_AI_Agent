# Structural Beam Analysis with ML Agent

## User Manual & ISO Standards Documentary

**Version 1.0**  
**April 2025**

---

## Table of Contents

1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Beam Analysis Module](#beam-analysis-module)
4. [Beam Optimization Module](#beam-optimization-module)
5. [Machine Learning Training Module](#machine-learning-training-module)
6. [Theoretical Background](#theoretical-background)
7. [Relevant ISO Standards](#relevant-iso-standards)
8. [Troubleshooting](#troubleshooting)
9. [Glossary](#glossary)
10. [References](#references)

---

## 1. Introduction

The Structural Beam Analysis with ML Agent is an advanced computational tool designed to assist structural engineers, architects, and engineering students in analyzing and optimizing beam designs. This application combines traditional structural engineering principles with modern machine learning techniques to provide accurate predictions of beam behavior under various loading conditions.

### 1.1 Key Features

- Interactive visualization of beam configurations
- Calculation of Shear Force Diagrams (SFD) and Bending Moment Diagrams (BMD)
- Machine learning-based prediction of maximum shear forces and bending moments
- Automatic identification of critical points along beam spans
- Intelligent optimization suggestions to improve beam performance
- Training and re-training capabilities for the ML models

### 1.2 System Requirements

- Python 3.7 or later
- Required libraries: gradio, numpy, matplotlib, pandas, scikit-learn, joblib
- Minimum 4GB RAM recommended
- Graphics support for visualization components

---

## 2. Getting Started

### 2.1 Installation

1. Ensure Python 3.7+ is installed on your system
2. Install required dependencies:
   ```
   pip install gradio numpy matplotlib pandas scikit-learn joblib
   ```
3. Download the application source code
4. Run the application:
   ```
   python beam_analysis_app.py
   ```

### 2.2 Interface Overview

The application interface is divided into three main tabs:

1. **Beam Analysis**: Configure beam parameters and visualize SFD/BMD results
2. **Beam Optimization**: Receive suggestions for improving beam performance
3. **ML Model Training**: Train or retrain the ML prediction models

---

## 3. Beam Analysis Module

The Beam Analysis module allows you to define beam parameters and visualize the resulting behavior.

### 3.1 Input Parameters

| Parameter | Description | Format | Example |
|-----------|-------------|--------|---------|
| Beam Length | Total span of the beam in meters | Positive number | 10.0 |
| Point Loads | List of position-magnitude pairs | [(pos1, mag1), (pos2, mag2), ...] | [(2, -1000), (8, -2000)] |
| UDL Start Position | Starting position of uniformly distributed load | Number between 0 and beam length | 4.0 |
| UDL End Position | Ending position of uniformly distributed load | Number between UDL start and beam length | 7.0 |
| UDL Value | Magnitude of uniformly distributed load in N/m | Any number (positive: upward, negative: downward) | -500 |

### 3.2 Interpreting Point Loads

- Position values must be between 0 and beam length
- Magnitude values are in Newtons (N)
- Positive values indicate upward forces
- Negative values indicate downward forces

### 3.3 Interpreting UDL Parameters

- The UDL is applied between the start and end positions
- UDL value is specified in Newtons per meter (N/m)
- Positive values indicate upward distributed load
- Negative values indicate downward distributed load

### 3.4 Output Visualization

The visualization consists of three main components:

1. **Beam Configuration**: Visual representation of the beam with all applied loads
2. **Shear Force Diagram (SFD)**: Graph showing shear force distribution along the beam
3. **Bending Moment Diagram (BMD)**: Graph showing bending moment distribution along the beam

### 3.5 Analysis Report

The report includes:

- Summary of beam configuration
- Maximum shear force and its location
- Maximum bending moment and its location
- Critical points (zero shear force, maximum bending)
- ML prediction values and their accuracy

---

## 4. Beam Optimization Module

The Beam Optimization module suggests changes to improve beam performance based on specified criteria.

### 4.1 Input Parameters

Uses the same beam configuration parameters as the Analysis module, plus:

| Parameter | Description | Options |
|-----------|-------------|---------|
| Target Criterion | Optimization goal | "minimize_bending" or "minimize_shear" |

### 4.2 Optimization Strategies

The system explores several strategies to optimize the beam:

1. **Point Load Repositioning**: Moves individual point loads to reduce maximum forces
2. **UDL Adjustment**: Modifies the position and coverage of uniformly distributed loads

### 4.3 Interpreting Suggestions

For each suggestion, the system provides:

- Type of modification (reposition load or adjust UDL)
- Original and suggested parameters
- Expected improvement percentage
- Ranking of suggestions based on effectiveness

### 4.4 Implementation Considerations

When implementing suggestions:

- Consider practical limitations of the structural system
- Verify that suggested changes meet all safety requirements
- Validate significant changes with manual calculations
- Consider running the analysis again after applying suggestions

---

## 5. Machine Learning Training Module

The ML Training module allows you to train or retrain the prediction models using synthetic data.

### 5.1 Training Process

1. The system generates a synthetic dataset of beam configurations
2. Random Forest Regression models are trained for SFD and BMD prediction
3. Models are evaluated using RMSE and R² metrics
4. Trained models are saved for future use

### 5.2 Training Parameters

The training process uses:

- 2000 synthetic beam configurations
- 80% training / 20% testing split
- Random Forest with 100 estimators

### 5.3 Feature Importance

The ML models consider several key features:

- Beam length
- Number of point loads
- Total magnitude of point loads
- Average position of loads (weighted by magnitude)
- UDL parameters (start, end, value, coverage percentage)
- Total UDL force

### 5.4 When to Retrain

Consider retraining models when:

- Adding new types of beam configurations
- Accuracy metrics fall below acceptable thresholds
- Changing the range of input parameters
- After major software updates

---

## 6. Theoretical Background

### 6.1 Beam Theory Basics

The application applies fundamental principles from beam theory:

- Simply supported beams with fixed ends at positions 0 and L
- Linear elastic material behavior
- Small deflection theory
- Bernoulli-Euler beam assumptions

### 6.2 Shear Force and Bending Moment

- **Shear Force**: Internal force perpendicular to the beam axis
- **Bending Moment**: Internal moment causing beam curvature

The relationship between load (w), shear force (V), and bending moment (M) is:

```
dV/dx = -w
dM/dx = V
```

### 6.3 Calculation Method

The application uses direct integration and superposition:

1. For point loads: Step function change in shear force
2. For UDLs: Linear change in shear force
3. Bending moment calculated by integrating shear force

### 6.4 Machine Learning Approach

The ML models:

- Learn patterns between beam configurations and resulting maximum forces
- Use ensemble methods (Random Forest) to handle non-linearities
- Predict maximum values without calculating full diagrams
- Complement exact calculations with predictive capabilities

---

## 7. Relevant ISO Standards

### 7.1 ISO 2394 - General Principles on Reliability for Structures

**Description**: Establishes principles for the reliability of structures.

**Application in Software**:
- The optimization module follows reliability principles by prioritizing safety factors
- Calculation methods align with load effect determination procedures
- Uncertainty is addressed through comprehensive analysis reports

### 7.2 ISO 3010 - Basis for Design of Structures

**Description**: Provides basic requirements for structural design.

**Application in Software**:
- Beam configurations follow standard design principles
- Load representations (point loads, UDLs) conform to standard definitions
- Critical point identification follows established engineering practices

### 7.3 ISO 13822 - Assessment of Existing Structures

**Description**: Sets guidelines for assessment of existing structures.

**Application in Software**:
- Optimization module can be used for assessment of existing beams
- Analysis outputs provide data required for safety evaluation
- Comparative analysis capabilities support rehabilitation planning

### 7.4 ISO 22111 - Bases for Design of Structures - General Requirements

**Description**: Defines general requirements for structural design.

**Application in Software**:
- Load combinations follow standard practices
- Analysis methods conform to accepted engineering approaches
- Safety verification is supported through comprehensive output data

### 7.5 ISO/TR 14638 - Computational Structural Engineering - Model Validation

**Description**: Provides guidelines for validation of computational models.

**Application in Software**:
- ML model validation through RMSE and R² metrics
- Comparison between predicted and calculated values
- Model retraining capabilities for ongoing validation

### 7.6 ISO/IEC 25010 - Software Quality Models

**Description**: Defines quality characteristics for software products.

**Application in Software**:
- User interface design follows software quality principles
- Error handling implemented for input validation
- Performance metrics available for computational components

---

## 8. Troubleshooting

### 8.1 Common Input Errors

| Error | Possible Cause | Solution |
|-------|----------------|----------|
| "Invalid point loads format" | Syntax error in point loads input | Check syntax matches [(pos1, mag1), (pos2, mag2)] |
| Zero or negative beam length | Invalid beam length specified | Enter positive value for beam length |
| UDL end before start | UDL end position less than start position | Ensure UDL end > UDL start |

### 8.2 Calculation Issues

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| Unexpected maximum values | Loads positioned at beam end | Review load positions relative to supports |
| High prediction errors | Configuration outside training distribution | Retrain model with similar configurations |
| Graph visualization issues | Extreme load values | Scale load values or adjust plot settings |

### 8.3 ML Model Problems

| Problem | Possible Cause | Solution |
|---------|----------------|----------|
| Model file not found | Missing model files | Run training module to generate models |
| High RMSE values | Insufficient training data | Increase synthetic dataset size |
| Low R² scores | Complex configurations | Add more features or adjust model parameters |

---

## 9. Glossary

- **BMD**: Bending Moment Diagram
- **SFD**: Shear Force Diagram
- **UDL**: Uniformly Distributed Load
- **Critical Point**: Location of maximum shear force or bending moment
- **RMSE**: Root Mean Square Error, a measure of prediction accuracy
- **R²**: Coefficient of determination, indicates goodness of fit
- **Random Forest**: An ensemble ML algorithm used for regression
- **Feature Vector**: Set of parameters used for ML prediction

---

## 10. References

1. Timoshenko, S. P., & Gere, J. M. (1972). Mechanics of Materials. Van Nostrand Reinhold.
2. Hibbeler, R. C. (2018). Structural Analysis (10th ed.). Pearson.
3. Géron, A. (2019). Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow. O'Reilly Media.
4. International Organization for Standardization. (2015). ISO 2394:2015 - General principles on reliability for structures.
5. International Organization for Standardization. (2017). ISO 3010:2017 - Basis for design of structures.
6. International Organization for Standardization. (2010). ISO 13822:2010 - Assessment of existing structures.

---

*This user manual and ISO standards documentary complies with ISO/IEC/IEEE 26511:2018 - Systems and software engineering — Requirements for managers of information for users of systems, software, and services.*
