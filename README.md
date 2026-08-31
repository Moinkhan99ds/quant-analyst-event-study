Quantitative Analyst Event Study

Overview

This project analyzes how corporate announcements affect stock prices and trading volume across five BSE-listed companies: RELIANCE, HDFCBANK, NYKAA, HAL, and RVNL.

The analysis covers corporate announcements from August 2023 to August 2026 and focuses on event alignment, announcement classification, short- and long-term price reactions, trading-volume impact, and post-earnings announcement drift (PEAD).

The analysis was performed using Python with a rule-based and reproducible methodology.

Objectives

- Clean and validate corporate announcement and market data.
- Align announcements with the first complete tradable one-minute market bar.
- Group related announcements into independent events.
- Classify announcements into meaningful subject groups.
- Measure price and trading-volume reactions at multiple horizons.
- Compare announcement impact across subjects and stocks.
- Investigate price-conditioned post-earnings announcement drift.
- Report statistical evidence, limitations, and practical findings.

Dataset

The analysis uses the following provided files:

- "corporate_announcements.csv"
- "RELIANCE.csv"
- "HDFCBANK.csv"
- "NYKAA.csv"
- "HAL.csv"
- "RVNL.csv"

The raw datasets are not included in this repository.

Place the provided datasets in the data directory before running the analysis.

Methodology

1. Data Preparation

Announcement timestamps were parsed using "DissemDT" when valid, with "DT_TM" used as the fallback.

Each announcement was aligned with the first complete one-minute market bar beginning at or after dissemination. This avoids using a bar that partially occurred before the announcement.

The analysis also checked for invalid timestamps, missing values, duplicate records, invalid OHLC values, zero-volume observations, and incomplete event windows.

2. Event Clustering

Announcements referring to the same underlying corporate event were grouped using a consistent rule-based clustering approach.

This reduced 2,528 announcement records to 2,396 independent events.

3. Announcement Classification

Announcements were grouped into seven subject categories:

- Press / Public Updates
- Regulatory / Compliance
- Investor Communication
- Board / Management
- Corporate Actions
- Orders / Business
- Financial Results

4. Price and Volume Analysis

Price reactions were measured over:

- 5 minutes
- 30 minutes
- 60 minutes
- Same-day close
- D+1
- D+5
- D+10
- D+20

Trading-volume impact and price volatility were also evaluated.

A strong-impact event was identified using the predefined price- and volume-impact criteria applied consistently across the dataset.

5. Post-Earnings Announcement Drift

Independent financial-result announcements were identified and analyzed separately.

The PEAD analysis contains 52 independent earnings events. D0 represents the first trading session in which the earnings information could be acted upon.

Returns were evaluated through D+1, D+3, D+5, D+10, and D+20.

Because analyst expectations and earnings-surprise data were not provided, the analysis is described as price-conditioned post-earnings announcement drift, rather than surprise-based PEAD.

Key Findings

- 2,528 announcement records were analyzed, representing 2,396 independent events after clustering.
- 597 events (23.615%) were classified as strong-impact events.
- Longer-horizon returns generally showed larger dispersion than short-horizon returns.
- Orders / Business announcements showed the highest mean same-day close return among the subject groups.
- Financial Results produced substantial trading-volume activity but did not by itself establish statistically significant positive price drift.
- Stock-level reactions were heterogeneous, with stronger longer-term effects observed for some stocks than others.
- The pooled PEAD analysis showed increasing mean returns at longer horizons, reaching 2.675% at D+20, but the result was not statistically significant at the conventional 5% level (p = 0.057).
- PEAD continuation increased to 74.0% at D+10, but declined to 63.3% at D+20, indicating that persistence was not uniformly sustained.

These findings describe associations within the supplied dataset and should not be interpreted as causal effects or trading recommendations.

Repository Structure

quant-analyst-event-study/
│
├── README.md
├── requirements.txt
│
├── notebooks/
│   └── analysis.ipynb
│
├── outputs/
│   ├── event_level_results.csv
│   ├── subject_summary.csv
│   ├── pead_summary.csv
│   └── figures/
│       ├── figure1.png
│       ├── figure2.png
│       ├── figure3.png
│       ├── figure4.png
│       ├── figure5.png
│       └── ...
│
└── report/
    └── report.pdf

Reproducibility

Install the required Python packages:

pip install -r requirements.txt

Place the original supplied datasets in the documented data directory and run the analysis notebook from beginning to end.
The analysis generates the event-level results, subject-level summary, PEAD summary, and figures used in the report.
 
## Outputs
 
### `event_level_results.csv`
 
Contains event-level announcement information and calculated price, volume, volatility, and impact metrics.
 
### `subject_summary.csv`
 
Contains aggregated impact statistics for each announcement subject group.
 
### `pead_summary.csv`
 
Contains pooled post-earnings drift results across D0, D+1, D+3, D+5, D+10, and D+20.
 
## Limitations
 
 
- The analysis covers only five supplied stocks and should not be generalized to the wider market.
 
- Corporate announcements can overlap or refer to the same underlying event; clustering reduces but may not completely eliminate this issue.
 
- Extreme observations can influence mean returns and volume measures.
 
- No analyst-expectation or earnings-surprise data was supplied, so the PEAD analysis is price-conditioned rather than surprise-based.
 
- The analysis identifies associations and does not establish causality.
 
- Market conditions and other simultaneous information may contribute to observed price movements.
 

 
## AI Disclosure
 
AI-assisted tools were used to support parts of the analysis workflow, including code assistance, report drafting, and explanation of analytical procedures. The final methodology, calculations, results, and interpretations were reviewed against the supplied dataset and assessment requirements.
