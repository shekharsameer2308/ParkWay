# ParkWay: Dynamic Pricing for Urban Parking Lots

**ParkWay** is a real-time dynamic pricing engine for urban parking lots, developed as a capstone project for **Summer Analytics 2025 by IIT Guwahati**. The project addresses the challenges of static pricing—such as overutilization and underutilization—by dynamically adjusting parking prices based on real-time factors like occupancy, traffic, queue length, vehicle type, and special days.

Using a data-driven pipeline powered by **Pathway** and visualized via **Bokeh** and **Panel**, ParkWay implements and compares multiple pricing models to ensure efficient space utilization and fair dynamic pricing.

---

##  Objectives

- Build a dynamic pricing engine to adjust rates for multiple parking spaces in real-time.
- Implement models from scratch using core data science libraries like NumPy and Pandas.
- Use a real-time data streaming framework (**Pathway**) to simulate and process live data.
- Provide real-time interactive dashboards using **Bokeh** and **Panel** to visualize pricing behavior.

---

##  Tech Stack

| Tool / Library    | Purpose |
|-------------------|---------|
| **Python**        | Programming language |
| **NumPy**         | Numerical computations, linear regression |
| **Pandas**        | Data manipulation & preprocessing |
| **Pathway**       | Real-time data stream processing |
| **Bokeh**         | Real-time interactive visualizations |
| **Panel**         | Interactive dashboard layout |
| **Google Colab**  | Development environment |

---

##  Architecture Diagram

```mermaid
graph TD
  A[Raw Parking Data - CSV] --> B[Pathway Streaming Engine]
  B --> C[Feature Extraction & Preprocessing]
  C --> D1[Model 1: Linear Pricing]
  C --> D2[Model 2: Demand-Based Pricing]
  C --> D3[Model 3: Competitive Pricing]
  D1 --> E[Price Output]
  D2 --> E
  D3 --> E
  E --> F[Bokeh Dashboard in Browser]


1) **Data Ingestion and Preprocessing**:
   - The project begins with a dataset.csv file containing historical parking data (occupancy, capacity, traffic, special days, vehicle types, etc.).
   - This raw data is first loaded and preprocessed using Pandas and NumPy. This involves:
     - Combining date and time columns into a single Timestamp.
     - Sorting data chronologically.
     - Encoding categorical features (like VehicleType and TrafficConditionNearby) into numerical representations.
     - Normalizing numerical features to a consistent scale (0-1) to ensure fair contribution in models.
     - Defining a Demand_Proxy from existing features to serve as the target variable for model training.
      
2) **Model Training (Offline)**:
   - Before real-time processing, the coefficients for Model 2 (Demand-Based Price Function) are determined.
   - A Linear Regression model is implemented from scratch using NumPy's Normal Equation method. This model is trained on the preprocessed historical data to learn the impact of factors like Occupancy Rate, Queue Length, Traffic Condition, Special Day, and Vehicle Type on the Demand_Proxy. The learned coefficients (alpha_occ, beta_queue, gamma_traffic, delta_special, epsilon_vehicle) are then used by the real-time pricing engine.
     
3) **Pathway Real-time Data Stream**:
   - The preprocessed historical data is saved into a parking_data_stream.csv.
   - Pathway is then used to simulate a real-time data stream from this CSV file using pw.demo.replay_csv. This function replays the data at a controlled rate, mimicking a live data feed.
   - A Pathway Schema is defined to ensure the incoming data is correctly structured and typed.
     
4) **Dynamic Pricing Engine (Pathway Pipeline)**:

####  Model 1: Baseline Linear Model
- Simple pricing based on occupancy ratio.
- Formula: `price = 10 + α * (occupancy / capacity)`

####  Model 2: Demand-Based Model
- Uses learned coefficients to calculate a demand score.
- Incorporates occupancy, queue length, traffic, vehicle type, and special days.
- Final price: `price = BASE_PRICE * (1 + λ * normalized_demand)`

####  Model 3: Competitive Model *(Optional / Simplified)*
- Adjusts price based on competition (e.g., neighbor lot prices).

  
     
5) **Real-time Visualization**:
   - The combined_prices stream is connected to Bokeh for interactive, real-time visualizations.
   - For each unique parking spot, a dedicated Bokeh plot is generated, displaying the price trends from all three models over time.
   - Panel is used to arrange and serve these Bokeh plots as an interactive dashboard, allowing users to observe the dynamic pricing behavior as the simulated data streams in.
     
6) **Pipeline Execution**:
   - The entire Pathway pipeline is executed using pw.run(), which continuously processes the simulated data stream and updates the Bokeh/Panel dashboard in real-time.

##  Repository Contents

| File | Description |
|------|-------------|
| `ParkWay.ipynb` | Main notebook with preprocessing, models, and visualization |
| `dataset.csv` | Original dataset used for training |
| `parkwaydatastream.csv.csv` | Preprocessed dataset used for streaming |
| `README.md` | Documentation for project |
| `ParkWay.pdf| Detailed explanation of models and assumptions |
---
Additional Content that I have added. How this model helps in solving real-life problems.
## 📈 Key Takeaways

- Pathway enables real-time streaming and transformation of structured data.
- Dynamic pricing improves parking lot efficiency compared to static models.
- Visualization with Bokeh provides clear insight into model behavior and trends.
- The system is modular, scalable, and ready for real-world parking management systems.

---
Additional Content that I have added. How this model helps in solving real-life problems.

