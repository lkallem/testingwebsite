---
layout: page
title: Test Cases
permalink: /test-cases/
---

# Test Cases

Validation and benchmarking for the MoSAIC-P38 system.

![RISC-V to SNN message-passing diagram]({{ '/assets/images/hero-riscv-snn.png' | relative_url }})

## Validation Suite
We provide a comprehensive set of tests to verify the correctness of the hardware-software interface.
- **Connectivity Tests**: Verifies NoC routing between all tiles.
- **SNN Logic Tests**: Validates spike integration and thresholding.
- **Memory Tests**: Ensures consistent data movement between RISC-V and SNN memory.

## Benchmarks
Performance metrics for common SNN workloads.
- **Latency**: Average time for a spike to traverse the network.
- **Throughput**: Maximum spikes per second per tile.
- **Power Efficiency**: Energy per synaptic operation (measured in pJ).

## Example Runs
Detailed logs and result files from our standard validation runs are available for download in the `/tests/results` directory of the main repository.
