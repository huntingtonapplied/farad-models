---
craft_id: farad_threat_detector_v1
version: 0.2.0
project: farad
license: Apache-2.0
tags: ['status:trained', 'project:farad', 'provenance:synthetic_labelled', 'release_metric:threat_macro_ap']
library_name: farad-models
---

# farad_threat_detector_v1

**Project:** farad · **Version:** 0.2.0 · **License:** Apache-2.0
**Produced by:** [Intel — Universal ML Inference Engine](https://huntingtonai.com)

> Farad Threat Detector (Craft 5.1)

> ⚠️ **Synthetic / non-engine-truth data (`synthetic_labelled`).** The metrics below are
> **NOT** the real simulation engine's output — they are computed on the craft's synthetic
> or cited training distribution. The headline number is the **`threat_macro_ap`** metric, not an
> engine-faithful accuracy; read it as such.
>
> _Eval note:_ farad r2 WIN: SecurityGenerator corpus 240->1000 scenarios. Same-test-set (234 scenarios) comparison — WINS ALL 3 metrics: macro_ap 0.849->0.889, micro_f1 0.727->0.902, stage_acc 0.526->0.970. The OLD registered "0.904 macro_ap" was a 43-scenario SMALL-SAMPLE inflation (on the fair 234-scenario test the registered ckpt is only 0.849). best-val pick (val 0.778) of best-of-4. Different-test-basis trap MASKED this real win as a ceiling — caught by the same-testset comparison. SYNTHETIC labels.

## Model description

`farad_threat_detector_v1` is a **surrogate model** ("craft") used by the AHL Intel inference
engine to replace expensive numerical simulation with fast neural inference.
Output kind: **fields** (0 outputs). Farad Threat Detector (Craft 5.1)

- **Status:** trained
- **Type:** neural inference surrogate (physics-trained)
- **Parameters:** 3,093,783
- **Weights format:** `model.safetensors` (float32)
- **Device family:** `—`

## Intended use

Drop-in inference surrogate for farad. You provide a physical **device
specification** (geometry, materials, doping, operating point); the package
returns the physical output channels below. The device→model featurization and
de-normalization are handled inside the package. Not intended for regimes
outside its training domain (below).

## Inputs & outputs

**Input — physical device specification** (`input.kind: device_spec`):

Provide a physical device/scene specification; see the project's model docs.

The internal encoding (how the device becomes model inputs) and the normalization are handled **inside the package** — you never build feature vectors by hand.

**Output — physical fields:**

| | |
|---|---|
| **Output channels** | 0 |
| **Parameters** | 3,093,783 |

## Training domain / compatibility

| Property | Value |
|---|---|
| Solution type | `—` |
| Physics models | — |
| Temperature | — K |
| Bias range (Vds) | — |
| Tags | `status:trained`, `project:farad`, `provenance:synthetic_labelled`, `release_metric:threat_macro_ap` |

## Training data

Trained on farad simulation output for the `—` solution regime (physics models: see config). Labels derive from the numerical farad engine / reference closed-forms; the data-generation pipeline is proprietary.

## Limitations & out-of-scope use

- **Do not** use outside the training domain above (solution type, temperature, bias range) — accuracy degrades with no guarantee.
- This is a **surrogate**, not the ground-truth solver: treat outputs as fast approximations; validate against the numerical engine where correctness is critical.
- Output kind is **fields** — consuming code must match the documented I/O contract exactly.


## Evaluation

| Metric | Value |
|---|---|
| **Held-out accuracy** | 0.889 |
| Best validation loss | 0.778318046879124 |

_**Held-out accuracy** is an independent benchmark (`offline_eval` on a held-out set); the loss rows are the model's own recorded train/val losses. See `config.json → metrics` for the machine-readable copy._

## Caveats & recommendations

- An independent **held-out** benchmark is reported (Held-out accuracy, via `offline_eval`); the loss rows remain the model's own recorded train/val losses.
- Verify integrity before use: `shasum -a 256 -c SHA256SUMS` (or `sha256sum -c SHA256SUMS` on Linux). Weights are `safetensors` — safe to load, no pickle.
- This is a **surrogate**, not the ground-truth solver — validate against the numerical engine where correctness is critical.

## Usage

Install the inference package and run it on a physical device spec — it fetches the
weights, builds the model, and returns physical fields (no PyTorch required):

```bash
pip install farad-models
```

```python
from farad_models import load

model = load("farad_threat_detector_v1")           # pulls + verifies weights, builds the compiled pipeline
fields = model.predict(device_spec)  # physical device in -> physical fields out
```

`device_spec` is the physical device specification documented under **Inputs & outputs**
above. Featurization and de-normalization happen inside the package.

## Provenance

- **Author:** sim-train release (NONBOLTZMANN_RELEASE_TRAINING.md)
- **Trained:** 2026-07-20T07:57:44.226915+00:00
- **Source checksum (runtime .pt):** `add7e1da621564641288ec7896150ee28494a6c5ab25d17efbec1d7be145c9e9`

## Citation

```bibtex
@software{farad_threat_detector_v1_0_2_0,
  title  = {farad_threat_detector_v1},
  author = {AHL / Intel},
  year   = {2026},
  note   = {Version 0.2.0},
  url    = {https://downloads.faraddefense.com/models/farad_threat_detector_v1/0.2.0/}
}
```

## License

Licensed under the **Apache-2.0** (Apache-2.0) — free to use for
inference; redistribution and reverse engineering of the compiled inference core
are not permitted. See `LICENSE`.
