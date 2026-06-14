# ⚡ Degradation-Aware MPC for a Freiburg Renewable District Microgrid 🇩🇪

### PV • BESS • EV Charging • Heat-Pump Flexibility • AC Grid Validation • Battery Aging

![Project Thumbnail](thumbnail.png)

---

## 🌍 Project Overview

This project presents a **degradation-aware Model Predictive Control (MPC)** framework for a representative **renewable district microgrid in Freiburg, Germany**.

The system coordinates:

* ☀️ Solar PV generation
* 🌬️ Wind generation
* 🔋 Battery Energy Storage System (BESS)
* 🚗 EV charging and V2G-style flexibility
* 🏠 Heat-pump demand flexibility
* ⚡ Grid import and export
* 📉 Dynamic electricity price response
* 🌱 Carbon-aware dispatch
* 🔌 Feeder congestion and voltage validation
* 🧠 Rainflow-based battery aging analysis

The goal is to operate a German renewable district more intelligently by reducing **energy cost, CO₂ emissions, peak grid import, battery degradation, voltage violations, and feeder congestion**.

---

## 🇩🇪 Why This Project Is Relevant to Germany

Germany is rapidly transforming its energy system through the **Energiewende**, with strong emphasis on:

* renewable energy integration,
* distributed solar PV,
* battery storage,
* electric mobility,
* heat-pump electrification,
* smart grids,
* grid congestion management,
* carbon reduction,
* digital energy management.

This project is designed around a **Freiburg-based renewable district microgrid**, making it highly relevant to German MSc programs in:

* Renewable Energy Systems
* Smart Grid Engineering
* Energy Management
* Electrical Power Engineering
* Sustainable Energy Technologies
* E-Mobility and Grid Integration
* Battery Storage and Power Electronics

---

## 🎯 Research Question

> How can degradation-aware MPC coordinate PV, BESS, EV charging, heat-pump flexibility, and grid-supportive operation to reduce operating cost, emissions, peak grid import, voltage violations, feeder congestion, and battery aging in a German renewable district microgrid?

---

## 🧠 What Is MPC?

**Model Predictive Control (MPC)** is an optimization-based control strategy that looks ahead into the future and decides the best control action now.

In this project, the MPC forecasts:

* future solar generation,
* load demand,
* EV availability,
* battery state of charge,
* electricity price,
* carbon intensity,
* feeder constraints,
* voltage limits.

Then it decides:

* when to charge or discharge the battery,
* when to charge EVs,
* when to use heat-pump flexibility,
* when to import/export electricity,
* when to reduce peak demand,
* how to protect battery health.

---

## 🏗️ System Architecture

```text
             ┌─────────────────────────────┐
             │   Real Freiburg Weather     │
             │   NASA POWER / PVGIS Style  │
             └──────────────┬──────────────┘
                            │
                            ▼
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Solar PV     │     │ Wind Power   │     │ Load Demand  │
│ Forecast     │     │ Forecast     │     │ Forecast     │
└──────┬───────┘     └──────┬───────┘     └──────┬───────┘
       │                    │                    │
       └────────────────────┼────────────────────┘
                            ▼
              ┌──────────────────────────┐
              │  Degradation-Aware MPC   │
              │  Optimization Controller │
              └─────────────┬────────────┘
                            │
        ┌───────────────────┼───────────────────┐
        ▼                   ▼                   ▼
 ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
 │ BESS        │     │ EV Charging │     │ Heat Pump   │
 │ Control     │     │ / V2G       │     │ Flexibility │
 └──────┬──────┘     └──────┬──────┘     └──────┬──────┘
        │                   │                   │
        └───────────────────┼───────────────────┘
                            ▼
              ┌──────────────────────────┐
              │ Grid Validation Layer    │
              │ pandapower + OpenDSS     │
              └──────────────────────────┘
```

---

## 🔋 Core Technical Features

| Feature                  | Description                                                |
| ------------------------ | ---------------------------------------------------------- |
| ☀️ Real Freiburg Weather | Uses location-based irradiance, temperature, and wind data |
| 🧠 MPC Optimization      | Rolling-horizon control for smart energy scheduling        |
| 🔋 BESS Dispatch         | Battery charge/discharge optimization                      |
| 🚗 EV Charging           | EV flexibility and mobility-aware control                  |
| 🏠 Heat Pump             | Flexible electrified heating demand                        |
| 🌱 Carbon-Aware Dispatch | Reduces grid import during high-carbon periods             |
| ⚡ Peak Reduction         | Limits high grid import during evening demand peaks        |
| 🔌 Feeder Validation     | Checks voltage and line loading                            |
| 🧪 pandapower AC Flow    | Balanced AC power-flow validation                          |
| 🔁 OpenDSS Validation    | Optional unbalanced three-phase feeder analysis            |
| 📉 Rainflow Aging        | Battery degradation using SOC cycle counting               |
| 🚨 SCADA Alarms          | Operational warning and alarm dashboard                    |
| 📦 Output Packaging      | Saves CSV, Excel, HTML dashboards, and ZIP results         |

---

## 📊 Compared Control Cases

This project compares five operating strategies:

| Case                                     | Description                                         |
| ---------------------------------------- | --------------------------------------------------- |
| 1. No Flexibility                        | No battery or EV optimization                       |
| 2. Rule-Based BESS                       | Simple charge/discharge logic                       |
| 3. Cost-Only MPC                         | Minimizes energy cost only                          |
| 4. Degradation-Aware MPC                 | Includes battery aging penalty                      |
| 5. Grid-Supportive Degradation-Aware MPC | Adds frequency-supportive and feeder-aware behavior |

---

## 🧮 MPC Objective Function

The optimization minimizes a combined cost function:

```text
Total Cost =
Grid Import Cost
- Export Revenue
+ Carbon Cost
+ Battery Degradation Cost
+ Load Shedding Penalty
+ Heat Shortfall Penalty
+ EV Mobility Shortfall Penalty
+ Renewable Curtailment Penalty
```

The controller balances economics, sustainability, battery health, and grid reliability.

---

## 🔬 Validation Layers

### 1️⃣ Linearized Feeder Validation

A fast approximate feeder model checks:

* minimum voltage,
* maximum voltage,
* line loading,
* transformer loading,
* feeder congestion.

### 2️⃣ pandapower AC Validation

A balanced AC power-flow model validates:

* LV bus voltages,
* transformer loading,
* line loading,
* grid import/export feasibility.

### 3️⃣ OpenDSS Unbalanced Validation

Optional OpenDSS validation checks:

* unbalanced three-phase operation,
* phase-specific load distribution,
* distributed PV injection,
* feeder voltage behavior.

---

## 🔋 Battery Degradation Analysis

Battery aging is estimated using:

* energy throughput,
* equivalent full cycles,
* rainflow cycle counting,
* depth-of-discharge behavior,
* temperature correction,
* state-of-health estimation,
* degradation cost approximation.

This makes the controller more realistic than a simple battery dispatch model.

---

## 📈 Main Outputs

The project generates:

* 📄 `input_and_forecast_data_real_freiburg.csv`
* 📄 `all_case_dispatch_grid_ac_opendss_results.csv`
* 📄 `main_case_grid_supportive_results.csv`
* 📄 `baseline_kpi_comparison.csv`
* 📄 `rainflow_battery_degradation_by_case.csv`
* 📄 `pandapower_ac_validation_results.csv`
* 📄 `opendss_unbalanced_validation_results.csv`
* 📄 `scada_alarm_log.csv`
* 📊 HTML dashboards
* 📘 Excel summary workbook
* 📦 zipped output folder

---

## 📌 Key Performance Indicators

The model evaluates:

| KPI                   | Meaning                                  |
| --------------------- | ---------------------------------------- |
| Net Energy Cost       | Total import cost minus export revenue   |
| Grid Import           | Energy imported from external grid       |
| Grid Export           | Renewable surplus exported               |
| CO₂ Emissions         | Carbon impact of grid import             |
| Peak Import           | Maximum grid dependency                  |
| Renewable Utilization | Share of available renewable energy used |
| Self-Sufficiency      | Share of demand met locally              |
| Battery SOH           | Estimated battery health                 |
| Rainflow Cycles       | Battery aging cycle count                |
| Voltage Violations    | Grid voltage limit violations            |
| Congestion Hours      | Feeder overload events                   |
| Load Shedding         | Unserved demand                          |
| Grid Support Hours    | Hours of support mode activation         |

---

## 🖼️ Example Visual Outputs

### ⚡ Dispatch Dashboard

```text
PV Generation + Wind + BESS + EV + Grid Import
```

### 🔋 Battery SOC and Rainflow Aging

```text
Battery SOC profile + charge/discharge cycles + aging estimate
```

### 🔌 Grid Validation

```text
pandapower voltage profile + feeder loading + OpenDSS unbalanced check
```

### 🚨 SCADA Alarm Console

```text
Voltage alarms + congestion alerts + low SOC warnings
```

---

## 🛠️ Technologies Used

| Tool                          | Purpose                               |
| ----------------------------- | ------------------------------------- |
| Python                        | Main simulation language              |
| NumPy                         | Numerical modeling                    |
| Pandas                        | Data processing                       |
| SciPy                         | Linear optimization                   |
| Plotly                        | Interactive dashboards                |
| pandapower                    | AC power-flow validation              |
| OpenDSSDirect.py              | Optional unbalanced feeder validation |
| rainflow                      | Battery cycle-counting degradation    |
| NASA POWER / PVGIS-style data | Freiburg weather and renewable input  |
| Google Colab                  | Cloud-based execution                 |

---

## 🚀 How to Run in Google Colab

1. Open the notebook in Google Colab.
2. Set the simulation length:

```python
SIMULATION_DAYS = 7
```

or for a longer study:

```python
SIMULATION_DAYS = 30
```

3. Run all cells.
4. The notebook will generate:

   * plots,
   * tables,
   * Excel results,
   * CSV files,
   * HTML dashboards,
   * zipped output package.

---

## 📁 Suggested Repository Structure

```text
degradation-aware-mpc-freiburg-microgrid/
│
├── README.md
├── notebooks/
│   └── EnergieQuartier_MPC_Extended.ipynb
│
├── reports/
│   ├── IEEE_Project_Report_Oihika_Arpit.pdf
│   └── IEEE_Project_Report_Oihika_Arpit.docx
│
├── outputs/
│   ├── baseline_kpi_comparison.csv
│   ├── rainflow_battery_degradation_by_case.csv
│   ├── pandapower_ac_validation_results.csv
│   └── scada_alarm_log.csv
│
├── figures/
│   ├── thumbnail.png
│   ├── dispatch_dashboard.png
│   ├── battery_soc_rainflow.png
│   ├── ac_validation.png
│   └── scada_alarms.png
│
└── requirements.txt
```

---

## 📦 Requirements

```text
numpy
pandas
scipy
plotly
openpyxl
tabulate
kaleido
requests
rainflow
pandapower
opendssdirect.py
```

Install with:

```bash
pip install numpy pandas scipy plotly openpyxl tabulate kaleido requests rainflow pandapower opendssdirect.py
```

---

## 🧪 Research Contribution

This project contributes an applied simulation framework that connects:

* renewable energy forecasting,
* predictive control,
* battery degradation modeling,
* EV and heat-pump flexibility,
* grid validation,
* carbon-aware operation,
* German district-energy relevance.

The project is intentionally designed to be more than a basic PV-battery simulation. It combines energy management, power-system validation, and degradation-aware optimization in one integrated workflow.

---

## 🎓 Relevance for MSc Renewable Energy in Germany

This project demonstrates practical readiness for German MSc programs because it connects academic and industry-relevant themes:

* renewable generation integration,
* decentralized energy systems,
* battery storage optimization,
* smart grid control,
* grid congestion reduction,
* EV charging infrastructure,
* heat-pump electrification,
* carbon-aware operation,
* distribution-grid validation,
* Python-based energy analytics.

It is especially relevant for programs focused on:

* Renewable Energy Engineering
* Energy Systems
* Smart Grids
* Electrical Power Engineering
* Sustainable Energy Technologies
* E-Mobility
* Energy Informatics
* Power System Optimization

---

## 🔮 Future Work

Future extensions may include:

* German standard load profiles,
* real DWD weather data,
* real Freiburg feeder topology,
* PyPSA integration,
* stochastic MPC,
* robust MPC,
* inverter current-limit modeling,
* reactive power capability curves,
* transformer thermal aging,
* tariff sensitivity analysis,
* multi-season annual simulation,
* hydrogen storage comparison.

---

## 👩‍💻 Author

**Oihika Arpit**
Electronics and Communication Engineering Background
Renewable Energy Systems | Smart Grid | Battery Storage | Energy Optimization

---

## ⭐ Project Tagline

> A Freiburg-focused smart microgrid simulation combining predictive control, renewable integration, battery health protection, and grid validation for Germany’s clean-energy transition.

---

## 📌 Recommended Repository Name

```text
degradation-aware-mpc-freiburg-microgrid
```

---

## 📌 Recommended GitHub Description

```text
Degradation-aware MPC for a Freiburg renewable microgrid with PV, BESS, EV charging, heat pumps, AC validation, OpenDSS checks, and rainflow battery aging.
```
