# Rocket Trajectory Simulation & Machine Learning

[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![Scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange.svg)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-Ensemble-green.svg)](https://xgboost.readthedocs.io/)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/amirachebied-svg/rocket-trajectory-ml/blob/main/rocket-trajectory-ml.ipynb)

## Overview

I built a simplified rocket-flight simulator and used it to generate data for a machine-learning experiment.

The main idea was to see how well machine-learning models could predict a rocket's maximum altitude from its design parameters.

I compared Linear Regression, Random Forest, and XGBoost, and also tested whether adding physics-based features could improve the predictions.

The project combines rocket physics, numerical simulation, feature engineering, machine learning, model evaluation, and error analysis.

## Main Results

| Metric | Result |
|--------|--------|
| Best Model | Random Forest + Physics Features |
| Best R² (5-fold CV) | 0.9749 |
| XGBoost R² | 0.9526 |
| XGBoost MAE | 544 m |
| Physics validation error | 0.285% |

## Why I Built It

I wanted to understand how rocket parameters affect flight performance and whether machine learning could learn part of this relationship.

Instead of starting with an existing dataset, I generated the data myself using the physics simulator. This gave me control over the rocket parameters and allowed me to test different configurations.

## Physics Simulation

The simulator models a simplified vertical rocket flight.

It includes:

- Gravity
- Changing atmospheric density with altitude
- Thrust
- Aerodynamic drag
- Fuel consumption
- Changing rocket mass during the burn

For each rocket configuration, the simulator calculates the maximum altitude reached.

I also compared the simulator with an analytical no-drag solution. The difference was about 0.285%, which gave me a basic check that the simulation was producing reasonable results.

## Dataset

I generated 1,000 different rocket configurations by varying:

- Thrust
- Initial mass
- Fuel mass
- Burn time
- Drag coefficient
- Reference area

The target variable is the maximum altitude produced by the simulation.

## Feature Engineering

I also created several physics-based features from the original parameters:

- Total impulse = Thrust × Burn Time
- Thrust-to-weight ratio (TWR)
- Mass ratio
- Effective drag area (CdA)

The goal was to give the models information that has a direct physical meaning.

## Machine Learning

I compared three models using 5-fold cross-validation.

| Model | Raw Features | + Physics Features |
|-------|--------------|--------------------|
| Linear Regression | 0.9015 | 0.9302 |
| Random Forest | 0.9451 | 0.9749 |
| XGBoost | — | 0.9526 |

The biggest improvement came from Random Forest after adding the physics-based features.

The best result was:

**Random Forest + Physics Features → R² = 0.9749**

XGBoost also performed well:

- R² = 0.9526
- MAE = 544 m

## Error Analysis

I looked at the prediction errors at different altitude ranges.

| Altitude Range | Mean Absolute Error |
|----------------|---------------------|
| Low (<10 km) | 305 m |
| Mid (10–20 km) | 801 m |
| High (>20 km) | 3,324 m |

The model was more accurate at lower altitudes and less accurate at higher altitudes.

One possible reason is that there are fewer high-altitude examples in the generated dataset.

## V-2 Case Study

I also tried the simulator with approximate historical parameters for the German V-2 rocket.

| Parameter | Value |
|-----------|-------|
| Simulated maximum altitude | 101,109 m |
| Historical maximum altitude | 206,000 m |
| Relative error | 50.9% |

The difference is large, but this was expected.

My simulator assumes a simplified vertical flight, while the real V-2 followed a ballistic trajectory and was affected by physical factors that are not included in the current model.

This showed me one of the main limitations of the simulation and also gave me ideas for improving it later.

## Verification and Debugging

One of the problems I found during testing was that some rockets were still climbing when the simulation stopped.

In the first version, 232 out of 1,000 rockets were affected.

I extended the simulation after fuel burnout so that the rockets had enough time to reach their actual maximum altitude.

After this correction, none of the 1,000 simulations were stopped while the rocket was still climbing.

This was an important part of the project because the machine-learning results depend directly on the quality of the simulated data.

## Limitations

This is a simplified educational simulation, not a high-fidelity rocket simulator.

Some limitations are:

- Only vertical flight is simulated
- Launch angle is not included
- Gravity is treated as constant
- The drag coefficient does not change with Mach number
- Wind is not modeled
- Coriolis effects are not included
- No multi-stage rockets
- The dataset is generated by simulation rather than real flight measurements

Because of these limitations, the ML models should not be treated as replacements for professional rocket-flight simulations.

## Future Work

Some improvements I would like to explore are:

- 2D or 3D trajectories
- Launch-angle optimization
- More realistic atmospheric and drag models
- Real rocket-flight data
- Physics-Informed Neural Networks (PINNs)
- Reinforcement learning for trajectory optimization
- More machine-learning models and ensemble methods

## Tools

- Python
- NumPy
- Pandas
- Matplotlib
- Scikit-learn
- XGBoost
- Google Colab

## Project Structure

`rocket-trajectory-ml.ipynb`

The notebook contains the simulation, dataset generation, feature engineering, machine-learning experiments, evaluation, error analysis, V-2 case study, and debugging.

## AI Assistance

I used AI tools as a supporting resource during the project, mainly for occasional debugging help, implementation ideas, and understanding some coding problems.

I designed the project, ran the experiments, checked the results, and made the final decisions about the methods and analysis.

## Project Report

A complete written report is available in this repository:

[**Rocket_AI_Project_Report.pdf**](./Rocket_AI_Project_Report.pdf)

The report includes:

- Executive summary
- Detailed methodology
- Results and model comparison
- Error analysis by altitude regime
- V-2 case study
- Limitations and future work
## Author

Amira Chebieb

GitHub: [@amirachebied-svg](https://github.com/amirachebied-svg)
