# Dynamics of static stall – flow over a 2D flat plate at low Reynolds number

Bachelor thesis, B.E. Mechanical Engineering, The National Institute of Engineering (NIE), Mysuru, 2020–21. Team of 4: D Ashrith, Shashank S S, Sumanth C T, Venkatesha T E. Guide: Mr. P Srinag, Assistant Professor.

**My role:** team lead. I generated the mesh, did the MATLAB analysis of the lift signals (FFT, wavelet, recurrence) and interpreted the results, and wrote the report.

Full report: `Dynamic of Static Stall - Final Report.pdf`

## Question

How does the flow over a thin flat plate change from steady to chaotic as the angle of attack increases, and where does stall set in? We simulated the plate in ANSYS Fluent at angles of attack from 0° to 32.5° and analysed the lift signals with time-series and dynamical-systems methods.

## Setup

| Parameter | Value |
|---|---|
| Flow | 2D, incompressible, unsteady, laminar (no turbulence model) |
| Solver | ANSYS Fluent, double precision, 8 parallel processes |
| Free-stream velocity | 0.148 m/s (air), Re ≈ 1000 based on chord |
| Plate | 10 cm chord × 0.2 cm thickness |
| Mesh | Overset plate mesh in a circular background mesh (radius 12 chords), about 202,000 nodes |
| Angles of attack | 0° to 32.5° |
| Time step | 0.003 s, 100,000 steps, 20 iterations per step |

The report calls this setup DNS: at Re ≈ 1000 the flow is laminar, so the unsteady Navier–Stokes equations are solved directly without a turbulence model.

## Results

| Angle of attack | Flow behaviour |
|---|---|
| 0°–9° | Steady, two stable shear layers, no shedding |
| 10°–20.5° | Periodic vortex shedding |
| 20.5°–22° | Quasi-periodic, transition begins |
| 23°–25° | Chaotic; lift jumps from 22° to 23° and drops sharply from 24° to 25° |

- Stall occurs between 24° and 25°.
- At 26°–27° the flow is still unsteady.
- The lift-coefficient trend was compared with published data for a 5 %-thick flat plate and for NACA 0012 at similar Reynolds numbers (Mittal; Durante et al.). The airfoil data are a different shape, so this checks the trend, not the values.

## Analysis methods

Applied to the lift-coefficient time series in MATLAB:

- **Recurrence quantification analysis (RQA):** determinism falls from 99.4 % at 15° to 97.9 % at 22° and 93.6 % at 25°, confirming the move toward chaos.

  | AoA | Embedding dim. | Delay | Recurrence rate | Determinism |
  |---|---|---|---|---|
  | 15° | 3 | 86 | 10.22 % | 99.40 % |
  | 22° | 3 | 90 | 6.62 % | 97.86 % |
  | 25° | 3 | 210 | 5.40 % | 93.58 % |

- **Fast Fourier transform (FFT):** dominant shedding frequencies
- **Continuous wavelet transform:** how frequency content changes over time
- **Empirical mode decomposition and Hilbert-Huang transform:** instantaneous frequency and energy of the non-stationary signals
- **Q-criterion:** vortex identification at the leading and trailing edges

## Files

- `Dynamic of Static Stall - Final Report.pdf` – full thesis with setup, validation, vortex plots and time-series analysis

## Key references

- Anderson, J. D. (2003). *Fundamentals of Aerodynamics.*
- Liu, Y. et al. (2012). Numerical bifurcation analysis of static stall of airfoil.
- Durante, D. et al. (2020). Bifurcations and chaos transition in the flow over an airfoil at low Reynolds number.
- Huang, N. E. et al. (1998). The empirical mode decomposition and the Hilbert spectrum for nonlinear and non-stationary time series analysis.
- Eckmann, J. P. et al. (1987). Recurrence plots of dynamical systems.

Submitted in partial fulfilment of the B.E. in Mechanical Engineering, NIE Mysuru (2020–21).
