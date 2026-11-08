# 🗳️ India Lok Sabha Election 2024 Analytics Dashboard — Tableau BI

[![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)](https://www.tableau.com/)
[![Tableau Public](https://img.shields.io/badge/Tableau_Public-002D62?style=for-the-badge&logo=tableau&logoColor=white)](https://public.tableau.com/)
[![Election Commission of India](https://img.shields.io/badge/ECI-Official_Data-blue?style=for-the-badge)]()
[![LOD Expressions](https://img.shields.io/badge/Tableau-LOD_Expressions-orange?style=for-the-badge)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)

An end-to-end, enterprise-grade political analytics and business intelligence project developed in **Tableau Desktop**, visualizing and synthesizing the **2024 General Parliamentary Elections (18th Lok Sabha)** across all **543 constituencies** in **36 States and Union Territories**. The dashboard provides interactive national alliance tracking (**NDA vs. I.N.D.I.A. vs. Others**), geographic seat distribution, state demographic deep-dives, candidate victory margins, and voting channel breakdowns (**EVM vs. Postal Votes**).

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset Architecture & Schemas](#-dataset-architecture--schemas)
- [Tableau Workbook & Dashboards Breakdown](#-tableau-workbook--dashboards-breakdown)
  - [1. National Overview & Alliance Dynamics](#1--national-overview--alliance-dynamics)
  - [2. State Demographics & Geographic Mapping](#2--state-demographics--geographic-mapping)
  - [3. Constituency Deep-Dive & Candidate Diagnostics](#3--constituency-deep-dive--candidate-diagnostics)
- [Advanced Calculations & Level of Detail (LOD) Modeling](#-advanced-calculations--level-of-detail-lod-modeling)
- [Key Electoral Insights & Metrics](#-key-electoral-insights--metrics)
- [Prerequisites & Getting Started](#-prerequisites--getting-started)
- [Tech Stack & Tools](#-tech-stack--tools)
- [Future Enhancements](#-future-enhancements)

---

## 🔍 Project Overview

The 2024 Indian General Election was the largest democratic exercise in human history, involving over **64.5 Crore votes cast** across 543 Parliamentary Constituencies. This project transforms raw election result tables into an interactive, multi-layered visual analytics platform designed to answer critical strategic questions:

- **Alliance Performance**: Did the National Democratic Alliance (NDA) or the Indian National Developmental Inclusive Alliance (I.N.D.I.A.) secure the 272-seat majority threshold?
- **Party Dispersal**: How did major national parties (BJP, INC) perform compared to regional powerhouses (SP, AITC, DMK, TDP, JD(U))?
- **Vote Channel Diagnostics**: What was the split between Electronic Voting Machine (EVM) votes and Postal ballots across candidates?
- **Victory Margins & Competitiveness**: Where were the landslides and razor-thin photo-finishes won?
- **State-by-State Dominance**: Which coalition captured the majority of seats in pivotal battleground states?

---

## 🗄️ Dataset Architecture & Schemas

The project ingests and models five normalized relational datasets stored in `Dataset/`:

| Dataset File | Rows | Primary Key / Grain | Description |
|:---|:---:|:---|:---|
| **`constituencywise_details.csv`** | **8,903** | `Constituency ID` + `Candidate` | Granular candidate-level records including EVM votes, postal votes, total votes, and vote share percentage |
| **`constituencywise_results.csv`** | **544** | `Constituency ID` (543 Seats) | Constituency-level winning candidate, margin, state association, and winning party ID |
| **`partywise_results.csv`** | **43** | `Party ID` | Summary catalog of 42 political parties plus independents that secured parliamentary seats |
| **`statewise_results.csv`** | **544** | `Constituency` + `State ID` | Detailed seat tallies, leading vs. trailing candidate pairs, victory margins, and seat status |
| **`states.csv`** | **37** | `State ID` | Master geographic dimension table mapping 28 States and 8 Union Territories |

### Data Attributes Breakdown:
- **`constituencywise_details.csv`**: `S.N.`, `Candidate`, `Party`, `EVM Votes`, `Postal Votes`, `Total Votes`, `% of Votes`, `Constituency ID`
- **`constituencywise_results.csv`**: `S.No`, `Parliament Constituency`, `Constituency Name`, `State`, `Winning Candidate`, `Total Votes`, `Margin`, `Constituency ID`, `Party ID`
- **`partywise_results.csv`**: `Party`, `Won`, `Party ID`
- **`states.csv`**: `State ID`, `State`
- **`statewise_results.csv`**: `Constituency`, `Const. No.`, `Parliament Constituency`, `Leading Candidate`, `Trailing Candidate`, `Margin`, `Status`, `State ID`

---

## 📊 Tableau Workbook & Dashboards Breakdown

The packaged Tableau workbook (`Working File/India Loksabha Election 2024 - Final.twbx`) contains three dedicated executive dashboards engineered for exploratory and diagnostic reporting:

```
┌────────────────────────────────────────────────────────────────────────┐
│               INDIA LOK SABHA ELECTION 2024 TABLEAU BI                 │
├─────────────────────┬───────────────────────────┬──────────────────────┤
│ 1. NATIONAL         │ 2. STATE DEMOGRAPHICS     │ 3. CONSTITUENCY      │
│    OVERVIEW         │    & GEOGRAPHIC MAP       │    DEEP-DIVE         │
│ • NDA Seats & %     │ • Winning Candidates/     │ • 6 Executive KPIs   │
│ • I.N.D.I.A Seats   │   Party by State          │ • Candidate Card     │
│ • Party Bar Chart   │ • Constituency Fill Map   │ • Alliance Split     │
│ • Alliance Matrices │ • State Coalition Balance │ • Dynamic Top N      │
│ • Leadership Focus  │ • Geographic Heatmap      │ • Measure Selector   │
└─────────────────────┴───────────────────────────┴──────────────────────┘
```

### 1. 🇮🇳 National Overview & Alliance Dynamics
*Dashboard: `INDIA LOKSABHA ELECTION 2024 - Overview`*

- **Executive KPI Callouts**:
  - **Total NDA Seats Won**: **293 Seats** (`53.96%` of parliament)
  - **Total I.N.D.I.A. Seats Won**: **234 Seats** (`43.09%` of parliament)
  - **Others / Unaligned Seats**: **16 Seats** (`2.95%` of parliament)
- **Party-Wise Seat Distribution (Horizontal Bar Chart)**:
  - Cleanly ranks political parties by parliamentary seats won, featuring distinct thematic color coding for BJP (Saffron), INC (Cyan/Blue), SP (Red), AITC (Green), DMK (Orange), and regional parties.
- **Alliance Breakdown Panels**:
  - Comprehensive listing of parties belonging to the **NDA Coalition** (BJP, TDP, JD(U), SHS, LJPRV, JnP, RLD, JD(S), AGP, HAMS, SKM, AJSUP, ADAL).
  - Comprehensive listing of parties belonging to the **I.N.D.I.A. Bloc** (INC, SP, AITC, DMK, SHSUBT, NCPSP, RJD, CPI(M), AAP, JMM, IUML, CPI(ML)(L), CPI, VCK, MDMK, BAP, KEC, JKN, RLTP, RSP).
- **Leadership Visual Branding**:
  - Dedicated visual anchors showcasing key political figures (Narendra Modi / BJP and Rahul Gandhi / INC).

### 2. 🗺️ State Demographics & Geographic Mapping
*Dashboard: `INDIA LOKSABHA ELECTION 2024 - STATE DEMOGRAPHICS`*

- **Geographic Choropleth Mapping**: Interactive constituency-level and state-level boundary map of India displaying political party spatial density.
- **State Majority Indicators**: Level-of-Detail calculated fields dynamically determining whether a state leaning majority favoured NDA or I.N.D.I.A.
- **Winning Candidates by State**: Interactive cross-tabular explorer allowing users to click on any state (e.g., Uttar Pradesh, Maharashtra, West Bengal, Tamil Nadu) to isolate winners, vote counts, and runner-ups.

### 3. 🔍 Constituency Deep-Dive & Candidate Diagnostics
*Dashboard: `INDIA LOKSABHA ELECTION 2024 - STATES DEMOGRAPHICS (2)`*

- **Executive Metric Ribbon**:
  - **Total Parliamentary Seats**: `543`
  - **Total Contesting Candidates**: `8,101`
  - **Total Participating Parties**: `746`
  - **Total Votes Cast**: `645,363,445` (64.54 Crore)
  - **Total EVM Votes**: `641,618,937` (99.42%)
  - **Total Postal Ballots**: `3,744,508` (0.58%)
- **Winning Candidate Profile Card**:
  - Dynamic KPI container detailing the selected constituency's Winner, Party Name, Total Votes Secured, Victory Margin, and Vote Share Percentage.
- **Alliance & Party Diagnostics**:
  - Seats by Alliance donut and bar visualizations.
  - Granular comparative listing of all contesting candidates in that constituency sorted by rank.
- **Interactive Tableau Controls**:
  - **State Filter**: Multi-select dropdown filtering all visuals across India's 36 administrative divisions.
  - **Constituency Filter**: Single-select dropdown focusing on individual seats.
  - **Dynamic Measure Selector**: Parameter enabling instant switching between `Total Votes`, `EVM Votes`, and `Postal Votes`.
  - **Top N Parameter**: Dynamic parameter controlling candidate and party ranking limits.

---

## ⚙️ Advanced Calculations & Level of Detail (LOD) Modeling

The Tableau model leverages complex **Level of Detail (LOD) expressions**, multi-condition boolean logic, and dynamic parameters:

### 1. Alliance Categorization (`[Party Allianz]`):
Categorizes 40+ national and regional parties into political coalitions:
```tableau
IF [Party (partywise_results.csv)] IN (
    "Bharatiya Janata Party - BJP", "Telugu Desam - TDP", 
    "Janata Dal (United) - JD(U)", "Shiv Sena - SHS", 
    "Lok Janshakti Party(Ram Vilas) - LJPRV", "Janasena Party - JnP", 
    "Rashtriya Lok Dal - RLD", "Janata Dal (Secular) - JD(S)",
    "Asom Gana Parishad - AGP", "Hindustani Awam Morcha (Secular) - HAMS", 
    "Sikkim Krantikari Morcha - SKM", "AJSU Party - AJSUP", "Apna Dal (Soneylal) - ADAL"
) THEN "NDA"
ELSEIF [Party (partywise_results.csv)] IN (
    "Indian National Congress - INC", "Samajwadi Party - SP", 
    "All India Trinamool Congress - AITC", "Dravida Munnetra Kazhagam - DMK", 
    "Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT", 
    "Nationalist Congress Party Sharadchandra Pawar - NCPSP", 
    "Rashtriya Janata Dal - RJD", "Communist Party of India (Marxist) - CPI(M)", 
    "Aam Aadmi Party - AAAP", "Jharkhand Mukti Morcha - JMM", 
    "Indian Union Muslim League - IUML", "Communist Party of India - CPI", 
    "Viduthalai Chiruthaigal Katchi - VCK", "Jammu & Kashmir National Conference - JKN"
) THEN "I.N.D.I.A."
ELSE "OTHER"
END
```

### 2. State-Level Majority Determination (LOD Expression):
```tableau
IF { FIXED [State] : COUNT(IF [Party Allianz] = "NDA" THEN [Winning Candidate] END) } >=
   { FIXED [State] : COUNT(IF [Party Allianz] = "I.N.D.I.A." THEN [Winning Candidate] END) }
THEN "NDA"
ELSE "INDIA"
END
```

### 3. Dynamic Measure Parameter Control:
```tableau
CASE [Parameters].[Select Measure]
  WHEN "Total Votes"  THEN [Total Votes]
  WHEN "EVM Votes"    THEN [EVM Votes]
  WHEN "Postal Votes" THEN [Postal Votes]
END
```

### 4. Alliance Seat Shares & Percentages:
```tableau
// % of NDA Seats
SUM(IF [Party Allianz] = "NDA" THEN [Won] END) / SUM([Won])

// % of I.N.D.I.A. Seats
SUM(IF [Party Allianz] = "I.N.D.I.A." THEN [Won] END) / SUM([Won])
```

---

## 📈 Key Electoral Insights & Metrics

| Dimension / Metric | 🟠 NDA Coalition | 🔵 I.N.D.I.A. Coalition | ⚪ Others & Independents |
|:---|:---:|:---:|:---:|
| **Total Seats Won** | **293** (54.0%) | **234** (43.1%) | **16** (2.9%) |
| **Lead Party** | BJP (240 Seats) | INC (99 Seats) | YSRCP (4 Seats), IND (7) |
| **Top Partner 1** | TDP (16 Seats) | SP (37 Seats) | ASPKR (1 Seat) |
| **Top Partner 2** | JD(U) (12 Seats) | AITC (29 Seats) | AIMIM (1 Seat) |
| **Total Parties in Alliance** | 13 Parties | 20+ Parties | 10+ Parties |
| **Majority Threshold (272)** | **Achieved (+21)** | Opposition | Neutral |

### Key Takeaways:
- **Coalition Era Returns**: The BJP emerged as the single largest party with 240 seats, forming a parliamentary majority through key NDA coalition partners TDP (Andhra Pradesh) and JD(U) (Bihar).
- **Strong Opposition Resurgence**: The I.N.D.I.A. alliance secured 234 seats, anchored by the Indian National Congress (99 seats) and major regional breakthroughs by Samajwadi Party in Uttar Pradesh (37 seats) and All India Trinamool Congress in West Bengal (29 seats).
- **Massive Electoral Turnout**: Over 64.53 crore voters participated, with EVM votes constituting 99.42% and Postal votes making up 0.58%.

---

## 🚀 Prerequisites & Getting Started

### Prerequisites:
- [Tableau Desktop](https://www.tableau.com/products/desktop) (v2022.1 or newer recommended) or [Tableau Public](https://public.tableau.com/) (Free)
- Any CSV / Spreadsheet viewer (Microsoft Excel, LibreOffice Calc)

### How to Open and Explore the Project:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/bhattchintan8540-cmd/Data-Analytics-with-Tableau.git
   ```

2. **Navigate to the repository folder**:
   ```bash
   cd Data-Analytics-with-Tableau
   ```

3. **Open the Packaged Tableau Workbook**:
   - Navigate to `Working File/`
   - Double-click **`India Loksabha Election 2024 - Final.twbx`**.
   - Tableau will automatically extract the embedded `.hyper` database and load all three interactive dashboards.

4. **Interact with the Visuals**:
   - Switch between the three dashboard tabs at the bottom (`Overview`, `STATE DEMOGRAPHICS`, and `STATES DEMOGRAPHICS (2)`).
   - Use the interactive State, Alliance, and Constituency slicers to filter results dynamically.
   - Adjust the **Select Measure** parameter to inspect candidate standings by EVM vs. Postal votes.

---

## 🛠️ Tech Stack & Tools

- **Business Intelligence**: Tableau Desktop, Tableau Public
- **Data Engine**: Tableau Hyper Extract (`.hyper`)
- **Calculations & Analytics**: Tableau Level of Detail (LOD) Expressions (`FIXED`), Dynamic Parameters, Custom Table Calculations (`RANK_UNIQUE`, `INDEX`)
- **Data Modeling**: Relational Schemas across 5 CSV Data Sources
- **Visual Design**: Choropleth Filled Maps, Horizontal Bar Charts, Donut Charts, Dynamic Card Containers, KPI Metrics

---

## 🔮 Future Enhancements

- [ ] **Historical Swing Analysis**: Integrate 2019 Lok Sabha results to compute swing percentages and seat-gain/seat-loss metrics.
- [ ] **Demographic & Voter Turnout Correlation**: Merge voter turnout percentages with gender and constituency urbanization demographics.
- [ ] **Tableau Storyboard**: Build a step-by-step interactive Tableau Story guiding users through key election night turning points.

---
*⭐ If you find this political intelligence dashboard informative, consider giving the repository a star!*
