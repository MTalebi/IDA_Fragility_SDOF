# IDA and Fragility Analysis of a Nonlinear SDOF System

**Author:** Mohammad Talebi-Kalaleh  
**Contact:** [talebika@ualberta.ca](mailto:talebika@ualberta.ca)

## Overview

This repository provides a Jupyter Notebook implementation for performing an **Incremental Dynamic Analysis (IDA)** and generating a **fragility curve** for a single-degree-of-freedom (SDOF) system with nonlinear behavior. The analysis is performed using OpenSeesPy and is based on the FEMA P695 far-field ground motion records (NGA-West2 database).

The notebook is designed with modular functions and is thoroughly commented to explain each step of the process.

## Capabilities

- **Ground Motion Input:**  
  Reads ground motion records in the NGA-West2 `.AT2` format. The code extracts the necessary metadata (such as time step) and acceleration data.

- **SDOF Nonlinear Modeling:**  
  The SDOF system is modeled with nonlinear hysteretic behavior using a bilinear (Steel01) material model. A `MinMax` material is applied to simulate collapse once a defined deformation threshold (corresponding to a collapse force) is exceeded. Key properties (stiffness, yield force, post-yield ratio, and collapse force) are randomized within specified ranges for demonstration.

- **Rayleigh Damping:**  
  A Rayleigh damping model is implemented to achieve a target damping ratio (5% by default) at the fundamental mode and an arbitrarily chosen higher mode. The damping coefficients are calculated based on the given circular frequencies.

- **Incremental Dynamic Analysis (IDA):**  
  The analysis scales each ground motion record from 0.05g to 2.0g (in 0.05g increments). For each scale, the transient dynamic response is computed using Newmark integration. The peak acceleration response and collapse occurrence are recorded, thereby forming the basis of IDA curves.

- **Fragility Curve Construction:**  
  Based on the collapse intensities obtained from the IDA, the code computes empirical probabilities of collapse for different intensity levels. A lognormal fragility curve is then fitted to these data points, with parameters (median collapse intensity and dispersion) estimated from the dataset.

- **Visualization:**  
  The notebook produces professional plots including:  
  - **IDA Curves:** Displaying peak SDOF acceleration versus intensity for each ground motion record (with collapse points marked).  
  - **Fragility Curve:** Showing the probability of collapse versus intensity (PGA), along with a fitted lognormal cumulative distribution function (CDF).

## Methods

- **IDA Curve Methodology:**  
  The SDOF system is subjected to scaled ground motion records. The analysis uses a time-history dynamic analysis with Newmark integration to capture the nonlinear response. The point of collapse is identified either when the analysis fails to converge or when the displacement exceeds the collapse limit defined in the `MinMax` material.

- **Fragility Curve Methodology:**  
  Empirical collapse data from the IDA are used to determine the probability of collapse at various intensity levels. A lognormal CDF is then fitted to these empirical data to produce a continuous fragility curve, a standard approach in performance-based earthquake engineering.

## Usage

1. **Ground Motion Files:**  
   Place your FEMA P695 NGA-West2 `.AT2` ground motion records in a folder named `Records` in the repository root.

2. **Notebook Execution:**  
   Run the `IDA_Fragility_SDOF.ipynb` notebook. The main block will automatically read the ground motion files, perform the analysis, and generate the corresponding plots.

## Citation

If you use this repository in your research or projects, please cite it as follows:

> **Talebi-Kalaleh, M.** (Year). *IDA and Fragility Analysis of a Nonlinear SDOF System Using OpenSeesPy*. GitHub repository. Retrieved from [(https://github.com/MTalebi/IDA_Fragility_SDOF/tree/main)].

Feel free to contact me at [talebika@ualberta.ca](mailto:talebika@ualberta.ca) with any questions or inquiries.

---

*This repository is provided "as is" without warranty of any kind, and contributions are welcome.*
