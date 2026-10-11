# MASTER PROMPT: INTERNAL RATINGS PLATFORM (IRP) PRODUCT NOTE SPECIFICATION
**Version:** 2.0.0 (Enhanced Institutional Edition)  
**Target Output:** Modular, Multi-Document Institutional Product Requirement & System Architecture Suite (PRD / FSD)  
**Industry Scope:** Non-Retail Corporate, Mid-Corporate, SME, NBFC, CRE & Infrastructure Credit Risk & Internal Rating Based (IRB) Platform for Scheduled Commercial Banks in India  
**Competitive Benchmark:** Moody’s Analytics CreditLens, CRISIL RAM, S&P Capital IQ Pro Scorecards, Finacle Credit Assessment  

---

```markdown
# INSTRUCTION TO THE AI SYSTEM / PRINCIPAL RISK & ENTERPRISE ARCHITECT

You are a Principal Enterprise Risk Architect, Senior Banking Business Analyst, and Lead Credit Risk Specialist with 20+ years of institutional experience architecting, building, deploying, and auditing mission-critical credit underwriting and rating platforms across Indian Tier-1 Scheduled Commercial Banks (State Bank of India, HDFC Bank, ICICI Bank, Axis Bank, Bank of Baroda, Punjab National Bank) and global financial technology firms (Moody's Analytics, CRISIL, S&P).

Your task is to generate a master-level, exhaustive, implementation-ready **Product Note (Product Requirements Document & System Functional Architecture Suite)** for a next-generation **Internal Ratings Platform (IRP)** tailored for the Indian non-retail banking ecosystem.

This platform is engineered to directly compete with and supersede **Moody’s Analytics CreditLens**, solving for Indian regulatory frameworks (RBI Master Directions on IRB, LEF, IRACP, Basel III, Ind-AS & I-GAAP duality, MCA/GSTN/CIBIL integrations, and CRILC), model flexibility, low-code financial template configuration, bi-temporal data versioning, comprehensive Facility/Issuer/Issue rating dualities, RAROC pricing, collateral haircut engines, and strict banking Non-Functional Requirements (NFRs).

---

## 1. DOCUMENT SUITE MODULARITY, NUMBERING & CROSS-LINKING SPECIFICATION

The generated Product Note MUST NOT be a single unorganized text block. It must be structured as an enterprise-grade **Modular Document Suite** with strict document numbering, explicit cross-linking anchors, and a master traceability matrix.

### 1.1 Document Index & Numbering Scheme
The generated documentation must be organized into 12 standalone yet strictly inter-linked modules:
- **`DOC-00`**: Executive Summary, Platform Vision & Enterprise Architecture Blueprint
- **`DOC-01`**: Obligor, Conglomerate Group & Corporate Hierarchy Engine
- **`DOC-02`**: Master Data Architecture, Reference Lookup Dictionary & Dependency Matrix
- **`DOC-03`**: Financial Spreading, Chart of Accounts & Normalization Template Engine
- **`DOC-04`**: Borrower Risk Rating (BRR) & Model Studio (Low-Code Scorecard Builder & Sandbox)
- **`DOC-05`**: Parental Support, Government/GRE Support & External Notch Modifiers
- **`DOC-06`**: Facility Risk Rating (FRR), Collaterals, Security Charges & Haircut Engine
- **`DOC-07`**: Issuer Rating vs. Issue Rating, Guarantors & Credit Enhancement Framework
- **`DOC-08`**: Limit, Exposure Architecture, Credit Conversion Factors (CCF) & RAROC Engine
- **`DOC-09`**: Model Versioning, Artifact Packaging, Release CI/CD & Deployment Pipeline
- **`DOC-10`**: Bi-Temporal Data Architecture, Time-Series Lookups & Rating Migration Analytics
- **`DOC-11`**: Audit Trail, Data Lineage, Four-Eyes Governance & Workflow State Machine
- **`DOC-12`**: Stakeholder Portals, Regulatory MIS & Mandatory Banking Non-Functional Requirements (NFRs)

### 1.2 Cross-Linking & Traceability Rules
- Every module must maintain standardized cross-reference tags in the format `[REF: DOC-XX §Y.Z]`. For example:
  - *Calculation of Facility LGD in `DOC-06 §3.2` must cite the Collateral Haircut Master in `DOC-02 §4.8` and the Facility Hierarchy in `DOC-08 §2.1`.*
  - *RAROC computation in `DOC-08 §4.0` must pull Borrower PD from `DOC-04 §5.0`, Facility LGD from `DOC-06 §3.0`, and Group Capital Allocation from `DOC-01 §3.0`.*
- Include a **Traceability & Dependency Matrix** in `DOC-00` mapping all upstream and downstream data flows across modules.

---

## 2. DETAILED FUNCTIONAL MODULE REQUIREMENTS

Every module must be developed with granular institutional depth, formulas, database schemas, and concrete Indian banking examples:

---

### MODULE DOC-00: EXECUTIVE SUMMARY & ENTERPRISE ARCHITECTURE BLUEPRINT
1. **Platform Objectives & Scope:** Non-retail credit underwriting, annual surveillance, mid-term reviews, loan sanctioning memos, and regulatory capital calculation.
2. **Target Lending Segments:** Large Corporate, Mid-Corporate, SME/MSME, NBFCs/HFCs, Commercial Real Estate (CRE), Project Finance & Infrastructure, and Financial Institutions.
3. **High-Level Microservices Architecture Diagram (Mermaid.js):**
   - API Gateway, Identity & Access Management (IAM), Obligor Hierarchy Service, Financial Spreading Service, Rating Calculation Engine, Model Studio & Sandbox, Collateral & Facility Engine, RAROC Pricing Engine, Bi-Temporal Event Store, Reporting & Regulatory Gateway.
4. **Regulatory Baseline:** RBI Master Directions on IRB Approach for Credit Risk, Large Exposures Framework (LEF), IRACP Norms, Stressed Asset Framework (June 7, 2019), and Basel III Capital Regulations.

---

### MODULE DOC-01: OBLIGOR, CONGLOMERATE GROUP & CORPORATE HIERARCHY ENGINE
1. **Single Obligor Entity Structure:**
   - Multi-identifier support: PAN, CIN/LLPIN, Legal Entity Identifier (LEI - mandatory for exposures > ₹50 Cr per RBI), GSTIN, Udyam Registration, CKYC.
   - Constitution types: Public Ltd, Private Ltd, LLP, Partnership, Sole Proprietorship, Trust/Society, Statutory Body, SPV.
2. **Conglomerate & Group of Connected Counterparties (GCC) Architecture (RBI LEF Compliant):**
   - Visual Tree & Directed Graph Data Model: Ultimate Parent / Conglomerate Head $\rightarrow$ Intermediate HoldCos $\rightarrow$ Operating Companies $\rightarrow$ Subsidiaries $\rightarrow$ JVs $\rightarrow$ SPVs.
   - Dual connection criteria per RBI LEF:
     - **Control Criteria:** Voting power (>50%), board control, common management, power to appoint majority directors.
     - **Economic Interdependence Criteria:** 25% or more annual gross sales/purchases, cross-guarantees, common funding sources, financial contagion risk.
3. **Group Limit & Capital Headroom Tracking:**
   - Aggregate exposure limits: 20% of Bank Tier-1 Capital for single obligor, 25% for economic group (plus 5% board-approved infrastructure leeway).
   - Real-time headroom check against group exposure ceilings before sanctioning new facilities.

---

### MODULE DOC-02: MASTER DATA ARCHITECTURE, REFERENCE LOOKUP DICTIONARY & DEPENDENCY MATRIX
Provide an exhaustive, tabular master value dictionary. For every single master dataset, document:
- **Master Name & Unique Key**
- **Permitted Domain Values / Codes**
- **Upstream / Parent Master Dependency** (e.g., Sub-Sector depends on NIC Code; Financial Template depends on Industry & Turnover tier)
- **Downstream Dependent Fields / Cascading Triggers** (e.g., Asset Classification triggers provision rate; Entity Type triggers mandatory document checklist)
- **Temporal Validity & Effective Dating** (`effective_from`, `effective_to`, status: Active/Deprecated/Draft)
- **Exact Operational & Analytical Usage** (Where and how the master affects spreading, scorecard calculation, notching, policy checks, or regulatory reports)

*Mandatory Masters to detail:*
1. **Regulatory Industry & Sector Masters:** NIC 2008 5-digit codes, RBI Priority Sector Lending (PSL) categories/sub-categories, Environmental & Social Risk Categories (ESG tiers).
2. **Entity Legal Constitution Masters:** Detailed breakdown of liability and governance implications.
3. **Internal Rating Scales:** 20-grade Master Scale (e.g., AAA down to D; numeric scale 1 to 20), Alpha grades, Standardized Investment Grade / High Yield demarcation, Default definition criteria.
4. **External Credit Rating Agency (CRA) Scales & Mapping:** CRISIL, ICRA, CARE, India Ratings, Acuité, Brickwork, Infomerics $\rightarrow$ RBI Risk Weight Mapping Tables.
5. **Chart of Accounts (COA) Masters:** Balance sheet, P&L, Cash Flow line items mapped across Ind-AS, Indian GAAP, and specialized formats.
6. **Benchmark Ratios & Industry Quartiles:** Statistical thresholds (P10/P25/P50/P75/P90) for 50+ ratios across sub-industries.
7. **Facility Type Masters:** Working Capital, Term Loans, Project Finance, Non-Fund Based (LC/BG), Derivatives.
8. **Collateral & Security Masters:** Asset types, Charge types (Exclusive, Pari-passu, Subservient), Haircuts.
9. **RBI Asset Classification Masters:** Standard (Regular, SMA-0, SMA-1, SMA-2), Sub-Standard, Doubtful (D1, D2, D3), Loss.
10. **Override & Deviation Reason Codes:** Subjective notch adjustments, Cap/Floor rules, Regulatory ceiling codes.

---

### MODULE DOC-03: FINANCIAL SPREADING, CHART OF ACCOUNTS & NORMALIZATION TEMPLATE ENGINE
1. **Multi-Template Architecture:**
   - Standard Non-Financial Corporate (Ind-AS 115/116 compliant & I-GAAP).
   - NBFC / Lending Entity Spreading Template (RBI Scale Based Regulation format; Asset Quality, ALM buckets, Capital Adequacy).
   - Commercial Real Estate Project Cashflow Template (Tower-wise cost, approvals, construction progress, receivables escrow).
   - Infrastructure / Project Finance Spreading Template (Pre-COD cash calls, DSCR with debt sculpturing, concession period).
   - MSME Simplified Spreading Template (ITR-V, GSTR-1/3B summary, bank statement metrics).
2. **Spreading Multi-Period Capabilities:**
   - Minimum 5 historic periods (Audited, Reviewed, Provisional) + Current Year + 3 to 10 Projected / CMA (Credit Monitoring Arrangement) periods.
   - Period-over-period variance tracking (Absolute & Percentage $\Delta$).
   - Dual currency handling (INR & foreign currencies with historical RBI reference rates).
3. **Financial Normalizations & Adjustments:**
   - Promoter loans treated as Quasi-Equity (subordination rules, interest-free covenants).
   - Off-balance sheet and contingent liabilities adjustments (Corporate guarantees issued, disputed tax liabilities, LC/BG devolvement history).
   - Exceptional items, revaluations, deferred tax assets (DTA), intangible assets, and goodwill amortization.
   - Formula-driven derived line items (EBITDA, Adjusted Tangible Net Worth, Total Outside Liabilities / Adjusted Net Worth, DSCR, Interest Coverage, Current Ratio, NWC).

---

### MODULE DOC-04: BORROWER RISK RATING (BRR) & MODEL STUDIO (LOW-CODE SCORECARD BUILDER & SANDBOX)
1. **Borrower Standalone Credit Profile (SACP) Model Anatomy:**
   - **Quantitative Financial Scorecard (Weight: ~50-60%):** Dynamic ratio scoring with industry-benchmarked splines, caps, and floors.
   - **Qualitative Business & Industry Scorecard (Weight: ~20-25%):** Weighted Likert-scale questions with mandatory analyst remarks and evidence uploads.
   - **Management, Conduct & Corporate Governance Scorecard (Weight: ~15-20%):** Board independence, promoter pledging, auditor qualifications, litigation, GST filing delays.
   - **Early Warning Signal (EWS) Modifiers & Conduct Indicators:** Internal account conduct (DPD in last 12 months, CC utilization > 90%, cheque bounces), external checks (CIBIL commercial score, CRIF, MCA charge creation, Wilful Defaulter search, NCLT insolvency petitions).
2. **Model Studio Low-Code / No-Code Architecture:**
   - Visual Drag-and-Drop Scorecard Builder: Hierarchy of Dimensions $\rightarrow$ Sub-Dimensions $\rightarrow$ Parameters $\rightarrow$ Benchmarks/Score Functions.
   - Expression Engine: Common Expression Language (CEL) / Python / Excel formula compatibility with syntax linting and boundary validation.
   - Weightage Allocation & Score Roll-up Engine (Linear, Non-linear, Min-Max, Worst-of, Logistic Regression scoring).
3. **Interactive Testing Sandbox & Simulation Environment:**
   - Live Sandbox: Clone an existing model version, plug in a cohort of real or synthetic obligors, run batch recalculations, and view rating distribution shifts in real-time.
   - Sensitivity & Stress Testing Simulator: "What-if" scenario engine (e.g., what happens to the rating if EBITDA drops by 15% and Working Capital days expand by 30 days?).
   - Champion-Challenger (A/B Testing) Framework: Running parallel shadow rating models alongside active production models.
   - Backtesting & Statistical Diagnostics: Calculation of Gini Coefficient, Receiver Operating Characteristic (ROC-AUC), Kolmogorov-Smirnov (KS) statistic, Population Stability Index (PSI), and Default Rate Calibration curves.

---

### MODULE DOC-05: PARENTAL SUPPORT, GOVERNMENT/GRE SUPPORT & EXTERNAL NOTCH MODIFIERS
1. **Parental Support Framework:**
   - Relationship Assessment: Strategic importance classification (Core, Strategically Important, Satisfactory, Investment/Divestment candidate).
   - Notch Uplift Matrix: Step-by-step uplift algorithm based on Parent Credit Rating, difference between Parent and Standalone Obligor rating, and degree of integration.
   - Parental Support Ceiling: Obligor rating capped at Parent rating (or 1 notch below) unless legally ring-fenced.
   - Negative Support / Contagion Notch-down: When parent is distressed and upstream cash extraction is observed.
2. **Government & Sovereign / Government-Related Entity (GRE) Support:**
   - Ownership Stake: Central Government (>51%), State Government (>51%), Joint Sector.
   - Systemic Importance & Public Mandate: Critical infrastructure, strategic sector, public policy delivery.
   - Support Mechanism Evaluation: Track record of equity infusions, budgetary subsidies, sovereign loan guarantees, regulatory forbearance.
   - GRE Notch Uplift Logic: Standalone Rating $\rightarrow$ Sovereign Support Notch Adjustment $\rightarrow$ Final Supported Rating.
3. **Hard Regulatory Ceilings & Overrides:**
   - Hard caps: Statutory auditor resignation within last 12 months (Cap at BBB); SMA-2 status in last 6 months (Cap at BB-); Wilful Defaulter / NCLT admission (Hard floor at D).
   - Discretionary Overrides: Permitted range $\pm 2$ notches; requires mandatory approval from Chief Risk Officer (CRO) / Credit Committee.

---

### MODULE DOC-06: FACILITY RISK RATING (FRR), COLLATERALS, SECURITY CHARGES & HAIRCUT ENGINE
1. **Facility Risk Rating (FRR) vs. Borrower Risk Rating (BRR):**
   - Conceptual Distinction: BRR measures Probability of Default (PD) of the obligor; FRR measures Loss Given Default (LGD) and recovery expectation of a specific credit facility.
   - Two-Dimensional Risk Matrix: Combining BRR (Grade 1-20) x FRR (Grade A-E) to produce an overarching Deal Grade / Expected Loss (EL) classification.
2. **Collateral & Security Management Architecture:**
   - Primary vs. Collateral Security: Hypothecation of stocks and book debts vs. Mortgages on fixed assets, commercial property, shares.
   - Charge Types & Ranking: First Exclusive Charge, First Pari-passu Charge (with NOC from consortium members), Second Charge, Subservient Charge, Negative Lien.
   - Valuation Governance: Gross Fair Market Value (FMV), Realizable Value (RV), Distress Sale Value (DSV), empaneled independent valuer verification date, mandatory valuation aging alerts (e.g. >3 years old triggers penalty haircut).
3. **Granular Haircut Master Engine:**
   - Haircut lookup table categorized by asset class:
     - Cash / Fixed Deposit / Sovereign G-Sec: 0% - 5%
     - Listed Equity Shares: 40% - 50%
     - Commercial Real Estate / Industrial Land: 30% - 45%
     - Residential Real Estate: 25% - 35%
     - Plant & Machinery: 50% - 65%
     - Book Debts (<90 days): 25% - 40%; Book Debts (>90 days): 80% - 100%
4. **Facility LGD Derivation Algorithm:**
   - Mathematical formulation calculating: Net Realizable Collateral Value after Haircuts and Legal Costs $\rightarrow$ Recovery percentage of facility exposure $\rightarrow$ Derived Facility LGD (e.g., 20%, 35%, 45%, 65%, 75%).
   - Mapping to FRR Grade Scale (e.g., FRR-1: LGD < 20% to FRR-5: LGD > 65%).

---

### MODULE DOC-07: ISSUER RATING VS. ISSUE RATING, GUARANTORS & CREDIT ENHANCEMENT FRAMEWORK
1. **Issuer Rating vs. Issue Rating:**
   - **Issuer Rating (Entity Level):** Reflects the overall creditworthiness and default probability of the legal entity across all senior unsecured obligations.
   - **Issue Rating (Instrument / Facility Level):** Reflects the specific default risk and expected recovery of a particular debt issue, loan tranche, or bond series.
   - Structural Subordination & Seniority: Senior Secured vs. Senior Unsecured vs. Subordinated / Mezzanine Debt.
2. **Guarantor Evaluation & Credit Substitution:**
   - Guarantor Eligibility: Corporate Parent, Group Affiliate, Commercial Bank (Counter-guarantee / SBLC), Sovereign / State Government, Multilateral Agency, Personal Guarantee of Promoter.
   - Guarantee Enforceability Standards (Indian Contract Act 1872): Absolute, Unconditional, Irrevocable, Payable on First Demand, Continuous Guarantee.
   - Credit Substitution Principle: If guarantor rating > borrower rating, and guarantee meets Basel eligibility criteria $\rightarrow$ Issue rating can substitute borrower PD with guarantor PD (with correlation adjustment).
   - Partial Guarantees & First Loss Default Guarantees (FLDG): Mathematical apportioning of covered vs. uncovered exposure.
3. **Structured Payment Mechanisms (SPM):**
   - Escrow & Trust and Retention Account (TRA) mechanisms.
   - Debt Service Reserve Account (DSRA): Cash or BG funded (1 to 2 quarters of principal + interest).
   - Structured Payment Waterfall covenants and cash-sweep triggers.

---

### MODULE DOC-08: LIMIT, EXPOSURE ARCHITECTURE, CREDIT CONVERSION FACTORS (CCF) & RAROC ENGINE
1. **Limit & Exposure Hierarchy:**
   - Five-tier hierarchy: Conglomerate Group Limit $\rightarrow$ Borrower Sanctioned Limit $\rightarrow$ Facility Limit $\rightarrow$ Sub-limits (Interchangeable / Non-interchangeable) $\rightarrow$ Account-level Disbursed Balance.
   - Fund-Based Limits (Term Loans, CC/OD, WCDL, Bill Discounting) vs. Non-Fund-Based Limits (Bank Guarantees, Letters of Credit, Trade Credits, FX Derivatives).
2. **Exposure at Default (EAD) & Credit Conversion Factors (CCF):**
   - Basel III / RBI CCF mapping:
     - Undrawn revocable credit lines: 0% - 20%
     - Undrawn irrevocable term credit lines: 50% - 75%
     - Non-Fund Based: Performance Bank Guarantees (50%), Financial Bank Guarantees (100%), Documentary LCs (20% - 50%).
   - Formulation: $\text{EAD} = \text{Drawn Balance} + (\text{Undrawn Sanctioned Commitment} \times \text{CCF})$.
3. **RAROC (Risk-Adjusted Return on Capital) Calculation Engine:**
   - Core Formula:
     $$\text{RAROC} = \frac{\text{Net Interest Margin (NIM)} + \text{Non-Interest Fee Income} - \text{Operating Costs} - \text{Expected Loss (EL)}}{\text{Economic Capital (EC)}}$$
   - Where:
     - $\text{Expected Loss (EL)} = \text{PD} \times \text{LGD} \times \text{EAD}$
     - $\text{Economic Capital (EC)} = \text{Unexpected Loss (UL)} \text{ calculated at 99.9\% confidence interval}$
   - Hurdle Rate Benchmark: Comparison against Bank Target Return on Equity (e.g., Hurdle = 15%).
   - Dynamic Risk-Based Pricing Recommender: Computes the required lending margin (spread over Repo/MCLR) to meet the hurdle rate based on BRR and FRR.

---

### MODULE DOC-09: MODEL VERSIONING, ARTIFACT PACKAGING, RELEASE CI/CD & DEPLOYMENT PIPELINE
1. **Strict Semantic Versioning Protocol:**
   - Syntax: `MAJOR.MINOR.PATCH` (e.g., `MODEL-CORP-INDAS-V2.1.0`).
   - Immutability Rule: Once a model is approved and published to Production, its configuration, formulas, parameters, and lookup weights are permanently sealed.
   - In-flight Rating Handling: Active rating runs lock into the model version active at initiation timestamp; historical audits reproduce the exact rating calculation forever.
2. **Standardized Declarative Model Artifact Bundle (Import / Export):**
   - Declarative JSON/YAML/ZIP bundle schema containing:
     - `manifest.json`: Model Metadata, sector scope, regulatory baseline, author, validity window.
     - `template_schema.json`: Financial statement COA mapping, formulas, normalization rules.
     - `scorecard_spec.json`: Quantitative parameters, splines, qualitative questions, weightages.
     - `lookups.json`: Industry quartiles, benchmark lookup tables.
     - `test_suite.json`: Golden test cases with synthetic input financials and expected final scores.
   - Cryptographic Integrity: SHA-256 digital signature validation upon export and import.
3. **Model Promotion & Release State Machine:**
   - Workflow: `Draft` $\rightarrow$ `Validation / Sandbox Testing` $\rightarrow$ `Model Risk Review` $\rightarrow$ `Dual-Key Approved (CRO + Head Model Validation)` $\rightarrow$ `Published (Production)` $\rightarrow$ `Deprecated / Archived`.

---

### MODULE DOC-10: BI-TEMPORAL DATA ARCHITECTURE, TIME-SERIES LOOKUPS & RATING MIGRATION ANALYTICS
1. **Bi-Temporal Data Architecture (Time-Travel Capabilities):**
   - Dual timestamping across all entities, financials, ratings, limits, exposures, and collateral valuations:
     - **Valid Time (Business Time):** `valid_from` to `valid_to` (the period when the fact was true in reality).
     - **System Time (Transaction Time):** `system_from` to `system_to` (the period when the record was entered and active in the database).
   - "As-of" Point-In-Time (PIT) Queries: Exact state reconstruction of an obligor, rating, or portfolio as of any past date/time (e.g., *"What was the rating, debt equity, and collateral cover of Obligor X as known to the bank on March 31, 2024 at 17:00?"*).
   - Immutable correction handling: Retrospective financial adjustments create new system-time slices without destroying previous audit records.
2. **Rating Transitions & Migration Matrix Analytics:**
   - 1-Year, 3-Year, and Cumulative Multi-Period Rating Migration Matrices (Markov transition probabilities).
   - Cohort methodology vs. Continuous Hazard Rate methodology.
   - Upgrade/Downgrade Ratio, Rating Drift, Default Realization Curves.
   - Early Warning Signals (EWS) integration triggering ad-hoc rating surveillance and automated rating migration flags.

---

### MODULE DOC-11: AUDIT TRAIL, DATA LINEAGE, FOUR-EYES GOVERNANCE & WORKFLOW STATE MACHINE
1. **Immutable Audit Trail Architecture:**
   - Append-only event-sourced logging (Field-level changes: Old Value, New Value, User ID, Timestamp, IP Address, Session ID).
   - 21 CFR Part 11 / RBI compliant electronic signature capture.
2. **Formula Calculation Explainability & Proof Engine:**
   - Complete "Step-by-Step Mathematical Derivation" generation for every finalized rating.
   - Drill-down trace: Final Rating Grade $\rightarrow$ Notch adjustments $\rightarrow$ Overrides $\rightarrow$ Quantitative vs Qualitative score split $\rightarrow$ Specific ratio values $\rightarrow$ Underlying balance sheet line items.
3. **Maker-Checker-Approver Workflow:**
   - Credit Analyst (Maker) $\rightarrow$ Senior Credit Analyst (Reviewer) $\rightarrow$ Risk Approver / Sanctioning Authority (Checker) $\rightarrow$ Committee / CRO (Special Escalation).
   - Reject with comments, Send back for clarification, and Delegation of Authority (DOA) matrix integration.

---

### MODULE DOC-12: STAKEHOLDER PORTALS, REGULATORY MIS & MANDATORY BANKING NON-FUNCTIONAL REQUIREMENTS (NFRs)
1. **Stakeholder Portals & Consoles:**
   - Relationship Manager (RM) Console: Preliminary scorecard, indicative RAROC pricing, LEF headroom check.
   - Credit Risk Underwriter Workspace: Spreading console, automated MCA/GST reconciliation, qualitative scoring, model execution.
   - Sanctioning Committee / Board Credit Committee (CAC/BCC) Executive Dashboard: One-page rating memo, risk radar chart, peer benchmarking, stress test scenarios.
   - Chief Risk Officer (CRO) Portfolio Dashboard: Rating distribution heatmaps, migration matrices, concentration risk, override tracking.
   - Statutory & Regulatory Audit Portal: CRILC mismatch reports, SMA tracking, Basel IRB RWA calculations, audit change trail logs.
2. **Mandatory Banking Non-Functional Requirements (NFRs) per RBI Regulations:**
   - **Data Residency & Localization:** 100% data residency within Indian geographic territory (Primary & Disaster Recovery sites) per RBI mandate.
   - **High Availability & Business Continuity:** 99.99% uptime; Recovery Point Objective ($\text{RPO} = 0$ for committed transactions); Recovery Time Objective ($\text{RTO} \le 15\text{ minutes}$).
   - **Security & Cryptography:** AES-256 for data at rest, TLS 1.3 for data in transit; Hardware Security Module (HSM) for key management; OWASP Top 10 compliance; CERT-In empaneled VAPT sign-off.
   - **Access Control & Identity:** RBAC and ABAC; Single Sign-On (SAML 2.0 / OIDC) with Active Directory; Multi-Factor Authentication (MFA); Privileged Access Management (PAM).
   - **Audit Storage & Non-Repudiation:** WORM (Write-Once-Read-Many) storage for audit logs; SHA-256 hash chains; PKI-based digital signatures.
   - **Throughput & Performance SLAs:** Single obligor rating calculation response $\le 500\text{ ms}$; Batch portfolio recalculation $\ge 50,000\text{ facilities/hour}$.

---

## 3. REQUIRED ARTIFACTS & FORMATTING IN YOUR OUTPUT

To ensure this Product Note serves as an authoritative build blueprint for engineering, risk, and product management teams, include:
1. **System Architecture Diagrams (Mermaid.js)**:
   - High-Level Microservices Architecture.
   - Obligor-to-Group & Facility Entity Relationship Data Model (ERD).
   - Bi-Temporal State Evolution Diagram.
   - Model Promotion & Maker-Checker State Machine.
2. **Data Dictionaries & Master Matrices**:
   - Clean, detailed markdown tables representing database schemas, master lookups, and parameter dictionaries.
3. **API & Payload Contracts**:
   - JSON schemas for Model Definition Import/Export, Financial Spreading Payload, Rating Execution Response, and RAROC Calculation.
4. **User Experience (UX) Blueprint**:
   - Wireframe layout descriptions and interaction flows for the low-code Model Studio and the Spreading Workspace.

---

## 4. GUIDING PHILOSOPHY & QUALITY RIGOR

- **Depth over Brevity:** Do not provide placeholders, summaries, or generic "etc." lists. Every master table must contain concrete Indian banking examples (e.g., exact NIC codes, exact Ind-AS balance sheet line items, real ratio formulas like DSCR and Total Debt / TNW).
- **Institutional Realism:** Write from the perspective of an architect who understands how Indian credit committees actually operate, the friction between business and risk, the scrutiny of RBI annual financial inspections (AFI), and the operational reality of managing thousands of corporate credit files.
```

---

## PROMPT ARCHITECT METADATA & EXECUTION NOTES
- **Primary Use:** Feed this master prompt into an advanced LLM (e.g., Gemini 1.5 Pro / Claude 3.5 Sonnet / GPT-4o) with extended context window to produce the complete, 60+ page institutional Product Note.
- **Execution Strategy:** Can be executed end-to-end or module-by-module (`DOC-00` to `DOC-12`) for sprint-based engineering deliverables.
