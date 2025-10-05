# Mutual Fund vs NIFTY Daily Analysis

This script analyzes how selected mutual funds perform **relative to the NIFTY index** on a **daily basis**.

It:
- Fetches mutual fund NAV data from [`https://api.mfapi.in`](https://api.mfapi.in)
- Fetches daily NIFTY index data using Yahoo Finance (`yfinance`)
- Computes **daily start-end prices**, **daily percentage changes**, and **correlations**
- Compares fund movement with NIFTY movement per day
- Creates an Excel report with:
  - One sheet per mutual fund (with daily NAV, fund % change, and NIFTY % change)
  - A summary sheet (first sheet) summarizing performance metrics
  - NIFTY start, end, and percent change for each day in every sheet

---

## 🧩 Features

- Automatic matching of user-specified fund names with the correct scheme name using fuzzy logic.
- Daily comparison of **fund NAV** vs **NIFTY closing value**.
- Correlation and “with market” percentage (fund moves in the same direction as NIFTY).
- Capture ratios (Up/Down capture).
- Excel output with **colored summary table** for quick visualization.

---

## 🧠 How It Works

1. The script fetches all available mutual fund schemes from `mfapi.in`.
2. For each query in `FUND_QUERIES`, it finds the best matching scheme.
3. NAV data for the last `DAYS` (default: 30) is fetched.
4. NIFTY data for the same range is fetched from Yahoo Finance.
5. The script:
   - Calculates **start**, **end**, and **percent change** for both NIFTY and the mutual fund **per day**.
   - Compares them side-by-side.
   - Computes metrics such as correlation, up/down capture, and behavior.
6. Outputs a formatted Excel file with all results.

---

## 📦 Installation

Clone or download this repository, then install dependencies:

```bash
pip install -r requirements.txt
```

---

## ⚙️ Usage

Run the script directly:

```bash
python mf_vs_nifty_analysis.py
```

### Optional Edits:
- Modify `FUND_QUERIES` at the top of the script to include the funds you want to analyze.
- Adjust `DAYS` (default = 30) to change the analysis window.
- The Excel file will be saved as:

```
mf_vs_nifty_YYYYMMDD_HHMMSS.xlsx
```

---

## 🧾 Output

### 🟩 **Summary Sheet** (First Sheet)
| Column | Description |
|--------|-------------|
| Query | Your original fund name query |
| Matched Scheme | Best match found on `mfapi.in` |
| Scheme Code | Unique fund code |
| Correlation | Fund vs NIFTY correlation |
| With Market % | % of days fund moved in same direction as NIFTY |
| Avg Fund Return (%) | Average daily % change of fund |
| Avg NIFTY Return (%) | Average daily % change of NIFTY |
| Up Capture (%) | Fund's performance on NIFTY up days |
| Down Capture (%) | Fund's performance on NIFTY down days |
| Behavior | “With Market”, “Against Market”, or “Low Corr” |
| Market Tolerance | High / Medium / Low |
| NIFTY Start | NIFTY opening price for the range |
| NIFTY End | NIFTY closing price for the range |
| NIFTY % Change | Overall % change of NIFTY over range |

---

### 📊 **Per-Fund Sheet**
Each sheet contains daily data:

| Date | Fund NAV | Fund Start | Fund End | Fund % Change | NIFTY Start | NIFTY End | NIFTY % Change |

---

## 🧩 Example Output (Summary)

| Query | Correlation | Up Capture (%) | Down Capture (%) | Behavior | Market Tolerance |
|-------|-------------|----------------|------------------|-----------|------------------|
| Parag Parikh ELSS | 0.78 | 115 | 85 | With Market | High |
| Bajaj Finserv ELSS | 0.45 | 95 | 105 | Low Corr | Medium |

---

## 🧰 Dependencies

- `requests` — for API calls to mfapi.in  
- `pandas` & `numpy` — for data processing  
- `yfinance` — for fetching NIFTY data  
- `openpyxl` — for Excel writing and formatting  

---

## ⚠️ Notes

- API data from `https://api.mfapi.in` can sometimes lag by 1–2 days.
- NIFTY data comes from Yahoo Finance (`^NSEI`).
- Some mutual funds may not have NAV data for weekends or holidays, so alignment is done on available dates.

---

## 🧑‍💻 Author

**Abhijeet Pise**  
📅 October 2025  
📈 For data analysis, mutual fund insights, and automation.
