# Deploy Guide — K_ELEPHANT
**Tier:** TIER_7_BIOSIGNALS_NEURO | **Stack:** Python 3.11, elephant 1.x, neo, numpy, PAX 27B, AIOSS_FORMAT
**Air-gap capable after initial setup.**

## Prerequisites
Python 3.11+, elephant 1.0+, neo 0.13+, numpy 1.26+. CPU-intensive for spike sorting.

## Environment
16GB RAM for large neural recordings. CPU-intensive. No GPU required.

## AIOSS Integration
```bash
aioss init --module K_ELEPHANT --output ./k_elephant.aioss
aioss append --chain ./k_elephant.aioss --payload ./output.bin --module K_ELEPHANT
aioss verify --chain ./k_elephant.aioss
```

## Air-Gap Setup
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="K_ELEPHANT",
    aioss_chain="./K_ELEPHANT.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./K_ELEPHANT.aioss --verbose
python -m K_ELEPHANT.tests.smoke
```
