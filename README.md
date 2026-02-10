# Wildfire Susceptibility Modelling using Machine Learning
This repository supports an MSc dissertation works. Some components are intentionally abstracted or omitted to align with planned peer-reviewed publications.

## Outline 
Developed as part of an MSc in Satellite Data Science (University of Leicester), this work investigates how machine learning models can be applied to wildfire risk assessment within a spatially constrained study area (Pacific Palisades, California).

The framework compares multiple classification algorithms under severe class imbalance and translates model outputs into an interpretable wildfire susceptibility surface.

## 1. Methodological Workflow

### Problem Framing & Literature Review
As per I read, the January 2025 Palisades Fire in Pacific Palisades, California was one of the most destructive wildfire events in Los Angeles history, resulting in significant structural loss and large-scale evacuation. Satellite observations captured rapid fire spread, smoke plume transport, and post-burn footprint patterns, highlighting the importance of remote sensing in wildfire monitoring. These events and reports informed the framing of wildfire susceptibility modelling within a spatially constrained, high-risk wildland–urban interface (WUI) environment.

References
	•	[CAL FIRE – Palisades Fire Incident Updates](https://www.fire.ca.gov/incidents/2025/1/7/palisades-fire/)
	•	[CAL FIRE – Structure Status Map (ArcGIS)](https://hub-calfire-forestry.hub.arcgis.com/maps/2d764eef786841ce9194e84f524f2c8e)
	•	[NASA Earth Observatory – Fires Tear Through Los Angeles (Jan 9, 2025)](https://science.nasa.gov/earth/earth-observatory/fires-tear-through-los-angeles-153793/)
	•	[NASA Earth Observatory – Smoke Streams from Palisades and Eaton Fires (Jan 14, 2025)](https://science.nasa.gov/earth/earth-observatory/smoke-streams-from-palisades-and-eaton-fires-153813/)
	•	[NASA Earth Observatory – The Palisades Fire’s Footprint (Jan 17, 2025)](https://science.nasa.gov/earth/earth-observatory/the-palisades-fires-footprint-153831/)
	•	[ABC News – After Wildfires, Devastation in California](https://abcnews.go.com/US/after-wildfires-devastation-california/story?id=117499669)
	•	[Boston University School of Public Health – Excess mortality estimates related to LA County wildfires (2025)](https://www.bu.edu/sph/news/articles/2025/death-count-for-2025-la-county-wildfires-likely-hundreds-higher-than-official-records-show/)
	•	[Swiss Re – Global insured losses report referencing 2025 California wildfires](https://www.swissre.com/media/press-release/pr-20250806-wildfires-thunderstorms-global-insured-losses-first-half-2025.html)

### 2. Data Composition
The modelling framework integrates satellite-derived vegetation metrics (e.g., NDVI), meteorological indicators (e.g., relative humidity, fire weather variables), topographic attributes, and spatial coordinates within the Pacific Palisades study area. Datasets were spatially resampled and harmonised to <500 m resolution, with temporal alignment applied where required to maintain consistency across predictors.

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/7bfe9d49-5a84-43b8-879f-187e10b8c1f0" />

## 3. Data Preprocessing & Imbalance Strategy

### Data Preprocessing
All datasets were spatially clipped to the defined study boundary, reducing the initial sample size from around ~500,000 to ~300,000 observations by excluding areas outside Pacific Palisades. Predictors were resampled and harmonised to a consistent spatial resolution (<500 m) and aligned temporally where required. Missing vegetation signals were addressed using temporal interpolation to maintain continuity in modelling inputs.


### Imbalance Strategy
Wildfire occurrence represented an extreme rare-event scenario (~30 positive vs ~350,000 negative samples prior to balancing). Multiple resampling strategies were evaluated to mitigate majority-class dominance and ensure stable learning behaviour. Model selection prioritised robustness and discrimination performance under skewed class distributions rather than raw accuracy.

## 4. Model Development & Evaluation

Four classification algorithms were evaluated: Logistic Regression, Decision Tree, Random Forest, and XGBoost. Each model was trained under multiple resampling strategies to address severe class imbalance.

Models were compared using AUC and F1-score, with emphasis on stability under skewed distributions. Random Forest with Random Oversampling (RF + ROS) demonstrated the strongest discrimination performance (AUC ≈ 1.00; F1 = 0.92) and was selected for final susceptibility mapping.

## 5. Interpretability & Spatial Output

Model interpretability was assessed using SHAP (SHapley Additive exPlanations) to quantify feature contributions and understand variable influence on wildfire susceptibility predictions. Key environmental and spatial predictors demonstrated consistent explanatory power across model runs.

Final model outputs were translated into a quantile-based wildfire susceptibility surface, producing spatially coherent high-risk zones within the wildland–urban interface (WUI). This step bridged machine-learning predictions with spatial risk interpretation, moving beyond isolated classification scores toward operationally meaningful mapping.

## 6. Results Summary

Model development was informed by established wildfire and rare-event modelling literature, particularly regarding evaluation metrics and imbalance-aware learning strategies. Hyperparameter configurations were guided by prior research benchmarks and iteratively refined within the study context. Among the evaluated models, Random Forest with Random Oversampling (RF + ROS) demonstrated the strongest discrimination performance under extreme class imbalance, achieving AUC ≈ 1.00 and F1-score ≈ 0.92. Importantly, model outputs produced spatially coherent susceptibility patterns rather than noise-driven classifications, supporting the robustness of the modelling framework within the defined study area.

## Reproducibility

The codebase is implemented in Python, with dependencies listed in `requirements.txt`. 

Raw datasets are not included due to size, licensing restrictions, and ongoing publication considerations. However, the repository structure and workflow outline provide sufficient guidance for methodological replication.

## License

This project is released under the MIT License. See the LICENSE file for details.






