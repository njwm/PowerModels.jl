# PowerModels.jl 

[![Build Status](https://travis-ci.org/lanl-ansi/PowerModels.jl.svg?branch=master)](https://travis-ci.org/lanl-ansi/PowerModels.jl)
[![codecov](https://codecov.io/gh/lanl-ansi/PowerModels.jl/branch/master/graph/badge.svg)](https://codecov.io/gh/lanl-ansi/PowerModels.jl)

PowerModels.jl is a Julia/JuMP package for Steady-State Power Network Optimization.
It is designed to enable computational evaluation of emerging power network formulations and algorithms in a common platform.
The code is engineered to decouple problem specifications (e.g. Power Flow, Optimal Power Flow, ...) from the power network formulations (e.g. AC, DC-approximation, SOC-relaxation, ...).
This enables the definition of a wide variety of power network formulations and their comparison on common problem specifications.

**Core Problem Specifications**
* Power Flow
* Optimal Power Flow
* Optimal Transmission Switching

**Core Network Formulations**
* AC (polar coordinates)
* DC Approximation (polar coordinates)
* SOC Relaxation (W-space)
* QC Relaxation (W+L-space)

**Network Data Formats**
* Matpower ".m" files


## Installation

For the moment, PowerModels.jl is not yet registered as a Julia package.  Hence, "clone" should be used instead of "add" for package installation,

`Pkg.clone("git@github.com:lanl-ansi/PowerModels.jl.git")`

At least one solver is required for running PowerModels.  Using the open-source solver Ipopt is recommended, as it is extremely fast, and can be used to solve a wide variety of problems and network formulations in PowerModels.  Ipopt is installed in Julia via,

`Pkg.add("Ipopt")`


## Basic Usage

Once PowerModels is installed, Ipopt is installed, and a network data file (e.g. "nesta\_case3\_lmbd.m") has been acquired, then an AC Optimal Power Flow can be executed with,
```
using PowerModels
using Ipopt

run_ac_opf("nesta\_case3\_lmbd.m", IpoptSolver())
```

Similarly a DC Optimal Power Flow can be executed with,
```
run_dc_opf("nesta\_case3\_lmbd.m", IpoptSolver())
```

In fact, "run_ac_opf" and "run_dc_opf" are simply shorthands for a more general formulation-independent OPF execution, "run_opf".  For example, "run_ac_opf" is equivalent to,
```
run_opf("nesta\_case3\_lmbd.m", ACPPowerModel. IpoptSolver())
```

Where ACPPowerModel indicates an AC formulation in polar coordinates.  This more generic "run_opf" allows one to solve an OPF problem with any power network formulation implemented in PowerModels.  For example, an SOC Optimal Power Flow can be run with,

```
run_opf("nesta\_case3\_lmbd.m", SOCWRPowerModel. IpoptSolver())
```

Extending PowerModels with new problems and formulations will be covered in a another tutorial, that is not yet available.


## Comparison to Other Tools

Forthcoming.


## Development

Community-driven development and enhancement of PowerModels are welcome and encouraged. Please fork this repository and share your contributions to the master with pull requests.


## Acknowledgments

This code has been developed as part of the Advanced Network Science Initiative at Los Alamos National Laboratory.
The primary developer is Carleton Coffrin, with significant contributions from Russell Bent.

Special thanks to Miles Lubin for his assistance in integrating with Julia/JuMP.


## License

This code is provided under a BSD license as part of the Multi-Infrastructure Control and Optimization Toolkit (MICOT) project, LA-CC-13-108.