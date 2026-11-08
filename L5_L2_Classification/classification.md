# L5 Narrow / L2 General Classification — K_ELEPHANT
**Platform:** Anticloud | **Tier:** TIER_7_BIOSIGNALS_NEURO | **PAX:** 27B
**IP:** USPTO pending 2026, Anticloud FZ LLE, 0-1.gg | **License:** Apache-2.0

## L5 Narrow
K_ELEPHANT provides Elephant neurophysiology analysis for Anticloud: spike train statistics, local field potential (LFP) analysis, Granger causality between brain regions, and spike-LFP coupling. Narrow scope: Anticloud neuro-embodied research (TIER_5/TIER_7).

## L2 General
L2 General: K_ELEPHANT's neurophysiology analysis serves TIER_5 neuro-embodied research and TIER_7 clinical biosignal processing. Same LFP and spike analysis, different deployment contexts.

## PAX 27B Integration
PAX 27B interprets Elephant analysis results: given spike train statistics and LFP power, PAX generates research-grade summaries for neuro-embodied system design.

## AIOSS Audit Chain
Every neural analysis (recording hash + spike sorting result hash + LFP spectral hash + PAX interpretation) is chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Offline-verifiable, tamper-evident, zero cloud dependency.

## Regulatory / Compliance
Good Clinical Practice (GCP) for research data. IEC 62304 (medical software).
