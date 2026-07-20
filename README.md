# farad-models

Runnable neural-surrogate inference for the **Farad** cyber-simulation platform.
Torch-free (ONNX + `onnxruntime`, CPU).

```python
from farad_models import load

model = load("farad_threat_detector_v1")
out = model.predict(inputs={
    "node_features": node_features,  # [N, 20] network-asset features
    "edge_index":    edge_index,     # [2, E]
    "edge_attr":     edge_attr,      # [E, 10]
    "flows":         flows,          # [1, T, 15] netflow sequence
    "logs":          logs,           # [1, T, 12] log sequence
})
# -> {threat_classification[1,15], threat_severity, attack_stage[1,7], dominant_threat, confidence}
```

`model.input_names` / `model.output_names` and each craft's `MODEL_CARD.md` document I/O.

## Install
```
pip install farad-models      # numpy + onnxruntime only, no torch
```

## Scope
- **Preview build**: ships `farad_threat_detector_v1`; more crafts follow.
- **Fast surrogates, not the ground-truth solver.**

## License
Closed-source, compiled distribution under the **AHL Model EULA** (see `LICENSE`).
© 2025–2026 Huntington Applied.
