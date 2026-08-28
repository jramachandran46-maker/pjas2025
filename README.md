# pjas2025- For FULL EXPLANATION SEE FILES "PRESENTATION" and "RESEARCH PAPER"

Independent research project investigating whether particles carried by convection currents in boiling water exhibit chaotic motion — specifically, whether their trajectories form a strange attractor in phase space.

Pennsylvania Junior Academy of Science, 2025: 1st Place, Physics Category, plus state-level special honors.

The Experiment

A red tracer particle (a seed) was released into a container of boiling water and filmed simultaneously by two cameras — one facing the front of the container, one facing the side — so its full 3D motion could be reconstructed from two 2D views. Multiple trials were recorded (11 runs per view).

The analysis pipeline turns raw video into phase-space trajectories:

Particle tracking (particletracking.py) — OpenCV color tracking isolates the red particle in each frame, sampling at 6 Hz. Pixel coordinates are converted to centimeters using a measured calibration reference (1070 px = 15.75 cm), with a fixed physical origin.
Velocity computation (nvelocity.py) — central-difference differentiation of position (forward/backward differences at the endpoints).
Outlier removal (outliers.py) — IQR-based filtering on the velocity components to reject tracking glitches.
View combination (ScienceProject/input/src/combination.py) — merges the front and side camera data into full 3D trajectories.
Analysis & visualization:
Visualization.py — 3D phase-space plots of the combined trajectories across all trials
autocorrelation.py — autocorrelation of velocity time series (a signature test: chaotic signals decorrelate)
fouriertransform.py — frequency spectrum of the motion (broadband spectra indicate chaos; sharp peaks indicate periodicity)
Repository Layout
Main.py                     batch pipeline: track every trial video → clean → CSV
particletracking.py         OpenCV tracker + pixel→cm calibration (in ScienceProject/)
particletracking2.py        tracker variant
nvelocity.py                central-difference velocity
outliers.py                 IQR outlier filter
Visualization.py            3D phase-space plotting
autocorrelation.py          autocorrelation analysis
fouriertransform.py         FFT / frequency-spectrum analysis
pixeltrackingutil.py        tracking utilities
ScienceProject/
  input/src/datafront/      processed CSVs, front camera (11 trials)
  input/src/dataside/       processed CSVs, side camera (11 trials)
  input/src/combination.py  front+side → 3D trajectory merge
  *.png                     phase-space plot outputs

Each processed CSV contains: frame, timestamp, x_cm, y_cm, x_velocity_cm_per_s, y_velocity_cm_per_s.

Findings

Full methodology, results, and discussion are in the accompanying research paper and presentation (see resume/links). In brief, the phase-space reconstructions and spectral analysis were used to assess whether the particle motion is chaotic rather than periodic or random.
