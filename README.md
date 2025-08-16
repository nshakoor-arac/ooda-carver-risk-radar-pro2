# ooda-carver-risk-radar-pro2
Dashboard for risk analysis combining the OODA workflow, CARVER scoring, and a scale aware Risk Matrix. Import CSV or JSON, edit assets, see radar and barometer visuals, auto compute Likelihood, Impact, and Risk Score, then export to PDF, JSON, CSV, or Excel. Human in the loop.Here is a complete **README.md** you can drop into your repo.

---

# OODA CARVER Risk Radar - Pro 2

A single file, offline capable dashboard for risk analysis that blends **CARVER** scoring with an **OODA** workflow and a **scale aware Risk Matrix**. Built around the **Quanta Analytica MNS** integrated risk framework for humanitarian, geopolitical, socioeconomic, and stability operations use cases.

> More projects and links: **[https://linktr.ee/mnshakoor](https://linktr.ee/mnshakoor)**

---

## Table of contents

* [Overview](#overview)
* [Key features](#key-features)
* [How it works](#how-it-works)
* [Scoring scales](#scoring-scales)
* [Data contract](#data-contract)
* [Use cases](#use-cases)
* [How to use the app](#how-to-use-the-app)
* [Analyst guidance - human in the loop](#analyst-guidance---human-in-the-loop)
* [Quality checks](#quality-checks)
* [Security and privacy](#security-and-privacy)
* [Deploy on GitHub Pages](#deploy-on-github-pages)
* [Contributing](#contributing)
* [License](#license)

---

## Overview

This app helps analysts rapidly turn contextual information into a structured portfolio of **Assets** that include **Targets**, **Threats**, and **Vulnerabilities**. Each asset is scored using **CARVER** and rolled into **Likelihood**, **Impact**, and **Risk Score** with visualizations that support briefings and decision making. The design goal is fast situational sensemaking with transparent math and editable assumptions.

The framework integrates:

* **CARVER** for structured scoring

  * C Criticality
  * A Accessibility
  * R Recuperability
  * V Vulnerability
  * E Effect
  * Rz Recognizability
* **Risk Matrix** to combine Likelihood and Impact
* **OODA** as a workflow pattern

  * Observe input data
  * Orient with context and constraints
  * Decide on priorities and mitigations
  * Act to reduce risk and monitor change
* Alignment with **ISO 31000 style** risk management steps and an MNS consultative cycle

---

## Key features

* Import **CSV or JSON**. The app auto detects whether your data uses a **1 to 5** or **1 to 10** scale.
* **Nested translucent radar charts** per asset to compare CARVER dimensions.
* **Barometer style KPIs** for Total CARVER, P(a), Likelihood, Impact, and Risk Score with color bands.
* **Risk Matrix** with color coded cells. Popups use solid backgrounds that match rating colors for readability.
* **Editor tab** to adjust CARVER values with instant recompute of all visuals and metrics.
* **Add Asset** tab to append new items with auto calculations.
* **Schema panel** with a downloadable JSON schema and CSV template.
* Theme selection with **Dark**, **Light**, and **Auto**.
* Export to **PDF**, **JSON**, **CSV**, and **Excel**.
* Works offline in any modern browser. No server required.

---

## How it works

**Step 1. Score with CARVER**
You assign numeric values for C, A, R, V, E, Rz on the chosen scale.

**Step 2. Derive risk metrics**

* Likelihood L = (A + V + Rz) / 3
* Impact I = (C + E + R) / 3
* Total CARVER = C + A + R + V + E + Rz
* P(a) = Total CARVER divided by 6 times Scale
* Risk Score = L times I

**Step 3. Risk Matrix and visuals**

* Gauge bands show severity from green to red based on the selected scale.
* The Risk Matrix shades cells by percentile so thresholds are consistent whether you use 1 to 5 or 1 to 10.
* The Radar chart compares dimension shape across assets.

---

## Scoring scales

The app supports **1 to 5** and **1 to 10**.

* **Auto detection on import**
  If any CARVER value is greater than 5 the app switches to 1 to 10. Otherwise it uses 1 to 5.
* **Manual override**
  You can switch the scale in the control bar. All visuals and thresholds update immediately.

**Scale aware thresholds**
Risk ratings use percent of maximum, not fixed numbers. Example thresholds:
Very Low under 20 percent, Low 20 to under 40, Medium 40 to under 60, High 60 to under 80, Critical 80 to 100.
This keeps ratings consistent across 1 to 5 and 1 to 10.

---

## Data contract

Your data must match the schema used by the app. The app includes a Schema button that shows and downloads these artifacts.

**Minimal JSON shape**

```json
{
  "assets": [
    {
      "name": "string",
      "type": "string",
      "country": "string",
      "location": "string",
      "C": 0,
      "A": 0,
      "R": 0,
      "V": 0,
      "E": 0,
      "Rz": 0,
      "notes": "string",
      "L": 0,
      "I": 0,
      "totalCarver": 0,
      "pa": 0,
      "score": 0
    }
  ]
}
```

**CSV header example**

```csv
name,type,country,location,C,A,R,V,E,Rz,notes
```

* You may omit L, I, totalCarver, pa, score. The app computes them.
* Flexible header aliases are supported for import. For example criticality maps to C and vulnerability maps to V.

---

## Use cases

* **Humanitarian operations**
  Target - Regional Hospital. Threat - Militia checkpoint network. Vulnerability - Single access road and fuel scarcity.
  Purpose: prioritize protection, convoy routing, and generator support.

* **Geopolitical and socioeconomic stress**
  Target - Cross border market. Threat - Currency shock and customs clampdown. Vulnerability - Permit regime volatility.
  Purpose: anticipate price spikes, crowd risk, and supply chain impacts.

* **Stability operations and conflict prevention**
  Target - Substation and water plant. Threat - Rocket capable NSAG. Vulnerability - Power instability and sparse patrol coverage.
  Purpose: rank hardening measures, reroute services, inform ceasefire monitors.

---

## How to use the app

1. **Open the HTML**
   Clone the repo and open `index.html` or the provided single page HTML in your browser.

2. **Import data**
   Click Import and select your CSV or JSON. The scale is auto detected.

3. **Filter and explore**
   Use the asset filter. Selecting All displays averages across the set.

4. **Read the KPIs**
   Barometers show Total CARVER, P(a), Likelihood, Impact, and Risk Score with banded context.

5. **Review radar and matrix**
   Radar overlays the CARVER shape. The Risk Matrix shows Likelihood by Impact with readable color coded popups.

6. **Edit and add**
   In the Editor tab change CARVER values. All metrics and visuals update instantly. Use Add Asset to append new entries.

7. **Export**
   Export to PDF for briefings or JSON, CSV, Excel for analysis pipelines.

8. **Schema and templates**
   Use the Schema button to view or download the JSON schema and CSV template that import seamlessly.

9. **Theme**
   Switch between Dark, Light, or Auto to fit your briefing environment.

---

## Analyst guidance - human in the loop

This tool accelerates triage and visualization, but it does not replace judgment. Keep a **human in the loop**.

* Validate sources and triangulate claims.
* Make conservative estimates when data is thin and record assumptions in notes.
* Revisit scores after new reporting, route changes, or posture shifts.
* Use the tool to support decisions, not to automate them. Your analytic mind is the final say.

---

## Quality checks

* Ensure CARVER values stay within the chosen scale.
* Watch for stale context. If an actor posture changes, update A, V, and Rz.
* If an asset has strong redundancy, verify that V and R reflect that.
* Use the same scale across a portfolio unless you are deliberately comparing cohorts.

---

## Security and privacy

* Everything runs client side. No data leaves the browser unless you export it.
* Treat datasets as sensitive. Do not commit production data to a public repo.
* If you publish a live demo, sanitize or simulate data.

---

## Deploy on GitHub Pages

1. Commit the app files to your repo root.
2. In GitHub go to Settings then Pages.
3. Choose **Deploy from a branch**, select `main` or `gh-pages`, and the root folder.
4. Save. GitHub Pages will publish your app at the provided URL.

---

## Contributing

Issues and pull requests are welcome. Please include:

* A clear description of the change.
* Screenshots or short clips when altering visuals.
* Test data that demonstrates the fix or feature.

---

## License

MIT.

---

**Author links and projects**
Linktree: **[https://linktr.ee/mnshakoor](https://linktr.ee/mnshakoor)**
