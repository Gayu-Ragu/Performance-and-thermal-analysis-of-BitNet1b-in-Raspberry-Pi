# Benchmark scripts

This directory is reserved for the scripts used to execute and parse the Raspberry Pi benchmark campaign.

Planned files from the completed experiment include:

- `bench_one.sh` — runs one inference configuration and records timing/metadata
- `run_matrix.sh` — executes the workload matrix with warm-up and measured trials
- `telemetry.sh` — samples Raspberry Pi temperature, ARM clock and throttle state
- `parse_run.py` — parses raw benchmark output into structured results
- `build_prompts.py` — creates the frozen prompt-length files

The original scripts should be copied here from the Raspberry Pi without rewriting them so that the repository preserves the exact experimental implementation.
