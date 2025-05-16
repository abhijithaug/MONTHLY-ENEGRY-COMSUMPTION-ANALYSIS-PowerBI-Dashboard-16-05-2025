# MONTHLY-ENEGRY-COMSUMPTION-ANALYSIS-PowerBI-Dashboard-16-05-2025


# 📊 Power BI Dashboard: Monthly Energy Consumption Analysis



##  Overview

This Power BI dashboard provides an in-depth analysis of **Monthly Energy Consumption** using sensor-based data that includes appliance energy usage, temperature, humidity, weather conditions, and light consumption. The primary goal is to monitor, analyze, and visualize patterns that can drive energy efficiency and consumption awareness.

---

## Project Structure

### 🔹 Layer 1: Data Loading
- Source: SQL Server / CSV File
- Tables loaded: Energy sensor data (`Appliances`, `Lights`, `Temp`, `Humidity`, `Weather`, `DateTime`)

### 🔹 Layer 2: Data Cleaning
- Missing values handled
- Data types converted
- Time-based features extracted: `Hour`, `Day`, `Month`, `TimeBin`
- Created custom DAX measures for KPIs and aggregations

---


###  Target Variable
- **Appliances** – Energy usage in watt-hours (Wh)

###  Key Features
- **Temperature**: T1–T9 (indoor), T_out (outdoor)
- **Humidity**: RH_1–RH_9 (indoor), RH_out (outdoor)
- **Weather**: Pressure, Windspeed, Visibility, Dew Point
- **Lighting**: Separate column `Lights`
- **Datetime**: Used for time binning and temporal analysis

---

## Dashboard Visualizations

###  KPI Cards
- Total Energy Used (kWh)
- Average Daily Energy
- Max Daily Energy
- Total Appliance Usage
- Total Lights Usage
- % of Energy by Lights
- Weekday & Hourly Average Energy
- Avg Indoor Temperature (°C)
- Avg Indoor Humidity (g/m³)

### Graphs and Charts
- Month-wise Energy Consumption (Appliances & Lights)
- Energy Usage by Weekday
- Inside vs Outside Temperature Comparison
- Indoor vs Outdoor Relative Humidity Trends
- Monthly Outdoor Temp & RH vs Pressure
- Energy Usage by Time Bin: Morning, Afternoon, Evening, Night
- Windspeed by Time of Day
- Treemap: Monthly Appliance Usage

---

## DAX Highlights

Example measures used in the dashboard:

```DAX
Avg Indoor Temp = 
AVERAGEX(
    'Data',
    DIVIDE(
        'Data'[T1] + 'Data'[T2] + ... + 'Data'[T9], 
        9
    )
)

TimeBin = 
SWITCH(
    TRUE(),
    HOUR('Data'[date]) >= 6 && HOUR('Data'[date]) < 12, "Morning (6–12)",
    HOUR('Data'[date]) >= 12 && HOUR('Data'[date]) < 18, "Afternoon (12–18)",
    HOUR('Data'[date]) >= 18 && HOUR('Data'[date]) < 24, "Evening (18–24)",
    "Night (0–6)"
)
