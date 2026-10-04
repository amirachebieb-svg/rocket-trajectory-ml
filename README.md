# Rocket Trajectory Simulation & Machine Learning Prediction

A physics-based vertical rocket flight simulator and a Random Forest model that predicts maximum altitude from six design parameters.

## Simulator
- Vertical flight with constant gravity, altitude-dependent air density, thrust, aerodynamic drag and fuel burn
- Validated against the analytical no-drag solution (rocket equation): 69,073.6 m vs 69,270.8 m, a 0.285% difference
- Verification caught a bug: flights were cut 30 s after burnout, so 232 of 1,000 rockets were still climbing. The cutoff was extended to 600 s after burnout and all results were recomputed (0 of 1,000 truncated)

## Data and model
- 1,000 random rockets: thrust 30-70 kN, initial mass 800-1200 kg, fuel 250-450 kg, burn time 15-25 s, drag coefficient 0.3-0.7, reference area 0.8-1.2 m2
- Target: maximum altitude from the simulator
- Physics-derived features: impulse (thrust x burn time), thrust-to-weight ratio, mass ratio, drag area (Cd x A)

## Results (5-fold cross-validation, R2)
| Model | Raw features | + Physics features |
|---|---|---|
| Linear Regression | 0.9015 | 0.9302 |
| Random Forest | 0.9451 | 0.9749 |

- Random Forest on 200 held-out rockets: mean absolute error 6.3%
- Prediction takes 0.11 s vs 1.03 s for re-running the simulator on the same 200 rockets

## Limitations
- Data comes from a simplified simulator, not real flights
- Vertical flight only, with constant thrust and gravity
- The simulator is already fast (about 5 ms per rocket), so the model is a surrogate that demonstrates the idea, not a replacement

## Tools
Python, NumPy, Pandas, Matplotlib, scikit-learn, Google Colab
