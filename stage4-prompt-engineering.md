You are a financial modeling assistant and finance technologist.

# **GOAL**

Create a complete, professional **Excel (.xlsx)** model that evaluates FX hedging strategies for a U.S. firm with a **EUR receivable**. The model must be **auditable**, clearly formatted, and ready for submission.

# **DELIVERABLES**

Return:

1. A downloadable .xlsx workbook  
2. A brief build summary (sheet names \+ what’s where)  
3. A Formula\_Map sheet listing: Cell, Label, Formula, Inputs/Named Ranges used

# **CONTEXT FILES (GitHub)**

Use these as references (do not rely on them being available; the prompt is self-contained):

* [https://github.com/trustank/FIN321-Project/blob/main/stage2-spec-kekauoha.md](https://github.com/trustank/FIN321-Project/blob/main/stage2-spec-kekauoha.md)  
* [https://github.com/trustank/FIN321-Project/blob/main/stage3-model-Kekauoha.xlsx](https://github.com/trustank/FIN321-Project/blob/main/stage3-model-Kekauoha.xlsx)

# **CONTEXT**

Scenario: A U.S.-based pharmaceutical exporter expects a **EUR receivable** at maturity and reports in USD. EUR/USD volatility creates risk to USD proceeds. Build a spreadsheet that computes USD proceeds under:

* Forward hedge  
* Money-market hedge (3-step)  
* Option hedges (EUR put and EUR call, net of premium)  
* Sensitivity analysis for ending spot rates (S\_T)

# **INPUT VARIABLES (ALL VALUES MUST BE EXPLICIT)**

Use the following scenario-specific values for this run:

**Known / Provided**

* FC\_AMT \= 8,000,000 (EUR)  
* F0\_in \= 1.0890 (USD per EUR)  
* K\_PUT \= 1.17  
* K\_CALL \= 1.17  
* PREM\_PUT \= 0.021 (USD per EUR; no multiplier)  
* PREM\_CALL \= 0.026 (USD per EUR; no multiplier)  
* T\_DAYS \= 365  
* T\_YRS \= T\_DAYS/365

**Market Data (look up at runtime; if not possible use fallback values below)**

* S0\_in \= current EUR/USD spot (Yahoo Finance or XE)  
* R\_USD \= current 1-year USD rate (state the exact instrument/source used)  
* R\_FC \= current 1-year EUR rate (state the exact instrument/source used)

**Fallback values if lookup is unavailable**

* S0\_in \= 1.17  
* R\_USD \= 0.0425  
* R\_FC \= 0.0215

# **SPREADSHEET REQUIREMENTS**

## **1\) Workbook \+ Sheets**

Create a workbook with these sheets:

* Model  
* Formula\_Map

## **2\) Named Ranges (REQUIRED — DO NOT INVENT NAMES)**

Create named ranges exactly:  
FC\_AMT, S0\_in, F0\_in, R\_USD, R\_FC, K\_PUT, K\_CALL, PREM\_PUT, PREM\_CALL, T\_DAYS, T\_YRS

## **3\) Color Coding (REQUIRED)**

* Yellow \= Inputs / decision variables  
* Blue \= Assumptions / conventions / data sources  
* Green \= Formula cells  
* Gray \= Outputs / KPIs

## **4\) Model Components (REQUIRED)**

On Model, include labeled sections:

1. INPUTS (Yellow) \+ Data Sources & Timestamp (Blue)  
2. FORWARD HEDGE (Green formulas \+ Gray KPI)  
3. MONEY MARKET HEDGE (3-step: borrow → convert → invest)  
4. OPTION HEDGES (premium totals \+ payoff logic)  
5. SENSITIVITY TABLE (±5% around S0\_in)  
6. OUTPUT SUMMARY / KPIs (Gray)  
7. NOTES / ASSUMPTIONS (Blue)

# **MODEL LOGIC (PSEUDOCODE)**

## **A) Forward Hedge**

USD\_FWD \= FC\_AMT \* F0\_in

## **B) Money Market Hedge (EUR receivable)**

EUR\_BORROW \= FC\_AMT / (1 \+ R\_FC \* T\_YRS)  
USD\_TODAY \= EUR\_BORROW \* S0\_in  
USD\_MM \= USD\_TODAY \* (1 \+ R\_USD \* T\_YRS)

## **C) Option Hedges (Net of Premium)**

PUT\_PREM\_TOTAL \= FC\_AMT \* PREM\_PUT  
CALL\_PREM\_TOTAL \= FC\_AMT \* PREM\_CALL

For each ending spot S\_T:  
USD\_PUT\_NET \= IF(S\_T \< K\_PUT, K\_PUT*FC\_AMT \- FC\_AMT*PREM\_PUT, S\_T*FC\_AMT \- FC\_AMT*PREM\_PUT)  
USD\_CALL\_NET \= IF(S\_T \> K\_CALL, K\_CALL*FC\_AMT \- FC\_AMT*PREM\_CALL, S\_T*FC\_AMT \- FC\_AMT*PREM\_CALL)

(Also compute unhedged for comparison)  
USD\_UNHEDGED \= S\_T \* FC\_AMT

## **D) Sensitivity Table (±5% around S0\_in)**

Create S\_T values from:

* 0.95*S0\_in to 1.05*S0\_in  
* in 1% increments  
* total rows: 11 scenarios

For each S\_T compute columns:

* Forward proceeds (constant)  
* Money market proceeds (constant)  
* Put net proceeds  
* Call net proceeds  
* Unhedged proceeds

# **OUTPUT REQUIREMENTS (KPIs)**

In a Gray summary block show:

* USD\_FWD  
* USD\_MM  
* Parity\_Diff \= USD\_MM \- USD\_FWD  
* Parity\_Check \= IF(ABS(Parity\_Diff) \< 1000, "PASS", "CHECK INPUTS")  
* MIN/MAX of USD\_PUT\_NET across scenarios  
* MIN/MAX of USD\_CALL\_NET across scenarios  
* Recommendation placeholder (Stage 5\)

# **VERIFICATION (REQUIRED)**

1. Validate parity between forward and money-market hedges (show Parity\_Diff and PASS/CHECK).  
2. Confirm all named ranges exist and formulas reference them.  
3. Build Formula\_Map with: Sheet, Cell, Label, Formula, Named Ranges used.

# **EXPORT**

Return a downloadable .xlsx file that meets all requirements above.

