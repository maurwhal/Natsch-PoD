# Natsch PoD Calculator — *Marvelous Maura Model* (Strict)

Single‑page web app that reproduces **Andreas Natsch**’s quantitative **Point‑of‑Departure (PoD)** approach (predicted **pEC3/EC3**) using **exactly** the five equations from his calculator (EQ1, EQ4, EQ5, EQ6, EQ7). This build purposely avoids extra decision logic — it mirrors the spreadsheets and papers.

> **Scope:** Implements the equations and normalizations as described in Natsch & Gerberick (ALTEX 2022) and follow‑ups (2023). Vapor pressure handling follows the papers’ method. This tool does not add extra expert rules.

## What’s implemented

- **Equations**: **EQ1, EQ4, EQ5, EQ6, EQ7**. Results shown as **pEC3** and **EC3 (% w/w)**. A “recommended” row is highlighted based on data availability (EQ5 → EQ1 → EQ4 → EQ7 → EQ6), matching common usage in the Excel templates.
- **Inputs & units**
  - **CAS / Name / MW (g/mol)** — CAS lookup button uses PubChem to prefill *Name* and *MW* (optional; you can type manually).
  - **Vapor pressure (VP)** — enter **Pa** *or* **mmHg** (app keeps them synced using 1 mmHg = 133.322 Pa).  
    Normalization used in equations: **LogVP_norm = log10(VP in Pa) − 1**, with negatives clamped to 0.
  - **kDPRA** — enter **log k_max** (s⁻¹·M⁻¹). The model uses **log k_max_norm = log k_max + 3.5** (floored at 0).
  - **KeratinoSens™** — **EC1.5, EC3 (optional), IC50**. You may enter values in **µM** or **µg/mL**; the app converts **µg/mL → µM** using MW.  
    Normalization: `X_norm = −log10(X_µM) + log10(4000)`; if no induction/cytotox at the guideline max, the sheet’s default **4000 µM** is used before normalization.
  - **h‑CLAT** — **EC150 (CD86), EC200 (CD54)** → app takes **MIT = min(EC150, EC200)**; **CV75** accepted in **µM** or **µg/mL** (converted using MW).  
    Normalization: `MIT_norm = −log10(MIT_µM) + log10(25 000)`, `CV75_norm = −log10(CV75_µM) + log10(25 000)`.  
    When blank/negative at the guideline max, templates use **MIT = 25 000 µM** and **CV75 = 5 000 µg/mL** (converted to µM) before normalization.
- **PDF extraction (optional)** — Upload a PDF report (or paste its text) and the app will attempt to auto‑pull common assay fields (EC1.5/EC3/IC50/EC150/EC200/CV75/log k_max). This runs **entirely in your browser**; files are not uploaded or saved.
- **Data source finder** — Given a CAS, quick links to EPA CompTox Dashboard, PubChem, OECD eChemPortal, ECHA (site search), Google Scholar, and PubMed.

## Step‑by‑step (how to use)

1. **Open the app** (`index.html`).  
2. Enter **CAS** (optional) and click **Lookup** to prefill *Name* and *MW*; or type them manually.
3. Enter **VP** in **Pa** or **mmHg** (or click **EPA Dashboard** to open the CAS page and copy mmHg).  
   Confirm **LogVP_norm** is computed.
4. Enter **kDPRA**, **KeratinoSens™**, and **h‑CLAT** values. If you only have **µg/mL**, select the unit — the app converts to µM using the MW you provided.
5. Click **Calculate**. The app outputs **pEC3** and **EC3 (%)** for all applicable equations and highlights the preferred one based on available data.
6. (Optional) Use **PDF extract**: upload a report or paste text → click **Parse** → **Apply found values**.
7. (Optional) Use **Data source finder** to open official portals for the CAS.

## Reproducibility notes

- **No additional decision flags** are applied (e.g., precipitation/insolubility/borderline). The app is intentionally “calculator‑only.”
- **Defaults** match the spreadsheets:  
  - KS negatives → **4000 µM** prior to normalization.  
  - h‑CLAT negatives → **MIT = 25 000 µM**, **CV75 = 5 000 µg/mL** (converted to µM) prior to normalization.  
  - kDPRA **log k_max_norm = log k_max + 3.5**; values below 0 are treated as 0.  
  - **VP normalization** uses **Pa**; **LogVP_norm = log10(Pa) − 1**; negatives → 0.
- **pEC3/EC3 relationship** (per papers): `pEC3 = log10(MW / EC3)` ⇒ `EC3 = MW / 10^{pEC3}`.

## GitHub Pages (publish this as a website)

1. Create a public repo (e.g., `OECD497-PoD`).
2. Upload **`index.html`** (this app) and **`README.md`** (this file) to the repo root.
3. Go to **Settings → Pages** → **Source: Deploy from a branch** → pick your default branch and **/ (root)** → **Save**.
4. Visit `https://<your-username>.github.io/<your-repo>/`.

## Privacy

This is a static, client‑side app. Inputs and PDFs are processed **in your browser** and are **not** uploaded or stored.

## References

- Natsch A., Gerberick G.F. (2022). *Integrated Skin Sensitization Assessment (I): Establishing a quantitative PoD predictor from in vitro assays and vapor pressure.* ALTEX 39(4), 636–646.  
- Natsch A., Gerberick G.F. (2022). *Integrated Skin Sensitization Assessment (II): How to combine key events and reactivity with defined approaches.* ALTEX 39(4), 647–655.  
- Natsch A., Gerberick G.F. (2023). *Integrated Skin Sensitization Assessment (III): Incorporation of human data and refined modeling.* ALTEX 40(4), 571–583.  

— *Generated on 2025-09-02 for Maura’s Marvelous Model.*
