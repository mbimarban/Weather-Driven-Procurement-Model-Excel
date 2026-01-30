# 🌧️ Weather-Driven Procurement Model (Excel)

Excel-based weather-driven demand forecasting and procurement planning (Regression → Safety Stock → ROP → MOQ order decision)

---

## 📊 Project Overview

This case study demonstrates how to use **weather signals** (Rainfall, Temperature, Wind) to **forecast demand** for umbrellas and translate that forecast into a **procurement decision** (Safety Stock, Reorder Point, Order Quantity).

**Business Goal:** Help Procurement Manager decide *how much* and *when* to order based on weather forecasts.

---

## 📁 File Structure

| Sheet | Description |
|-------|-------------|
| `Data` | Historical data (19 months): Rainfall, Temperature, Wind, Sales |
| `Regression_Output` | Simple regression (Rainfall only) — R² = 82% |
| `Procurement_Plan` | ROP/Safety Stock calculator (1 variable) |
| `Regression_Output_Weather` | Multiple regression (Rain + Temp + Wind) — R² = 90% |
| `Procurement_Plan_Weather` | Full procurement calculator (3 variables) |

---

## 🔢 Methodology

### 1. Regression Model (Driver-Based Forecasting)

**Simple model (1 variable):**
```
Demand = Intercept + b_Rainfall × Rainfall
```
- R² = 0.822 (82% of demand variability explained)
- +1 mm rainfall → +47 units sold

**Extended model (3 variables):**
```
Demand = Intercept + b_Rain × Rain + b_Temp × Temp + b_Wind × Wind
```
- R² = 0.904 (90% explained)
- Rainfall & Temperature: statistically significant
- Wind: not significant (p > 0.05)

---

### 2. Procurement Logic (Forecast → Order Decision)
```
Demand_Forecast → DLT → Safety Stock → ROP → Order Qty → MOQ
```

| Step | Formula | Description |
|------|---------|-------------|
| **Demand Forecast** | `Intercept + b×Weather` | Expected demand from weather |
| **DLT** | `Demand × Lead_Time_months` | Demand During Lead Time |
| **Safety Stock** | `z × σ × √LT` | Buffer for forecast uncertainty |
| **ROP** | `DLT + Safety Stock` | Reorder Point trigger |
| **Order Qty** | `MAX(0, ROP - Inventory Position)` | How much to order |
| **Order MOQ** | `CEILING.MATH(Order, MOQ)` | Rounded to minimum order qty |

---

## 📈 Key Results (January 2025 Example)

**Inputs:**
- Forecast Rain: 90 mm
- Forecast Temp: 5°C
- Forecast Wind: 18 km/h
- Service Level: 95%
- Lead Time: 30 days

**Outputs:**
| Metric | Value |
|--------|-------|
| Demand Forecast | 3,156 units |
| Safety Stock | 668 units |
| ROP | 3,824 units |
| Inventory Position | 2,800 units |
| **Order Qty (MOQ)** | **1,200 units** |
| Reorder Flag | 🔴 ORDER |

---

## 🛠️ How to Use

1. Open `Umbrella_Company_Procurement_Model_Weather.xlsx`
2. Go to sheet **Procurement_Plan_Weather**
3. Update inputs:
   - `Forecast_Rain_mm_Jan25`
   - `Forecast_Temp_C_Jan25`
   - `Forecast_Wind_kmh_Jan25`
   - `StockOnHandW`, `OnOrderW`, `MOQW`
4. Read the decision:
   - `Reorder_FlagW` → ORDER / OK
   - `Order_Q_MOQ_Jan25W` → final order quantity

---

## 💡 Skills Demonstrated

- ✅ Multiple Linear Regression in Excel
- ✅ Driver-based demand forecasting
- ✅ Safety Stock & Reorder Point calculation
- ✅ Named ranges and structured references
- ✅ Conditional formatting for decision flags
- ✅ Procurement planning logic

---

## 👤 Author

**Marcin Banach**
- GitHub: [@mbimarban](https://github.com/mbimarban)

---

⭐ If you found this project helpful, please star this repository!
