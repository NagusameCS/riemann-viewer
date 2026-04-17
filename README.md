# Riemannian Manifold Viewer

3D visualization of the Riemannian geometry of neural network weight spaces.

Manifold data is computed by [Geodessical / HyperTensor](https://github.com/nicholascormier/HyperTensor) — an axiomatic survey pipeline that extracts intrinsic dimension, symmetry groups, curvature fields, metric tensors, and Christoffel connections from model weights.

## Models

| Model | Architecture | Dim | Layers | Quant | Intrinsic Dim | Max \|R\| |
|-------|-------------|-----|--------|-------|---------------|-----------|
| [SmolLM2-135M](smol/) | LLaMA | 576 | 30 | Q8_0 | 17 | 1083.88 |
| [Phi-3.5 Mini](phi/) | Phi-3 | 3072 | 32 | Q4_0 | 11 | 0.004 |
| [Gemma-4 E2B](gemma/) | Gemma-4 | 1536 | 35 | Q4_0 | 25 | 0 (flat) |

## Visualization

- **Curvature field**: Points colored by scalar curvature R (blue = negative, red = positive)
- **Point size**: Scaled by Christoffel connection norm ‖Γ‖
- **Metric ellipsoids**: Wireframe ellipsoids showing g_ii (metric tensor diagonal)
- **PCA cloud**: Raw projected weight samples in 3D PCA space
- **Connections**: Nearest-neighbor links in the curvature field

## Custom Data

Drop any `manifold_export.json` file onto the [viewer](viewer.html) to visualize your own model. Export format: `geodessical-manifold-v1`.

## Data Format

```json
{
  "format": "geodessical-manifold-v1",
  "model": { "name": "...", "arch": "...", "dim": 576, "layers": 30, ... },
  "manifold": { "cloud": [[x,y,z], ...], "intrinsic_dim": 17, ... },
  "curvature": {
    "points": [
      { "pos": [x,y,z], "R": 0.0, "g_diag": [g11,g22,g33], "christoffel_norm": 0.0 },
      ...
    ]
  },
  "axioms": { "n_axioms": 22, "consistency_score": 0.92, ... }
}
```
