# farad-models

Runnable neural-surrogate inference package for **farad** — compiled and torch-free (ONNX + `onnxruntime`, CPU). Physical spec in, physical results out.

```python
from farad_models import load, list_models
model = load(list_models()[0])
```

## Install

Preview packages are proprietary and are **not on PyPI**, so `pip install farad-models` will not resolve. Install the wheel directly from the GitHub release:

```
pip install https://github.com/huntingtonapplied/farad-models/releases/download/v0.2.1/farad_models-0.2.1-py3-none-any.whl
```

Dependencies: `numpy`, `onnxruntime` (CPU) — no torch. A hosted package index (so `pip install farad-models` resolves directly) is planned.

## License

Closed-source, compiled distribution. Licensed under the **Farad Model EULA** (see `LICENSE`). Reverse engineering, weight/feature extraction, and redistribution are prohibited. © 2025-2026 Huntington Applied.
