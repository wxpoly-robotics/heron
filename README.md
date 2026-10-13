# mobilityrobot-coverage-planning

Run-level dataset for the paper:

**Y. Guan, F. Fang, Y. Zhang, J. Pei, N. Jiang**, "A Connection-Cost Optimized Full-Coverage
Path Planning Method with Concave-Region Decomposition and Prescan Detour for Autonomous
Lawn Mowing Robots" (submitted to *Agriculture*, MDPI).

Correspondence: guanyg@wxpoly.cn

## Contents

- `data/summary.csv` — per-run metrics of the coverage-comparison batch
  (boundary × method × repetition): coverage, repeat rate, path length, planned/executed
  connection length, task time, collisions, run status (done / timeout / killed).
- `data/TABLES.md` — the exact aggregated values reported in Tables 1–4 of the paper.
- `data/FINAL_SUMMARY.md` — batch-level summary.
- `data/<run_id>/`:
  - `odom.csv` — 50 Hz ground-truth odometry (`t, x, y, yaw, v, w`)
  - `planned_path.csv` — the planned coverage path sent to Nav2 (`x, y`)
  - `scan.csv` — LiDAR scans
  - `meta.json` — boundary polygon, obstacles (type, x, y, radius), method, parameters
  - `run_params.yaml` — full planner/avoidance parameter set of the run
  - `launch.log` — run log (including the per-angle connection-cost profile)

Run-id convention: `sciA_<shape>_<shape>_<method>_r<i>`,
shape ∈ {rect6, L7, mush}, method ∈ {fixed0, pca, multi}.

## Batches

This repository holds the **coverage-comparison batch** (25 runs + disclosed backup runs).
The Nav2-baseline runs and the fusion-avoidance ablation batch (10 runs) are released with
the companion study: https://github.com/wxpoly-robotics/mobilityrobot-fusion-avoidance

## Metrics

- Coverage (%): executed trajectory buffered by 0.225 m, intersected with the boundary
  polygon eroded by 0.4 m, rasterised on a 0.05 m grid.
- Repeat rate (%): fraction of visits that are revisits (temporal clusters separated by > 5 s).
- Collision: distance from trajectory points to ground-truth obstacle geometry below the
  0.27 m robot body radius, cross-checked against the minimum LiDAR range.

## Source code

Not part of this release. Available from the corresponding author upon reasonable request.

## License

The data in this repository are licensed under the Creative Commons Attribution 4.0
International License (CC BY 4.0): https://creativecommons.org/licenses/by/4.0/
You are free to share and adapt the material with appropriate attribution.
