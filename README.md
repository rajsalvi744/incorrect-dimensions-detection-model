# Incorrect Package Dimensions Detection Model

## Overview
This project focuses on developing a detection model to identify consignments with potentially incorrect package dimensions. The model leverages various business rules and interquartile range (IQR) analyses to flag outliers at both the client and industry levels.

## Objectives
- To detect consignments with incorrect dimensions or weight based on predefined logics.
- To build models that classify consignments as outliers based on the number of violated logics.
- To improve package dimension data accuracy for logistics operations.

## Dataset Description
The project uses two primary datasets:

1. **Consignment Details**:
   - Key Columns: `consignment_id`, `created_date`, `cnote` (unique ID), `client_id`, `weight`, `volume`, `total_box`, `industry`, `CFT` (weight/volume).

2. **Package Dimensions**:
   - Key Columns: `consignment_id`, `length`, `breadth`, `height`, `unit`, `no. of boxes`.

## Logics for Flagging Consignments
1. **Client-Level CFT IQR**: Flag consignments where the `CFT` is outside the interquartile range (IQR) calculated at the client level.
2. **Industry-Level CFT IQR**: Flag consignments where the `CFT` is outside the IQR calculated at the industry level.
3. **Length IQR**: Flag consignments where the `length` exceeds the IQR calculated at the client level.
4. **Weight IQR**: Flag consignments where the `weight` exceeds the IQR calculated at the client level.
5. **Preferred Unit Violation**: Flag consignments where the `unit` used is not the client’s preferred measurement unit.
6. **1x1x1 Dimensions**: Flag consignments where all dimensions (`length`, `breadth`, `height`) are recorded as 1x1x1, indicating potential erroneous data entry.

## Model Definitions
Three models were developed to classify consignments based on the number of violated logics:

1. **Model 1**:
   - Flags consignments marked as outliers for at least one logic.

2. **Model 2**:
   - Flags consignments marked as outliers for at least two logics.

3. **Model 3**:
   - Flags consignments marked as outliers for at least three logics.

## Workflow
1. **Data Preparation**:
   - Merged consignment details and package dimensions data.
   - Calculated CFT and other metrics necessary for IQR computations.

2. **IQR Calculations**:
   - Computed IQR for `CFT`, `length`, and `weight` at client and industry levels.

3. **Logic Implementation**:
   - Applied the six logics to flag outliers.
   - Recorded the flagged consignments for each logic.

4. **Model Evaluation**:
   - Counted flagged consignments for each client and assigned them to the appropriate model based on the number of violated logics.

## Results
- Model 1 identified 43679 consignments out of 149487 as outliers.
- Model 2 identified 8435 consignments out of 149487 as outliers.
- Model 3 identified 1064 consignments out of 149487 as outliers.

## Recommendations
- Focus on consignments flagged under multiple logics for targeted data correction.
- Automate the flagging process for real-time detection of incorrect dimensions.
- Train staff to ensure accurate entry of package dimensions.

## Files in the Repository
- **D1_IQR_Analysis.xlsx**: Contains IQR calculations and flagged consignments based on individual logics.
- **D2_Model.xlsx**: Contains model-based classifications and client-level summaries.

## Future Scope
- Extend the model to include more sophisticated statistical methods for anomaly detection.
- Integrate with a live system to flag incorrect dimensions in real-time.
- Analyze the impact of detected errors on logistics costs and operational efficiency.

