# Hotel_Data_Processing


# 📝 Hotel Booking Data Cleaning Report

This README documents the data preprocessing steps applied to the hotel booking dataset.  
The objective was to prepare the dataset for a **cancellation prediction model** by ensuring data quality and avoiding data leakage.

---

## 🔎 Steps Performed

1. **Handling Missing Values**
   - `company`: Dropped (more than 50% missing values, not informative).
   - `agent`: Missing values replaced with **0**.
   - `country`: Missing values imputed with the **mode** (most frequent country).
   - `children`: Few missing values imputed with the **median**.

2. **Handling Outliers**
   - Applied the **IQR method** to cap extreme values in:
     - `adr`
     - `lead_time`
   - This prevents unrealistic values from skewing the model.

3. **Duplicates**
   - Found **32,298 duplicate rows** (≈55% of dataset).
   - All duplicates were removed → kept only **unique rows**.

4. **Data Types**
   - Converted `reservation_status_date` into proper datetime format.
   - Fixed binary variables (e.g., `is_repeated_guest`) to ensure only **0/1** values.

5. **Feature Engineering**
   - Added new features:
     - `total_guests` = adults + children + babies
     - `total_nights` = stays_in_weekend_nights + stays_in_week_nights
     - `is_family` = 1 if children + babies > 0, else 0

6. **Data Leakage**
   - Dropped **reservation_status** and **reservation_status_date**  
     → because they contain future information not available at prediction time.

7. **Encoding Categorical Variables**
   - One-Hot Encoding applied to:
     - `meal`
     - `market_segment`
     - `deposit_type`
     - `customer_type`
   - High-cardinality column `country` → encoded using frequency encoding.

8. **Final Dataset Split**
   - Split data into **train (80%)** and **test (20%)** sets with `random_state=42`.

---

## ✅ Final Notes
- The cleaned dataset is now ready for **model building**.
- The preprocessing ensures:
  - No data leakage.
  - Robust handling of missing values, outliers, and duplicates.
  - Correct data types and engineered features for better predictive power.

