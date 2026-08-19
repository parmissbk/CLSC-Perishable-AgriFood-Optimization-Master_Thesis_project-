# 🌱 CLSC-Perishable-AgriFood-Optimization

**A Sustainable Closed-Loop Supply Chain Model for Perishable Agri-Food Products under Demand Uncertainty**

![GAMS](https://img.shields.io/badge/GAMS-MILP%2FMINLP-blue)
![Solver](https://img.shields.io/badge/Solver-CPLEX%20%2F%20BARON-orange)
![Status](https://img.shields.io/badge/Status-Demo%20%2F%20Sample-lightgrey)
![License](https://img.shields.io/badge/License-MIT-green)

> ⚠️ **Note:** This repository is a **sanitized, sample version** of my M.Sc. thesis project. The original thesis used real-world demand and network data from the Tehran metropolitan area; the data included here is **synthetic** and intended only to demonstrate the model's logic and structure.

---

## 📖 Overview

This project presents an optimization model for reducing waste and cost in the supply chain of **perishable agricultural products** under **uncertain demand**. It was developed as part of my M.Sc. thesis in Industrial Engineering (Supply Chain), graded **19.5/20 (A+)**.

The model simultaneously optimizes three decision layers that are usually treated separately in the literature:

| Layer | What it does |
|---|---|
| 🚚 **Fleet Routing** | Multi-period, multi-product vehicle routing across distribution centers |
| 📦 **Age-Based Inventory Control** | Tracks product age/shelf-life to minimize decay-related losses |
| ♻️ **Reverse Logistics** | Routes waste/degraded products back to recycling facilities (circular economy) |

## 🗺️ Case Study

The full thesis validated the model on a real distribution network across **22 municipal districts of Tehran**, spanning farms (suppliers) → distribution centers → retailers/customers, with a reverse flow to recycling facilities.

<p align="center">
  <img src="results/figures/network_overview_sample.png" width="45%" />
  <img src="results/figures/supply_chain_process_sample.png" width="45%" />
</p>

*(Sample illustrations only — see `docs/thesis_summary.pdf` for the full figures.)*

## 🧮 Methodology

- **Model type:** Mixed-Integer Linear/Non-Linear Programming (MILP/MINLP)
- **Solvers:** CPLEX / BARON (Branch-and-Bound / Branch-and-Cut)
- **Implementation:** GAMS

**Objective function** minimizes total supply chain cost, combining:
1. Fixed & variable routing/transportation costs
2. Inventory holding costs at distribution centers
3. Stockout / penalty costs
4. Age-dependent product decay costs
5. Reverse logistics & recycling costs

```
Z = min [ R + N ]
```
where `R` is total routing cost and `N` is the total penalty/degradation cost (see `model/main_model.gms` for the full formulation).

## 📊 Key Results (from the original thesis)

- **Seasonality effect:** costs peak in **summer** (heat → faster decay → higher cold-chain costs) and are lowest in **winter**.
- **Geographic hotspots:** districts **4, 5, and 15** consistently account for the largest share of network costs.
- **Demand sensitivity:** a ±10% demand shock produces a **strictly linear** cost response — confirming model stability.
- **Shelf-life trade-off:** raising the allowable product age threshold from B=3 to B=5 reduces decay risk but **increases holding costs**.

<p align="center">
  <img src="results/figures/seasonal_cost_sample.png" width="60%" />
</p>

*(Chart generated from sample data — trend mirrors the real thesis results.)*

## 📁 Repository Structure

```
CLSC-Perishable-AgriFood-Optimization/
├── model/            # GAMS model files (sets, parameters, objective, constraints)
├── data/sample_data/ # Synthetic demand & network data
├── results/          # Sample outputs and figures
├── docs/             # Thesis summary (abstract-level, non-confidential)
└── notebooks/        # Optional: Python scripts to visualize GAMS output
```

## ▶️ How to Run

1. Install [GAMS](https://www.gams.com/) with a CPLEX or BARON license (or use the free demo solver for small instances).
2. Clone this repo:
   ```bash
   git clone https://github.com/<your-username>/CLSC-Perishable-AgriFood-Optimization.git
   ```
3. Open `model/main_model.gms` in GAMS Studio and run it — it will read the sample data from `data/sample_data/`.
4. Outputs (routes, inventory levels, costs) are written to `results/sample_output.csv`.

## 🎓 About

This work was completed as my M.Sc. thesis at the **Department of Industrial Engineering, University of Science & Culture**, under the supervision of **Prof. Rashed Sahraeian**.

📧 Contact: parmissaboktakin@gmail.com

## 📄 License

This sample code is released under the MIT License — see [LICENSE](LICENSE) for details. The underlying research and thesis document remain the intellectual property of the author and university.
