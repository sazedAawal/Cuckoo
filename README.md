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
