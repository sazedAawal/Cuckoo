# Cuckoo
A custom Grasshopper based plugin aimed to explore Acoustics

Version 1.2.1
---
- Raytracer simulates a single Brep.
- CSV converter exports simulated ray-tracing data.
- Latin Hypercube Sampling (LHS) generates Brep variations while maintaining the original proportions.
- Generated Brep variations are exported as CSV.


Next Steps
---
- For each Brep variation, run the raytracer.
- Export the geometry and ray-tracing results to CSV, linked by GeometryID.
- Calculate acoustic features/results from the ray data.
- Combine geometry + ray + (acoustic) data into one training dataset.
- Train a CatBoost surrogate model to predict acoustic results.
- Validate the model against ray-tracing/acoustic simulations.
- Export the trained CatBoost model to ONNX-ML.
- Integrate the ONNX model into the Grasshopper plugin using ONNX Runtime.


Version 1.2.2
---
## CatBoost Raytracing Surrogate — To Do

* [x] Train 10 CatBoost models for raytracing prediction
* [x] Test models on unseen geometries
* [ ] Export all 10 models as `.cbm`
* [ ] Keep the exact 18-feature order used during training
* [ ] **Do not convert to ONNX yet** — direct `.cbm` deployment in C# is the simpler route

### Grasshopper Components

* [ ] **C# Component 1 — Brep → ML Inputs**

  * Input: unknown Brep
  * Generate geometry features
  * Generate all initial rays using the same ray-generation method as the original raytracer
  * Generate the 18 required features
  * Output all feature rows

* [ ] **C# Component 2 — CatBoost Surrogate**

  * Input: 18-feature rows
  * Load the 10 `.cbm` models
  * Predict all ray outputs
  * Handle sequential ray bounces
  * Output predicted ray data

* [ ] **C# Component 3 — Ray Visualizer**

  * Input: surrogate predictions
  * Reconstruct predicted ray segments
  * Output all predicted ray lines in Grasshopper

### Final Workflow

* [ ] Connect:
  **Brep → ML Input Generator → CatBoost Surrogate → Ray Visualizer**
* [ ] Test with an unseen Brep
* [ ] Compare surrogate rays against the original raytracer
* [ ] Compare computation time
* [ ] Expand training dataset beyond 28 geometries
* [ ] Eventually combine the three components into one user-facing **ML Raytracer** component

### Later

* [ ] Investigate ONNX Runtime only if needed for deployment
* [ ] Add acoustic prediction after the raytracing surrogate is validated
