**Business Understanding**
The Used Car Dealership aims to identify the key factors that influence used car pricing. The primary goals are to:
* Handle Market Competition: Set more competitive prices for inventory
* Improve Decision-Making: Source high-demand vehicles using data
* Understand Customer Preferences: Learn what buyers value most
* Enhance Profitability: Reduce pricing errors and align with market demand

**Objective**
Develop machine learning models that predict used car prices and surface key pricing drivers based on historical vehicle and sales data.

**Technical Approach:**
* Supervised regression modeling using vehicle price as the target variable
* Trained models on predictors such as: year, odometer, condition, title status, fuel, transmission, drive, type, and engine cylinders
* Used techniques like feature selection, scaling, and regularization (Lasso & Ridge)

**Model Performance Summary : Model Performance Comparison**

| Model                         | RMSE     | R² Score | Notes                                              |
|--------------------------------|----------|----------|----------------------------------------------------|
| Ridge Regression (α=100)       | 5,965.13 | 0.7623   | Best performer: high accuracy, handles multicollinearity well |
| Linear Regression (raw)        | 7,142.56 | 0.6592   | Reliable baseline, but less precise               |
| Log-Transformed Linear Regression | 6,750.85 | 0.6955   | Price normalization improves fit                  |
| Lasso Regression               | 7,393.41 | 0.6348   | Over-regularized, comparatively lowest prediction performance |


**Key Modeling Insights**
* Ridge Regression performed best by balancing accuracy and feature interpretability
* Top predictive features:
    * Year: More recent vehicles tend to fetch higher prices
    * Odometer: Higher mileage typically leads to a lower resale value
    * Condition: Better condition boosts value significantly
    * Title status: Salvage, rebuilt, and lien titles drop value by up to $25,000
    * Vehicle type: Trucks and diesel vehicles retain value better than sedans or FWD models



**Top 20 Influential Features**
**Positive Influencers : Key Features & Coefficients**

| Feature               | Coefficient | Interpretation                                      |
|-----------------------|-------------|---------------------------------------------------- |
| `year`                | +0.382      | Newer cars command higher prices                    |
| `fuel_diesel`         | +0.080      | Diesel vehicles retain more value                   |
| `type_truck`          | +0.117      | Trucks have strong resale value                     |
| `type_pickup`         | +0.059      | Pickups are in high demand                          |
| `transmission_manual` | +0.054      | Enthusiast demand or they lower maintenance         |
| `type_convertible`    | +0.048      | Lifestyle appeal increases resale value             |


## ⬇️ Negative Influencers

| Feature                 | Coefficient | Interpretation                                      |
|--------------------------|-------------|-----------------------------------------------------|
| `odometer`               | -0.296      | More mileage means lower price                     |
| `cylinders_4 cylinders`  | -0.243      | Economy engine is equvalent to base segment pricing|
| `cylinders_6 cylinders`  | -0.173      | Mid-size engines in lower-demand segments          |
| `drive_fwd`              | -0.145      | FWD is common in lower-value sedans                |
| `title_status_rebuilt`   | -0.143      | Rebuilt history drops value significantly          |
| `title_status_salvage`   | -0.109      | Major loss in resale value                         |
| `fuel_gas`               | -0.092      | Default/common option, lower premium               |
| `cylinders_other`        | -0.089      | Rare configurations with uncertain demand          |
| `condition_good`         | -0.070      | Not as desirable as "excellent" condition          |
| `cylinders_8 cylinders`  | -0.068      | Big engines don’t always mean more value           |
| `title_status_lien`      | -0.054      | Financing complications reduce resale              |
| `type_sedan`             | -0.051      | Saturated market segment                           |
| `cylinders_5 cylinders`  | -0.049      | Uncommon engines may reduce appeal                 |


**Client Value Proposition**
This model helps dealerships:
* Set accurate, market-aligned vehicle prices
* Avoid overpaying for low-resale vehicles (e.g., salvage/rebuilt titles)
* Prioritize inventory with high resale demand (e.g., trucks, diesel)
* Empower staff with data-driven pricing tools

**Recommended Next Steps**
1. Deploy the Ridge model as a core pricing engine
2. Create a simple pricing dashboard or trade-in evaluation tool
3. Test the model on real dealership listings
4. Also, there is a need to Explore advanced tree-based models (XGBoost, Random Forest) for potential improvement

**Summary**
*Trained and evaluated multiple machine learning models to predict used car prices.
*The Ridge Regression model performed best, with an RMSE of $5,965 and R² of 0.7623. 
*These results provide a strong foundation for building a dealership-friendly pricing system that enhances profitability, reduces error, and improves customer trust.



