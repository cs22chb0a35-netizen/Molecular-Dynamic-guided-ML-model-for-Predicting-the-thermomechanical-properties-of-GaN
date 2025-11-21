# Molecular Dynamics-Guided Machine Learning for Thermo-Mechanical Prediction of Gallium Nitride (GaN)

##  Project Overview

**Gallium Nitride (GaN)** is a wide bandgap semiconductor that has revolutionized high-power electronics and optoelectronics due to its superior thermal stability and mechanical strength.



However, characterizing GaN's thermo-mechanical properties under varying operating conditions using experimental methods or repeated **Molecular Dynamics (MD)** simulations is computationally expensive and time-consuming.

This project develops a **surrogate Machine Learning model** (Polynomial Regression) trained on an MD-inspired dataset. The model rapidly and accurately predicts the **Stress**, **Young's Modulus**, and **Thermal Conductivity** of GaN based on temperature and strain inputs.

---

##  Objectives

1.  **Dataset Generation:** Create a synthetic dataset of 6,000 points representing the physical behavior of GaN at 300K, 600K, and 900K.
2.  **Model Development:** Implement a **Polynomial Regression** model (Degree 2) to capture non-linear dependencies between thermal and mechanical factors.
3.  **Validation:** Evaluate the model using $R^2$, Mean Absolute Error (MAE), and Root Mean Square Error (RMSE).

---

## ⚙️ Methodology

The workflow integrates physical principles with data-driven modeling:



[Image of Machine Learning regression workflow diagram]


### 1. Data Generation (MD-Inspired)
To simulate the data usually obtained from LAMMPS MD simulations, we generated data based on simplified physical relationships for GaN:
* **Temperature Range:** 300 K – 900 K
* **Strain Range:** 0.001 – 0.12
* **Properties Modeled:**
    * *Stress (GPa):* Calculated via Hooke's Law with temperature degradation.
    * *Young's Modulus (GPa):* modeled to decrease non-linearly with rising temperature.
    * *Thermal Conductivity (W/m·K):* modeled to decrease with temperature (phonon scattering effect).

### 2. Machine Learning Pipeline
* **Preprocessing:** `PolynomialFeatures` (Degree=2) to expand the feature space.
* **Scaling:** `StandardScaler` to normalize inputs.
* **Algorithm:** Linear Regression applied to polynomial features.
* **Split:** 70% Training / 30% Testing.

---

##  Dataset Description

The dataset (`GaN_MD_dataset.csv`) contains **6,000 data points** with the following structure:

| Feature Type | Variable Name | Unit | Description |
| :--- | :--- | :--- | :--- |
| **Input** | `Temperature` | Kelvin (K) | Operating temperature (300, 600, 900 K) |
| **Input** | `Strain` | - | Engineering strain (deformation) |
| **Output** | `Stress` | GPa | Internal restoring force |
| **Output** | `Youngs_Modulus`| GPa | Stiffness of the material |
| **Output** | `Thermal_Conductivity` | W/m·K | Heat transfer capability |

---

##  Results & Performance

The Polynomial Regression model demonstrated high accuracy in capturing the thermo-mechanical behavior of GaN.

### Performance Metrics (Test Set)
| Metric | Value |
| :--- | :--- |
| **$R^2$ Score** | **> 0.99** |
| **MAE** | Low |
| **RMSE** | Low |

### Visualizations
* **Stress-Strain Curves:** Accurately captures the linear elastic region and temperature softening.
* **Thermal Conductivity:** Correctly models the inverse relationship with temperature.
* **Parity Plots:** Actual vs. Predicted values show a tight correlation along the diagonal.


## 📚 References

1.  **Machine Learning in Materials:**
    * Schmidt, J., et al. "Recent advances and applications of machine learning in solid-state materials science." *npj Computational Materials*, 2019.
    * Agrawal, A., & Choudhary, A. "Perspective: Materials informatics and big data." *APL Materials*, 2016.

2.  **Gallium Nitride Properties:**
    * Levinshtein, M.E., et al. *Properties of Advanced Semiconductor Materials: GaN, AlN, InN, BN, SiC, SiGe*. Wiley, 2001.
    * Pearton, S.J. *GaN and Related Materials*. Gordon and Breach, 1997.

3.  **Methodology:**
    * Géron, A. *Hands-On Machine Learning with Scikit-Learn, Keras and TensorFlow*. O’Reilly Media, 2019.
