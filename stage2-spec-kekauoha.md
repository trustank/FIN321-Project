Created by: Trustan Kekauoha  
Date created: 11/06/25  
Date updated: 11/06/25  
Version: 1.0

**Problem statement:** The company faces foreign exchange exposure from a €8,000,000 receivable due in one year. USD proceeds are at risk if the euro weakens against the dollar. The primary risk is that a declining EUR/USD spot rate will reduce the USD cash inflow, potentially impacting profit and cash flow planning. This analysis evaluates hedging strategies to mitigate this FX risk.

1. **Objective**  
- To model USD proceeds from a €8,000,000 receivable under three hedging strategies: forward contract, money-market hedge, and EUR put option as well as identify which hedge best protects revenue and exchange rate fluctuations.  
2. **Scope**  
- In Scope:  
  - One-year hedging analysis  
  - Forward, money-market, and EUR put option  
  - Sensitivity analysis using different future EUR/USD spot rates  
- Out-of-scope:  
  - Multi-year hedges or swaps  
  - Forecasting foreign exchange rates or interest rates  
  - Transaction costs  
3. **Inputs**

| Input | Value | Description |
| ----- | ----- | ----- |
| Receivable | 8,000,000 | Amount in EUR |
| Spot EUR/USD (S) | 1.17 | Current spot rate |
| Forward EUR/USD (F) | 1.0890 | One-year forward rate |
| USD 1-year interest rate (i(\_{USD})) | 0.0425 | From memo |
| EUR 1-year interest rate (i(\_{EUR})) | 0.0215 | From memo |
| Option strike (K) | 1.17 | Set near current spot |
| Option premium (P) | 0.021 | Per euro |
| Scenario future spot rates (S(\_{future})) | Various | For sensitivity analysis |

- Forward rate formula: SpotRate \* (1 \+ USD\_Rate) / (1 \+ EUR\_Rate)

4. **Assumptions & Constraints**  
- Interest rates are based on annualized simple rates (USD 4.25%, EUR 2.15%).  
- Transaction costs, bid-ask spreads, and taxes are ignored.  
- Hedging strategies assume access to standard market instruments (forwards, money-market loans, options).  
- The option is European style and can only be exercised at maturity.  
- Future spot rates are hypothetical for sensitivity analysis; actual market movements may vary.

5. **Workflow/Steps**  
   1. Set up Inputs section in Excel  
   2. Forward hedge: 8000000 \* ForwardRate  
   3. Money-market hedge: (8000000 / (1 \+ EUR\_Rate)) \* SpotRate \* (1 \+ USD\_Rate)  
   4. Option hedge: \= MAX(Strike \- FutureSpot, 0\) \* 8000000 \- (Premium \* 8000000\)  
   5. Unhedged position: \= 8000000 \* FutureSpot  
   6. Build a summary table comparing USD proceeds for all hedge options.  
   7. Run sensitivity analysis using multiple FutureSpot values (e.g., 1.05, 1.10, 1.20).  
   8. Perform sensitivity analysis by varying future EUR/USD spot rates (e.g., 1.05, 1.10, 1.20) to observe the impact on USD proceeds for each hedge strategy. Results should be visualized in a chart to highlight the effectiveness of each hedge across different exchange-rate scenarios.

6. **Expected outputs**

| Hedge | USD Proceeds | Excel Formula |
| ----- | ----- | ----- |
| Forward | 8000000 × 1.0890 | \=8000000\*ForwardRate |
| Money Market | (8,000,000 ÷ (1+0.0215)) × 1.17 × (1+0.0425) | \=(8000000/(1+EUR\_Rate))\*SpotRate\*(1+USD\_Rate) |
| Option | max(1.17 − S(\_{future}),0) × 8,000,000 − 0.021 × 8,000,000 | \=MAX(Strike-FutureSpot,0)\*8000000-(Premium\*8000000) |
| Unhedged | 8,000,000 × S(\_{future}) | \=8000000\*FutureSpot |

7. **Evaluation Criteria**  
- Accuracy: Formulas produce correct USD proceeds  
- Clarity: Inputs, calculations, and tables are clearly labeled  
- Reproducibility: Results can be replicated using the same inputs  
- Visualization: Tables/charts are labeled and readable  
- Alignment: Model follows class examples and defines hedge types correctly

8. **AI Prompts**  
- “Create an Excel spreadsheet that calculates USD proceeds from a €8,000,000 receivable using forward, money-market, and EUR put option hedges, with editable inputs and a summary table.”  
- “Explain the difference between forward, money-market, and option hedges in simple terms for MBA students.”  
- “Generate Excel formulas to calculate net USD proceeds for each hedge given spot, forward, interest rates, strike, and premium inputs.”