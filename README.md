# Performance and Thermal Analysis of BitNet b1.58 on Raspberry Pi 5

This repository contains the experimental methodology, benchmark results, energy measurements, and analysis for a system-level evaluation of **BitNet b1.58 2B4T inference on a Raspberry Pi 5 (4 GB)**.

## Project objective

The project evaluates whether a highly quantized large language model can run practically on resource-constrained ARM edge hardware and studies how thermal management changes sustained inference performance and energy consumption.

The primary experiment compares two operating conditions while keeping the model, software environment, power path, workload, and benchmark methodology fixed:

- **Set A:** Raspberry Pi 5 without active cooling
- **Set B:** Raspberry Pi 5 with active cooling

## Model and platform

- Raspberry Pi 5, 4 GB RAM
- BitNet b1.58 2B4T
- I2_S GGUF representation
- CPU-only inference using bitnet.cpp
- Reference workload: **P512-G128-T4**
  - approximately 512 prompt tokens
  - 128 requested generated tokens
  - 4 CPU threads

## Measurements

The benchmark framework records:

- Prompt-processing throughput (tokens/s)
- Generation throughput (tokens/s)
- Wall-clock inference time
- CPU temperature
- ARM CPU frequency
- Thermal/throttle state
- Peak resident memory (RSS)
- Board-level energy consumption using an external USB power meter
- Energy per query and energy per requested generated token

## Key result

For the P512-G128-T4 reference configuration, active cooling substantially improved sustained performance and thermal stability. Prompt throughput increased from approximately **7.442 to 9.048 tok/s**, generation throughput increased from **6.348 to 8.460 tok/s**, and controlled benchmark wall time decreased from approximately **89.98 s to 72.74 s**.

In the dedicated five-query energy experiment, Set A consumed **861 mWh over 513 s**, while Set B consumed **903 mWh over 376 s**. Active cooling therefore reduced the sustained measurement interval by approximately **26.7%**, while total energy increased by approximately **4.9%**. The result demonstrates a clear performance-thermal-energy trade-off: cooling enables significantly faster and more stable inference at a modest increase in energy per query.

## Repository structure

```text
benchmark/      Benchmark and telemetry scripts
prompts/        Frozen benchmark prompts
results/        Set A and Set B CSV results, logs, and telemetry
energy/         Energy measurements and derived comparison data
analysis/       Analysis scripts and generated figures
docs/           Project reports and supporting documentation
paper/          Material prepared for a research-paper version of the project
```

## Experimental rule

Only one experimental factor is changed at a time. The Set A/Set B cooling comparison uses the same model, software, workload, power path, and benchmark settings so that cooling state is the primary independent variable.

## Status

- Set A benchmark: completed
- Set A energy measurement: completed
- Set B benchmark: completed
- Set B energy measurement: completed
- Set A vs Set B analysis: completed
- Research-paper preparation: in progress

## Model files

Large model binaries are intentionally not stored in this repository. The experiments use the BitNet b1.58 2B4T I2_S GGUF model. The model source, filename, hash, and runtime version should be recorded for reproducibility.
