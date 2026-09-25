# NYC Rental Market — Analysis for Renters & Owners

A real-estate client wanted the New York rental market read for **two audiences** — renters and property
owners. I analysed **17,614 listings** in Python to answer both, and the two owner questions turned out to
have *different* answers.

**▶ Live interactive dashboard:** https://nonsogithub41.github.io/nyc-rental-analysis/

---

## The headline

**Owners price on one lever and get booked on another.** A model of *price* leans almost entirely on
**location and room type**. A separate model of *occupancy* leans on **availability and reviews** — and
price barely registers: price and occupancy correlate just **−0.03**. Cutting your nightly rate is not
how a listing wins bookings.

## Key findings

| Area | Finding | So what |
|---|---|---|
| **Renters — room type** | A private room runs **~$70** vs **~$151** for an entire home | Room type is the fastest saving |
| **Renters — geography** | Prime Manhattan tops **$200**; outer-borough value neighbourhoods sit near **$60** | Value is one borough out |
| **Owners — price** | Location + room type carry **~58%** of the price model (R² 0.42) | Price is set structurally — get those right first |
| **Owners — bookings** | Availability drives **60%** of the occupancy model (R² 0.59); price just 2% | Availability & reviews fill a calendar, not discounts |
| **Price ↔ bookings** | Correlation **−0.03** | Discounting to drive occupancy is the wrong lever |
| **The opportunity** | A **~31% "dormant"** segment sits always-available, barely booked | A visibility & reviews problem, not a pricing one |

## Research questions

1. **What sets a listing's price?** (renters & owners — the pricing question)
2. **What gets a listing booked?** (owners — the demand question)
3. **Are they the same lever?** — can an owner book more simply by pricing lower?

## Data source & cleaning

- **Source:** New York City rental listings (17,614 rows), open-source, plus a NYC neighbourhoods GeoJSON
  for the geospatial join. Continuous variables: price, days booked, availability, reviews. Categorical:
  room type, neighbourhood, borough.
- **Cleaning:** dropped the index column; filtered prices to a valid $1–999 range (17,529 rows retained);
  mapped every listing to one of the five boroughs; standardised features before clustering and removed
  identifier columns so cluster distance reflects behaviour, not an ID's scale.

## What's here

- `nyc_rental_analysis.ipynb` — full reproducible analysis (pandas, scikit-learn), with outputs
- `new_york_rentals.csv` — the 17,614-listing dataset
- `index.html` — the interactive dashboard (also hosted via GitHub Pages, link above)

## Method

- **Tools:** Python (pandas, scikit-learn), Tableau
- **Two separate models**, because they answer different questions: a random forest for **price**
  (test R² ≈ 0.42) and one for **occupancy** (R² ≈ 0.59); driver weights are feature importances.
- **Segments** are K-means on **standardised** behavioural features with **identifier columns removed**,
  so distance reflects behaviour rather than an arbitrary ID scale.
- Run it yourself: `pip install pandas scikit-learn` then open the notebook — every figure regenerates
  from the CSV.

> **Note on rigour.** An earlier pass of this case study modelled `reviews_per_month` instead of price,
> ran K-means on unscaled features that still included the listing `id` (so the clusters split on ID
> magnitude, not behaviour), and concluded the dataset was too small. This version corrects all three:
> price is the target, features are standardised with identifiers removed, and 17,614 rows is ample.

---

Built by **Nonso Ezeoma** · Automation-first growth analytics, Berlin
[nonso-analytics.com](https://nonso-analytics.com) · [github.com/Nonsogithub41](https://github.com/Nonsogithub41)
