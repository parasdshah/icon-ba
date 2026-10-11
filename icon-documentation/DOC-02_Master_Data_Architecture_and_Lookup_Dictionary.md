# DOC-02: MASTER DATA ARCHITECTURE, REFERENCE LOOKUP DICTIONARY & DEPENDENCY MATRIX

**Document Reference:** `DOC-02`  
**System Name:** Next-Generation Internal Ratings Platform (IRP - Project ICON)  
**Parent Document:** `[REF: DOC-00 §3.0]`  
**Module Type:** Platform Reference Architecture & Master Data Specification  
**Classification:** Confidential / System Architecture Specification  

---

## 1.0 Master Data Governance & Temporal Versioning Framework

All lookups, benchmark quartiles, regulatory mapping tables, and scoring parameters in Project ICON are managed under strict metadata governance:
- **Bi-Temporal Validity:** Every lookup entry carries `effective_from`, `effective_to`, `version_number`, and `approval_status` (Draft, Published, Deprecated).
- **Zero Hard-Coding:** No scorecard formula, collateral haircut, or regulatory risk-weight may be hardcoded in application logic.
- **Cascading Triggers:** Alterations to parent masters trigger automated downstream re-validation or invalidate active draft rating sessions.

---

## 2.0 Master Dictionary 1: Regulatory Industry, NIC Codes & PSL Taxonomy

### 2.1 Master Specification & Metadata
- **Master Key:** `MST_SECTOR_INDUSTRY_NIC`
- **Upstream Dependency:** Ministry of Statistics and Programme Implementation (MoSPI) NIC-2008 Standard.
- **Downstream Dependency:** Selects Financial Spreading Template `[REF: DOC-03 §1.0]`, selects Benchmark Ratios `[REF: DOC-02 §6.0]`, and routes Qualitative Industry Questions `[REF: DOC-04 §1.2]`.

### 2.2 Domain Values & Cascading Matrix
| NIC-2008 Code | Industry / Sub-Sector Name | Sector Category | RBI Priority Sector Lending (PSL) Category | ESG Risk Tier | Template Route `[REF: DOC-03]` | Effective Window |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `24101` | Manufacture of Pig Iron & Sponge Iron | Manufacturing - Metals | Non-PSL / Large Corporate | Tier-3 (High ESG) | `TMPL_CORP_INDAS` | 2020-04-01 to 9999-12-31 |
| `24102` | Hot-Rolled and Cold-Rolled Steel Products | Manufacturing - Metals | Non-PSL / Large Corporate | Tier-3 (High ESG) | `TMPL_CORP_INDAS` | 2020-04-01 to 9999-12-31 |
| `21001` | Manufacture of Allopathic Pharmaceuticals | Healthcare & Pharma | Non-PSL / PSL Export Credit | Tier-2 (Medium ESG) | `TMPL_CORP_INDAS` | 2020-04-01 to 9999-12-31 |
| `01111` | Growing of Wheat & Cereals | Agriculture | PSL - Direct Agriculture | Tier-1 (Low ESG) | `TMPL_AGRI_CORP` | 2020-04-01 to 9999-12-31 |
| `41001` | Construction of Residential Buildings | Real Estate | PSL Housing (< ₹35 Lakhs) / Non-PSL CRE | Tier-2 (Medium ESG) | `TMPL_CRE_PROJECT` | 2020-04-01 to 9999-12-31 |
| `42101` | Construction of Motorways, Highways, Toll Roads | Infrastructure | Infra Debt Sub-Sector (RBI Master List) | Tier-2 (Medium ESG) | `TMPL_INFRA_PROJECT`| 2020-04-01 to 9999-12-31 |
| `64191` | Commercial Banking & Deposit Taking | Financial Institutions | Not Applicable | Tier-1 (Low ESG) | `TMPL_FI_BANK` | 2020-04-01 to 9999-12-31 |
| `64920` | NBFC - Non-Banking Credit Granting | NBFCs / Financial Services | PSL - On-lending to Priority Sector | Tier-1 (Low ESG) | `TMPL_NBFC_SBR` | 2022-10-01 to 9999-12-31 |
| `13111` | Preparation and Spinning of Cotton Fibers | Textiles & Apparels | PSL - MSME Manufacturing | Tier-2 (Medium ESG) | `TMPL_CORP_INDAS` | 2020-04-01 to 9999-12-31 |
| `62011` | Software Development & IT Services | Information Technology | Non-PSL Services / MSME Services | Tier-1 (Low ESG) | `TMPL_CORP_INDAS` | 2020-04-01 to 9999-12-31 |

---

## 3.0 Master Dictionary 2: Internal Rating Scale (20-Grade Master Scale)

### 3.1 20-Grade Master Scale Specification
Project ICON standardizes all non-retail exposures onto a 20-grade master scale with precise annualized 1-year Probability of Default (PD) midpoints, mapped to Basel III asset classifications:

| Internal Grade | Alpha Code | Grade Name / Classification | 1-Yr PD Midpoint (%) | 1-Yr PD Floor (%) | 1-Yr PD Cap (%) | Investment Grade Status | Default Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **G01** | `AAA` | Exceptional Credit Quality | `0.03%` | `0.01%` | `0.04%` | Investment Grade | Performing |
| **G02** | `AA+` | High Credit Quality - Upper | `0.06%` | `0.05%` | `0.08%` | Investment Grade | Performing |
| **G03** | `AA` | High Credit Quality - Mid | `0.10%` | `0.09%` | `0.12%` | Investment Grade | Performing |
| **G04** | `AA-` | High Credit Quality - Lower | `0.15%` | `0.13%` | `0.18%` | Investment Grade | Performing |
| **G05** | `A+` | Strong Credit Quality - Upper | `0.22%` | `0.19%` | `0.27%` | Investment Grade | Performing |
| **G06** | `A` | Strong Credit Quality - Mid | `0.32%` | `0.28%` | `0.38%` | Investment Grade | Performing |
| **G07** | `A-` | Strong Credit Quality - Lower | `0.45%` | `0.39%` | `0.54%` | Investment Grade | Performing |
| **G08** | `BBB+` | Adequate Credit Quality - Upper | `0.65%` | `0.55%` | `0.78%` | Investment Grade | Performing |
| **G09** | `BBB` | Adequate Credit Quality - Mid | `0.95%` | `0.79%` | `1.15%` | Investment Grade | Performing |
| **G10** | `BBB-` | Adequate Credit Quality - Lower | `1.45%` | `1.16%` | `1.80%` | Investment Grade (Threshold) | Performing |
| **G11** | `BB+` | Moderate Credit Risk - Upper | `2.20%` | `1.81%` | `2.70%` | High Yield (Sub-Investment) | Performing |
| **G12** | `BB` | Moderate Credit Risk - Mid | `3.30%` | `2.71%` | `4.10%` | High Yield (Sub-Investment) | Performing |
| **G13** | `BB-` | Moderate Credit Risk - Lower | `4.80%` | `4.11%` | `5.80%` | High Yield (Sub-Investment) | Performing |
| **G14** | `B+` | High Credit Risk - Upper | `6.80%` | `5.81%` | `8.20%` | High Yield (Sub-Investment) | Performing |
| **G15** | `B` | High Credit Risk - Mid | `9.50%` | `8.21%` | `11.50%` | High Yield (Sub-Investment) | Performing |
| **G16** | `B-` | High Credit Risk - Lower | `13.50%` | `11.51%` | `16.00%` | High Yield (Sub-Investment) | Performing |
| **G17** | `CCC+` | Substantial Vulnerability - Upper | `19.00%` | `16.01%` | `23.00%` | Vulnerable / Stressed | Performing |
| **G18** | `CCC` | Substantial Vulnerability - Mid | `28.00%` | `23.01%` | `35.00%` | Vulnerable / Stressed | Performing |
| **G19** | `CC / C` | Imminent Danger of Default | `45.00%` | `35.01%` | `75.00%` | Near Default | Performing / SMA-2 |
| **G20** | `D` | Default / In Bankruptcy / NCLT | `100.00%` | `75.01%` | `100.00%`| Default | Default (IRACP NPA) |

---

## 4.0 Master Dictionary 3: External Credit Rating Agency (CRA) & Basel Risk Weight Mapping

### 4.1 CRA Scale Standardization & RBI Risk Weight Engine
Master Key: `MST_CRA_RATING_MAPPING`. Used for external rating benchmarking, Basel III Standardized Approach Risk Weighted Asset (RWA) calculation, and external rating floor checks `[REF: DOC-05 §3.0]`.

| Long-Term Rating (CRISIL, ICRA, CARE, India Ratings, Acuité) | Short-Term Rating Equivalent (P1 / A1+ Scale) | Basel III Risk Weight (Claims on Corporates - Unrated = 100%) | Basel III Risk Weight (Claims on Banks - Scheduled) | Regulatory Provisioning Floor |
| :--- | :--- | :--- | :--- | :--- |
| `AAA` | `A1+` | `20%` | `20%` | `0.40%` (Standard) |
| `AA+`, `AA`, `AA-` | `A1+` | `30%` | `30%` | `0.40%` (Standard) |
| `A+`, `A`, `A-` | `A1` | `50%` | `50%` | `0.40%` (Standard) |
| `BBB+`, `BBB`, `BBB-`| `A2+, A2, A3` | `100%` | `50%` | `0.40%` (Standard) |
| `BB+` to `BB-` | `A4+` | `150%` | `100%` | `0.40%` (Standard) |
| `B+` to `C` | `A4` | `150%` | `150%` | `0.40%` (Standard) |
| `D` | `D` | `150%` | `150%` | `15.00%` to `100.00%` (NPA) |

---

## 5.0 Master Dictionary 4: Chart of Accounts (COA) Taxonomy & Ind-AS / I-GAAP Reconciliation

### 5.1 Standardized Balance Sheet & P&L Taxonomy
Master Key: `MST_COA_TAXONOMY`. Maps Schedule III Division II (Ind-AS), Division I (Indian GAAP), and IFRS (IAS 1/7) line items into normalized canonical identifiers `[REF: DOC-03 §1.0]`. *(For the exhaustive 4-level hierarchical tree, line-by-line leaf nodes, Cash Flow statements, and ambiguity resolution rules, refer to [DOC-03A: Master Chart of Accounts Taxonomy & Cross-GAAP Mapping](file:///c:/Users/user/icon-ba/icon-documentation/DOC-03A_Master_Chart_of_Accounts_IndAS_IGAAP_IFRS_Taxonomy.md)).*

| Canonical Field Code | Canonical Field Description | Ind-AS Schedule III Line Reference | Indian GAAP Schedule III Line Reference | Financial Category | Normalization Rule `[REF: DOC-03 §3.0]` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `BS_EQ_SHARE_CAP` | Paid-up Equity Share Capital | Equity -> Equity Share Capital | Share Capital | Net Worth | Direct Value |
| `BS_EQ_RES_SURP` | Other Equity / Reserves & Surplus | Equity -> Other Equity | Reserves and Surplus | Net Worth | Excludes Revaluation Reserve |
| `BS_DT_PROMOTER_SUB`| Subordinated Quasi-Equity Loans | Non-Current Liabilities -> Borrowings | Unsecured Loans from Promoters | Quasi-Equity | Reclassified to Equity if subordinated |
| `BS_NCL_BORR_TERM` | Long Term Secured Borrowings | Non-Current Liabilities -> Borrowings | Long-Term Borrowings | Long-Term Debt | Excludes current maturities |
| `BS_CL_ST_BORR_WC` | Short Term Working Capital Debt | Current Liabilities -> Borrowings | Short-Term Borrowings | Working Capital Debt | Includes CC/OD, WCDL, Buyers Credit |
| `BS_CL_CURR_MAT_LTD`| Current Maturities of Long Term Debt | Current Liabilities -> Other Fin Liab | Other Current Liabilities | Current Debt | Added to Total Debt |
| `PL_REV_OPS` | Revenue from Operations (Gross) | Revenue from Operations | Revenue from Operations | P&L Topline | Excludes GST |
| `PL_EXP_RAW_MAT` | Cost of Materials Consumed | Expenses -> Cost of Materials Consumed | Cost of Materials Consumed | Operating Expense | Direct Value |
| `PL_EXP_FIN_COST` | Finance Costs / Interest Expense | Expenses -> Finance Costs | Finance Costs | Finance Cost | Segregates interest vs bank charges |
| `PL_EXP_DEP_AMORT` | Depreciation & Amortization Expense | Expenses -> Depreciation and Amortisation | Depreciation and Amortisation | Non-Cash Expense | Added back for EBITDA calculation |

---

## 6.0 Master Dictionary 5: Benchmark Ratios & Statistical Industry Quartiles

### 6.1 Ratio Definitions & Percentile Distribution Matrix
Master Key: `MST_RATIO_BENCHMARKS`. The system maintains dynamic statistical quartiles ($P_{10}, P_{25}, P_{50}, P_{75}, P_{90}$) across sub-industries to govern scoring splines in `DOC-04 §1.1`:

| Ratio Code | Mathematical Formula | Directional Risk | Steel Industry (NIC: 24101) P10 / P50 / P90 | Pharma Industry (NIC: 21001) P10 / P50 / P90 | CRE Project (NIC: 41001) P10 / P50 / P90 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `RATIO_TOL_ATNW` | `(Total Debt + Current Liabilities) / Adjusted TNW` | Lower is Better | `4.2x / 1.8x / 0.8x` | `2.5x / 1.1x / 0.4x` | `5.5x / 2.8x / 1.2x` |
| `RATIO_ISCR` | `(PBIT + Depr) / Gross Interest Expense` | Higher is Better | `1.1x / 2.8x / 6.5x` | `2.2x / 6.0x / 14.5x` | `0.8x / 1.8x / 3.5x` |
| `RATIO_DSCR` | `(PAT + Depr + Int) / (Int + CMLTD)` | Higher is Better | `0.9x / 1.6x / 2.8x` | `1.3x / 2.4x / 5.2x` | `1.0x / 1.5x / 2.4x` |
| `RATIO_CURR_RATIO` | `Current Assets / Current Liabilities` | Higher is Better | `0.95 / 1.28 / 1.75` | `1.20 / 1.65 / 2.40` | `1.05 / 1.40 / 2.10` |
| `RATIO_OP_MARGIN` | `(Operating Profit / Net Sales) * 100` | Higher is Better | `6.5% / 14.2% / 22.0%` | `11.0% / 19.5% / 28.5%`| `15.0% / 24.0% / 38.0%`|
| `RATIO_NWC_DAYS` | `(NWC / Net Sales) * 365` | Lower is Better | `120 d / 75 d / 35 d` | `140 d / 95 d / 50 d` | `320 d / 180 d / 90 d` |
| `RATIO_ROCE` | `PBIT / (Adjusted TNW + Long Term Debt)` | Higher is Better | `5.0% / 12.5% / 21.0%` | `8.5% / 17.0% / 26.0%` | `6.0% / 13.0% / 20.0%` |

---

## 7.0 Master Dictionary 6: Facility Types & RBI Credit Conversion Factors (CCF)

### 7.1 Credit Facility Classification & CCF Mandates
Master Key: `MST_FACILITY_TYPE`. Controls whether facility is Fund-Based or Non-Fund-Based, determines CCF for EAD calculation `[REF: DOC-08 §2.0]`, and dictates collateral coverage rules:

| Facility Code | Facility Description | Fund / Non-Fund | Default Tenure | Standard CCF (Basel III / RBI) | Primary Purpose |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `FB_CC_OD` | Cash Credit / Working Capital Overdraft | Fund-Based | 12 Months (Revolving) | `20%` (Undrawn) | Working Capital against Stocks & Debtors |
| `FB_WCDL` | Working Capital Demand Loan | Fund-Based | 30 to 180 Days | `20%` (Undrawn) | Short-Term Peak Inventory Funding |
| `FB_TERM_LOAN`| Rupee Term Loan (Capex / Expansion) | Fund-Based | 3 to 12 Years | `50%` to `75%` (Undrawn) | Fixed Asset Creation / Project Capex |
| `FB_BILL_DISC`| Bills Discounted / Inland LC Bill Purchase | Fund-Based | 30 to 90 Days | `20%` (Undrawn) | Trade Receivables Monetization |
| `NFB_PERF_BG` | Performance Bank Guarantee | Non-Fund-Based | 1 to 3 Years | `50%` | Performance of Contract / Tenders |
| `NFB_FIN_BG` | Financial Bank Guarantee | Non-Fund-Based | 1 to 5 Years | `100%` | Debt Servicing / Tax Dispute / EPC Guarantee |
| `NFB_DOC_LC` | Documentary Letter of Credit (Sight/Usance)| Non-Fund-Based | 90 to 180 Days | `20%` to `50%` | Import & Domestic Raw Material Purchases |
| `FX_FORWARD` | Foreign Currency Forward Derivative Line | Derivative | 1 to 24 Months | Current Exposure Method | Currency & Interest Rate Hedging |

---

## 8.0 Master Dictionary 7: Collateral Asset Classes, Charges & Haircut Engine

### 8.1 Collateral Asset Taxonomy & Mandatory Haircut Limits
Master Key: `MST_COLLATERAL_HAIRCUT`. Used directly by the Facility Risk Rating (FRR) Engine `[REF: DOC-06 §3.0]` to compute Net Realizable Collateral Value:

| Asset Class Code | Collateral Description | Minimum Haircut (Standard) | Maximum Haircut (Stressed) | Valuation Frequency Mandate | Valuation Aging Penalty Trigger |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `COL_CASH_FD` | Bank Fixed Deposit (Lien Marked) | `0.0%` | `5.0%` | Real-time Core Banking sync | None |
| `COL_GOV_SEC` | Sovereign Government Securities (G-Sec) | `2.0%` | `5.0%` | Daily MTM | None |
| `COL_LISTED_EQ` | Listed Shares (BSE/NSE Top 500) | `40.0%` | `50.0%` | Daily MTM | Dropped if market cap < ₹1000 Cr |
| `COL_IND_LAND` | Industrial Land & Factory Shed | `35.0%` | `45.0%` | Triennial (Every 3 years) | +15% Haircut if valuation > 3 yrs old |
| `COL_COMM_PROP`| Commercial Office / Retail Property | `30.0%` | `40.0%` | Triennial (Every 3 years) | +15% Haircut if valuation > 3 yrs old |
| `COL_RES_PROP` | Residential Flats & Plots | `25.0%` | `35.0%` | Triennial (Every 3 years) | +10% Haircut if valuation > 3 yrs old |
| `COL_PLANT_MACH`| Plant, Machinery & Specialized Equipment| `50.0%` | `65.0%` | Biennial (Every 2 years) | +20% Haircut if valuation > 2 yrs old |
| `COL_BOOK_DEBT_90`| Book Debts & Receivables (< 90 Days) | `25.0%` | `40.0%` | Monthly Stock Audit | +25% Haircut if audit delayed > 60 days |
| `COL_BOOK_DEBT_OLD`| Book Debts & Receivables (> 90 Days) | `85.0%` | `100.0%` | Monthly Stock Audit | Ineligible if disputed |
| `COL_STOCK_RM` | Stocks of Raw Materials & Finished Goods | `25.0%` | `40.0%` | Monthly Stock Audit | Excludes slow-moving inventory |

---

## 9.0 Master Dictionary 8: RBI IRACP Asset Classification Masters

### 9.1 Asset Classification Taxonomy & Mandatory Regulatory Provisions
Master Key: `MST_IRACP_ASSET_CLASS`. Triggers hard cap overlays in `DOC-05 §3.0` and informs expected credit loss provisioning:

| Classification Code | Category Name | Days Past Due (DPD) Threshold | Supervisory Definition | Standard Provision Rate | Hard System Rating Cap `[REF: DOC-05 §3.0]` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `STD_REGULAR` | Standard - Regular | `0 DPD` | Fully performing account | `0.40%` | No Cap (Unconstrained) |
| `STD_SMA_0` | Special Mention Account - 0 | `1 to 30 DPD` | Incipient stress signs | `0.40%` | Cap at `G08` (`BBB+`) |
| `STD_SMA_1` | Special Mention Account - 1 | `31 to 60 DPD` | Significant liquidity stress | `0.40%` | Cap at `G11` (`BB+`) |
| `STD_SMA_2` | Special Mention Account - 2 | `61 to 90 DPD` | High default risk / Pre-NPA | `0.40%` | Cap at `G13` (`BB-`) |
| `NPA_SUBSTANDARD`| Sub-Standard Asset | `91 DPD to 12 Months NPA` | Ceased to generate income | `15.00%` (Secured) / `25%` (Unsec) | **Hard Floor at G20 (`D`)** |
| `NPA_DOUBTFUL_1` | Doubtful Asset - D1 | `NPA for > 12 to 24 Months`| Substantial erosion of security | `25.00%` (Secured) / `100%` (Unsec)| **Hard Floor at G20 (`D`)** |
| `NPA_DOUBTFUL_2` | Doubtful Asset - D2 | `NPA for > 24 to 48 Months`| High loss potential | `40.00%` (Secured) / `100%` (Unsec)| **Hard Floor at G20 (`D`)** |
| `NPA_DOUBTFUL_3` | Doubtful Asset - D3 | `NPA for > 48 Months` | Extreme unlikelihood of recovery | `100.00%` | **Hard Floor at G20 (`D`)** |
| `NPA_LOSS` | Loss Asset | `Identified by Bank / RBI` | Entirely uncollectible / Written off| `100.00%` | **Hard Floor at G20 (`D`)** |

---

## 10.0 Master Dictionary 9: Override & Deviation Reason Codes

### 10.1 Permitted Subjective Notching Overrides
Master Key: `MST_OVERRIDE_REASON_CODES`. Used in `DOC-05 §3.2` to record and audit manual rating adjustments:

| Reason Code | Permitted Notch Direction | Permitted Range | Approval Authority Required `[REF: DOC-11 §3.0]` | Justification Document Mandate |
| :--- | :--- | :--- | :--- | :--- |
| `OVR_LIQ_BACKSTOP` | Upward Notch | +1 to +2 Notches | Chief Risk Officer (CRO) | Formal Sanction Letter of Committed Revolver |
| `OVR_COMMODITY_SUPER` | Downward Notch | -1 to -2 Notches | Head - Credit Risk Underwriting | Global Benchmark Commodity Drop Analysis |
| `OVR_GOV_CHANGE_REG` | Downward Notch | -1 to -3 Notches | Credit Approval Committee (CAC) | Regulatory Notification / Policy Revision Memo |
| `OVR_AUDITOR_ADVERSE` | Downward Notch | -2 Notches to Floor `G10` | Chief Risk Officer (CRO) | Qualified Audit Report / Disclaimer of Opinion |
| `OVR_PROMOTER_DISPUTE`| Downward Notch | -1 to -3 Notches | Credit Approval Committee (CAC) | NCLT Petition / Arbitration Filings |
