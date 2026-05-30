# Manufacturing Downtime & Yield Analysis using Qlik Sense

## Project Overview

The Manufacturing Downtime & Yield Analysis project is an end-to-end Business Intelligence solution developed using Qlik Sense to analyze production performance, machine downtime, yield efficiency, and operational losses in a manufacturing environment.

The project focuses on transforming raw manufacturing data into meaningful business insights through data profiling, cleansing, dimensional modeling, KPI engineering, and interactive dashboard development.

The primary objective is to help manufacturing stakeholders identify production bottlenecks, monitor machine performance, reduce downtime, improve yield, and support data-driven operational decision-making.

---

## Business Problem

Manufacturing organizations generate large volumes of operational data from production lines, machines, shifts, and downtime events. However, raw data often contains inconsistencies, duplicate records, missing values, invalid quantities, and inconsistent date formats, making reliable analysis difficult.

Key challenges addressed in this project include:

- Monitoring machine downtime across plants and production lines.
- Measuring production efficiency and yield performance.
- Identifying major downtime causes affecting productivity.
- Detecting data quality issues that impact reporting accuracy.
- Providing management with actionable insights through interactive dashboards.
- Enabling What-If analysis using dynamic threshold parameters.

---

## Project Objectives

- Analyze production performance across plants, machines, and shifts.
- Track machine downtime and identify major downtime contributors.
- Measure yield and scrap performance.
- Improve data quality through cleansing and validation.
- Build a scalable data model for manufacturing analytics.
- Create interactive dashboards for operational monitoring.
- Enable parameter-driven analysis for downtime and yield anomalies.

---

# Technology Stack

| Category | Tool |
|-----------|------|
| BI & Visualization | Qlik Sense |
| Data Transformation | Qlik Load Scripts |
| Data Modeling | Star Schema |
| Data Profiling | Qlik Sense |
| KPI Engineering | Qlik Expressions |
| Reporting | Interactive Dashboards |

---

# Dataset Overview

The project utilizes manufacturing operational data consisting of:

### Fact Tables

#### Production Batches
Contains production-related information including:

- Batch ID
- Plant ID
- Machine ID
- Shift ID
- Total Quantity
- Good Quantity
- Scrap Quantity
- Batch Start Time
- Batch End Time

#### Machine Downtime
Contains downtime event information including:

- Downtime ID
- Plant ID
- Machine ID
- Shift ID
- Downtime Reason
- Downtime Start Time
- Downtime End Time
- Downtime Duration

---

### Dimension Tables

#### Plants

Contains:

- Plant ID
- Plant Name
- State
- Region

#### Machines

Contains:

- Machine ID
- Machine Name
- Plant ID
- Production Line

#### Calendar

Contains:

- Date
- Month
- Quarter
- Year

#### Shift Calendar

Contains:

- Shift ID
- Shift Name
- Shift Start Time
- Shift End Time

#### Downtime Reason Dimension

Derived dimension table used for downtime categorization and analysis.

---

# Data Profiling & Quality Assessment

Before data cleansing, the dataset was thoroughly profiled to identify quality issues.

The following issues were discovered:

### Date and Time Issues

- Multiple date formats
- Inconsistent timestamp formats
- Invalid date sequences

### Quantity Issues

- Negative production quantities
- Missing quantity values
- Scrap quantity exceeding total quantity

### Downtime Issues

- Missing downtime durations
- Missing downtime reasons
- Invalid downtime timestamps

### Data Integrity Issues

- Duplicate Batch IDs
- Duplicate Downtime IDs
- Missing Plant IDs
- Missing Machine IDs
- Missing Shift IDs

### Data Model Issues

- Synthetic Keys
- Broken relationships
- Orphan records

---

# Data Cleaning & Transformation

The following data quality improvements were implemented using Qlik Load Scripts.

## Standardization

- Standardized all date and timestamp fields.
- Unified date format across all tables.
- Standardized missing value handling.

## Missing Value Treatment

The following values were replaced with a common business-friendly value:

- NULL
- Blank
- N/A
- UNKNOWN

All such values were standardized to:

UNKNOWN

This ensured:

- Consistent reporting
- Stable joins
- Preservation of fact records

---

## Quantity Validation

Business rule enforced:

Total Quantity = Good Quantity + Scrap Quantity

Actions performed:

- Missing quantities derived where possible.
- Invalid records flagged.
- Negative quantities converted to positive values.
- Data quality flags created.

---

## Downtime Validation

Actions performed:

- Derived downtime duration when missing.
- Standardized downtime timestamps.
- Created validation flags for invalid durations.
- Standardized downtime reasons.

---

## Deduplication

Duplicate records were removed using the latest created timestamp.

### Production Batches

- Before Deduplication: 10,200 records
- After Deduplication: 10,000 records

### Machine Downtime

- Before Deduplication: 18,180 records
- After Deduplication: 18,000 records

---

# Data Quality Flags

The following audit flags were created:

### improper_balance_flag

Identifies records where:

Total Quantity ≠ Good Quantity + Scrap Quantity

### scrap_gt_total_flag

Identifies records where:

Scrap Quantity > Total Quantity

### date_violation_flag

Identifies records where:

Start Timestamp > End Timestamp

These flags help preserve problematic records while maintaining transparency for data quality monitoring.

---

# Data Modeling

A dimensional model was created to support scalable manufacturing analytics.

## Fact Tables

- FactProductionBatches
- FactMachineDowntime

## Dimension Tables

- DimPlant
- DimMachine
- DimCalendar
- DimShift
- DimDowntimeReason

The model was designed to:

- Eliminate synthetic keys
- Maintain referential integrity
- Improve dashboard performance
- Enable flexible slicing and filtering

---

# KPI Engineering

The following business KPIs were developed.

## Total Production Quantity

Measures total units produced.

Formula:

Sum(total_qty)

---

## Good Quantity

Measures successful production output.

Formula:

Sum(good_qty)

---

## Scrap Quantity

Measures production waste.

Formula:

Sum(scrap_qty)

---

## Yield %

Measures production efficiency.

Formula:

(Sum(good_qty) / Sum(total_qty)) × 100

---

## Scrap %

Measures production loss.

Formula:

(Sum(scrap_qty) / Sum(total_qty)) × 100

---

## Downtime Minutes

Measures total machine downtime.

Formula:

Sum(downtime_minutes)

---

## Uptime %

Measures machine availability.

Formula:

((Scheduled Time - Downtime Time) / Scheduled Time) × 100

---

## OEE-Style Proxy

Measures overall operational effectiveness.

Formula:

Availability × Quality

Where:

Availability = Uptime %

Quality = Yield %

---

# Dashboards Developed

## Dashboard 1 – Executive Overview

Provides a high-level summary of manufacturing performance.

Includes:

- Total Production
- Good Quantity
- Scrap Quantity
- Yield %
- Uptime %
- OEE Proxy

---

## Dashboard 2 – Downtime Analysis

Focuses on machine downtime performance.

Includes:

- Downtime by Plant
- Downtime by Machine
- Downtime by Shift
- Downtime by Reason
- Top Downtime Contributors

---

## Dashboard 3 – Yield & Scrap Analysis

Analyzes production quality performance.

Includes:

- Yield Trends
- Scrap Trends
- Plant Comparison
- Machine Comparison
- Shift Comparison

---

## Dashboard 4 – What-If & Parameter Analysis

Provides interactive simulation capabilities.

Includes:

### Downtime Threshold Analysis

Users can dynamically define downtime thresholds and monitor:

- Downtime Events Above Threshold
- Machines Above Threshold
- Plants Above Threshold

### Yield Anomaly Threshold Analysis

Users can identify production batches that fall below expected yield levels.

---

# Key Business Outcomes

The solution enables manufacturing teams to:

- Monitor production efficiency in real time.
- Identify high-downtime machines.
- Detect yield losses early.
- Track scrap generation trends.
- Improve operational visibility.
- Support data-driven maintenance planning.
- Enhance manufacturing decision-making.


---

# Skills Demonstrated

- Data Profiling
- Data Cleaning
- Data Transformation
- ETL Development
- Data Validation
- Data Quality Framework Design
- Data Modeling
- KPI Engineering
- Manufacturing Analytics
- Business Intelligence
- Dashboard Development
- What-If Analysis
- Qlik Sense Development

