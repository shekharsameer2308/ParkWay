# Dynamic Pricing for Urban Parking Lots

**Summer Analytics 2025 Capstone Project**  
Hosted by Consulting & Analytics Club × Pathway

---

## Overview

This project simulates a real-time pricing engine for 14 urban parking lots using machine learning, economic intuition, and real-time data processing.

Static pricing leads to inefficiencies in utilization. Our goal is to build dynamic models that adjust parking prices intelligently based on demand, traffic, vehicle types, and competition.

---

## Tech Stack

- Python
- NumPy
- Pandas
- Pathway (Real-time data streaming)
- Bokeh (Real-time visualization)
- Google Colab
- GitHub

---

##  Architecture Diagram

```mermaid
graph TD
  A[Raw Parking Data - CSV] --> B[Pathway Streaming Engine]
  B --> C[Feature Extraction & Preprocessing]
  C --> D1[Model 1: Linear Pricing]
  C --> D2[Model 2: Demand-based Pricing]
  C --> D3[Model 3: Competitive Pricing]
  D1 --> E[Price Output]
  D2 --> E
  D3 --> E
  E --> F[Bokeh Visualization]
