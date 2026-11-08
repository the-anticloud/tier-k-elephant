# Developer Cookbook — K_ELEPHANT
**Stack:** Python 3.11, elephant 1.x, neo, numpy, PAX 27B, AIOSS_FORMAT
**Domain:** Elephant: neurophysiology data analysis — spike sorting and LFP for Anticloud neuro research

## Spike train analysis
```python
from k_elephant import ElephantAnalyzer

analyzer = ElephantAnalyzer(
    pax_model="./pax-27b-q4.gguf",
    aioss_chain="./elephant.aioss"
)

recording = analyzer.load_neo("./cortical_recording.nix")  # Neo format
result = analyzer.analyze_spikes(
    recording,
    measures=["firing_rate", "isi_histogram", "cv_isi", "fano_factor"]
)
print(f"Mean firing rate: {result.mean_firing_rate:.2f} Hz")
print(f"CV ISI: {result.cv_isi:.3f}")
print(f"PAX interpretation: {result.pax_interpretation}")
```

## LFP analysis
```python
lfp = analyzer.analyze_lfp(recording, band="theta")
print(f"Theta power: {lfp.power:.4f}, Phase-amplitude coupling: {lfp.pac:.4f}")
```

## AIOSS Chain Append
```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()
```
