---
layout: page
title: Documentation
permalink: /documentation/
---

# Documentation

The MoSAIC-P38 documentation provides a comprehensive technical overview of the system's hardware and software stack.

## Architecture Overview
MoSAIC-P38 employs a tiled architecture where each tile contains a combination of a RISC-V processor and a specialized SNN accelerator. The communication between these entities is handled via a high-speed Network-on-Chip (NoC).

### Hardware Specifications
- **Processor**: RISC-V based control plane.
- **SNN Accelerator**: Specialized hardware for spike integration and firing.
- **Interconnect**: Low-latency asynchronous NoC.

## Build Instructions
To build the MoSAIC-P38 simulation environment, follow these steps:

1. **Prerequisites**: Ensure you have `gcc` and `make` installed.
2. **Clone Repository**: `git clone https://github.com/lbnlcomputerarch/MoSAIC-P38`
3. **Compile**: Run `make build` in the root directory.

## API Reference
The system exposes a C-based API for controlling the SNN blocks from the RISC-V cores. Detailed function signatures and usage examples can be found in the `/docs/api` directory of the source repository.
