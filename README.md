# Multi-Agent Predictive Maintenance & Evaluation Framework

This project implements a robust evaluation pipeline for predicting the Remaining Useful Life (RUL) of aircraft engines using the NASA C-MAPSS dataset. It features a multi-agent benchmarking approach and automated validation logic to ensure the physical correctness of AI outputs.

## Project Overview

* Goal: Evaluate and benchmark multiple machine learning agents to predict engine failure.
* Dataset: NASA C-MAPSS (Turbofan Engine Degradation Simulation).
* Core Feature: A custom-built Analytical Validation Layer that flags impossible predictions (e.g., negative RUL) before they reach the dashboard.

## Technical Implementation

  * Data Processing: Handled large-scale sensor data using Python (Pandas & NumPy) and SQL.
  * Multi-Agent Benchmarking: Compared a Linear Regression agent against a Random Forest agent to determine which handles non-linear engine degradation more effectively.
  * Automated Correctness Logic: Implemented a `verify_outputs` function to perform "non-negative" and "reasonable range" checks on all model inferences.

## Performance & Evaluation
Following a "Go Concrete" approach, here are the validated results on the **FD001 test set**:

| Agent Model | R² Score | Mean Absolute Error (MAE) | Validation Status |
| :--- | :--- | :--- | :--- |
| **Linear Regression** | 0.4492 | 25.58 cycles | PASSED (with clipping) |
| **Random Forest** | 0.5789 | 20.26 cycles | PASSED |

## Key Decisions & Lessons Learned
* Handling Model Failure: During initial testing, the Linear Regression agent predicted negative RUL. I implemented a clipping logic layer using np.maximum(0, ...) to ensure outputs remained physically meaningful.
* Agent Selection: While Linear Regression was faster, the Random Forest agent provided a 20% improvement in accuracy and handled sensor noise more reliably.

## Repository Structure
* `Untitled-1.ipynb`: Core evaluation pipeline and validation scripts.
* `data/`: NASA C-MAPSS sensor data.
* `models/`: Serialized versions of the trained agents.
  



   Developed by a Mechanical Engineering student focusing on AI Reliability and Data Science.
