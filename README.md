# Emergent scalar field from geometry: coherent vortices and energy localization

**Author:** Ramyar Azar
**Last updated:** November 26, 2025  

This repository contains a working implementation of an **emergent scalar field** built directly from geometric gradients on a time-evolving four-dimensional hyperspherical spacetime.  

The code here corresponds to the scalar-field case study on my modeling website and serves both as a **demonstration of methods** and as a **reproducible numerical experiment** on coherent vortices, modons, and energy localization.

---

## Snapshot

### Field
- Fundamental physics  
- Emergent geometry & complex systems  

### Model type
- Geometry → scalar field extraction  
- Topological structure and energy-density analysis  

### Stage
- Proof-of-concept with large-scale simulation  
- 400×400×400 spatial grid, 50 time steps  

### Main question

If four-dimensional spacetime is a dynamic hypersphere controlled by a single radial function, can we build a scalar field purely from geometric gradients that self-organizes into coherent vortices and energy clusters—**without** postulating a fundamental quantum field?

More concretely:

> When we define \(w(x,t)\) from spatial and temporal derivatives of the hyperspherical radius and evolve it on a 400³ grid over 50 time steps, do we observe stable modons, quantized phase winding, and smooth global behavior, rather than chaotic blow-up?

---

## Model & approach

We start from the same time-evolving 4D hypersphere used in the geometric core: a manifold with coordinates  
\((\chi, \theta, \phi, t)\) whose shape is determined by a radial field \(R(\chi,\theta,t)\).

Instead of introducing a new matter field, we **define the scalar directly from geometry**:

1. Compute spatial gradients \(\nabla R\) and the time derivative \(\partial_t R\) on the numerical grid.
2. Combine these into a real scalar amplitude \(w(x,t)\) with a curvature-based normalization factor \(\gamma\), so that both spatial and temporal variations of \(R\) contribute in a controlled way.
3. Promote \(w\) to a complex field
   \[
   w = |w| e^{i\phi}
   \]
   to track both amplitude and phase.

On the full \(400 \times 400 \times 400\) spatial grid with 50 time steps, we then:

- Monitor the **volume-averaged amplitude** \(\langle |w(t)| \rangle\) to test global stability (time series is smooth and non-chaotic).
- Locate nodes where \(|w| \to 0\) and measure the **circulation of the phase** around them, revealing integer winding numbers—quantized vortices and modon cores with conserved topological charge.
- Compute a **topological energy density** that combines amplitude and phase gradients; peaks in this energy highlight coherent structures such as vortex rings and rotating modons that act as localized energy reservoirs.
- Correlate regions of strong \(|\nabla w|^2\) and phase winding with anisotropy in the **extrinsic curvature** tensor, showing how the scalar both reflects and organizes the underlying geometry.

The result is a scalar field that does **not** behave chaotically, but exhibits self-organization, criticality, and long-range order: modons and vortices persist over many time steps, with their cores tracking geometric features of the evolving hypersphere.

---

## Numerical setup

The scalar field is constructed and analyzed on the same high-resolution grid as the geometric core:

- **Spatial grid:** \(400 \times 400 \times 400\) points  
- **Temporal evolution:** 50 time steps  
- **Resolutions:** fixed \(\Delta \chi, \Delta \theta, \Delta \phi, \Delta t\)

Given precomputed runs of the geometric core (metric, extrinsic curvature, and radial field \(R\)), this code:

- loads the relevant memmapped arrays,
- constructs \(w(x,t)\) and its derivatives,
- performs vortex and modon detection,
- computes topological energy density and summary statistics.

---

## Repository contents


```text
README.md                    # This file

src/
  load_geometry.py           # Helpers to load R, curvature, and grid metadata
  compute_w_field.py         # Constructs w(x,t) from gradients of R
  compute_w_derivatives.py   # Spatial and temporal derivatives of w
  vortex_scan.py             # Finds nodes, phase circulation, and vortex cores
  topology_energy.py         # Computes topological energy density maps
  veff_analysis.py           # Effective potential / interference-based diagnostics
  stability_timeseries.py    # Time series for <|w(t)|> and related measures
  run_full_pipeline_w.py     # Orchestrates the full scalar-field analysis

config/
  params_w.yaml              # Thresholds, grid subsets, analysis options

data/
  w_output/                  # Memmapped scalar field w(x,t)
  w_derivatives/             # Gradients and time derivatives of w
  w_inv_output/              # Diagnostics and normalizations (γ, etc.)
  vortex_scan_outputs/       # Identified nodes and phase-winding structures
  veff_output/               # Effective potential fields
  topology_analysis/         # Topological energy maps and statistics

plots/
  w_mean_timeseries.png      # Evolution of <|w(t)|>
  modon_maps_t*.png          # Spatial maps of modon cores / vortex rings
  energy_density_slices.png  # Slices of topological energy density

```
## How to run

This analysis assumes you already have a completed **geometric core** run  
(e.g. radial field \(R(\chi,\theta,t)\), metric, and curvature stored as NumPy/memmap arrays).

For testing, you can reduce grid size or restrict to a subset of time steps in `config/params_w.yaml`.

### 1. Set up environment

Create and activate a Python environment (e.g. `venv` or `conda`), then install dependencies:

```bash
pip install -r requirements.txt
```
### 2. (Optional) Adjust parameters

Edit `config/params_w.yaml` to change:

- grid size / subgrid selection  
- number of time steps to analyze  
- thresholds for vortex detection  
- parameters for topological energy density  

### 3. Run scalar-field analysis

```bash
python src/run_full_pipeline_w.py
```
Results will be written to the `data/` subfolders, and diagnostic plots to `plots/`.

---

## Relation to the EDGE framework

This scalar-field module sits on top of the geometric backbone of the EDGE model:

- Geometry (hyperspherical spacetime, metric, curvature) is treated as **primary**.
- The scalar field \(w(x,t)\) is **derived from geometry**, not postulated.
- Coherent vortices, modons, and energy localization emerge as **secondary structures** that organize and reflect the underlying spacetime dynamics.

In the broader EDGE program, this scalar serves as a bridge between:

- emergent geometry,
- topological / energetic structures,
- and later quantum-like or gauge-like behaviors.

For additional context and related cases, see the corresponding pages on the modeling website.

---

## Code archive & publications

All scalar-field and topology outputs (`w_output`, derivatives, vortex scans, effective potential, topology analysis) are part of the archived EDGE simulation package:

- **Simulation archive (Zenodo):** DOI `10.5281/zenodo.15873778`

The main EDGE manuscript — including the scalar-field section and figures on mean amplitude and modon behavior — is currently in submission.

Code and the full technical report are available privately (e.g., for collaborators or reviewers) and can be shared under NDA or specific agreement.

---

## License & usage

This repository is provided as a **demonstration and case study**.

- Use is limited to **personal, academic, and non-commercial** purposes.
- Do **not** integrate this code into clinical, diagnostic, or commercial products.
- Redistribution of modified or unmodified versions is **not permitted** without explicit written permission.

For collaboration, extended access, or use within a larger project, please contact the author.
