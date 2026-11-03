# Decoding the 2026 Tamil Nadu Assembly Election

A Python analysis of the 2021 and 2026 Tamil Nadu Assembly election results, built in a Jupyter notebook with pandas and Plotly. It answers three questions:

| Question | Topic | What it asks |
|---|---|---|
| **Q1** | The geographic story | How did seat distribution shift across Tamil Nadu's six regions between 2021 and 2026? |
| **Q2** | The flip story | In how many constituencies did the winning party change, and where did the seats go? |
| **Q6** | The margin of victory story | How did the average margin of victory change, and how many seats were won with more than 50% or less than 35% of the votes? |


## Key findings

The figures below come from the notebook's summary cell. **Run the notebook on your data to regenerate and confirm them before you rely on them.**

| Question | Finding |
|---|---|
| Q1 Geographic | TVK won 108 seats, dominant in Chennai Metro (29 of 32) and Kongu (16 of 33). DMK fell from 133 seats to 59. |
| Q2 Flips | 161 of 234 constituencies (69%) changed winning party. 65 seats moved directly from DMK to TVK. |
| Q6 Margin | The average margin fell from 22,871 to 16,784 votes (-27%). Seats won with less than 35% of the vote rose from 2 to 64. |

## Method

1. **Winner and runner-up per constituency:** sort candidates by votes, take the top two in each constituency (`ac_number`).
2. **Vote share:** winner's votes divided by total votes in the constituency.
3. **Margin:** winner's votes minus runner-up's votes.
4. **Party groups:** DMK, AIADMK, TVK, NTK, and Others (all remaining parties).
5. **Flip:** a constituency whose winning party group in 2026 differs from 2021.
6. **Vote-share buckets:** more than 50% (dominant), 35 to 50% (competitive), less than 35% (fragmented).

## Charts produced

| File | Description |
|---|---|
| `q1_regional_seats.html` | Seats by region and party, 2021 vs 2026 (grouped bars) |
| `q2_sankey.html` | Seat flow from 2021 winners to 2026 winners (Sankey) |
| `q2_flip_region.html` | Percentage of constituencies that flipped, by region |
| `q6_margin_dist.html` | Distribution of winner vote share, 2021 vs 2026, with 35% and 50% thresholds |
| `q6_buckets.html` | Constituencies by vote-share bucket |
| `q6_scatter.html` | Winner vote share against margin, 2026 |

The notebook also exports CSVs for Power BI: `q1_region_seats.csv`, `q2_flips_detail.csv`, `q2_sankey_flows.csv`, `q6_margins.csv` and `winners_all.csv`.

## Data

The notebook reads three CSV files from the same folder:

| File | Expected content |
|---|---|
| `tn_2021_results.csv` | One row per candidate: `ac_number`, `constituency`, `party`, `votes`, `region`, `reserved` |
| `tn_2026_results.csv` | Same columns for 2026 |
| `constituency_master.csv` | Constituency reference data (loaded, but not used in the current analysis) |

The data files are not included in this repository. Add your own copies, or download the official results from the Election Commission of India (<https://results.eci.gov.in>).

## How to run

```bash
pip install pandas plotly jupyter
jupyter notebook tn_election_analysis.ipynb
```

Place the three CSV files next to the notebook, then run all cells. Charts open in the notebook and are saved as HTML files in the same folder.

## Limitations

- **Party level, not alliance level.** Seats are counted by party. Alliance totals (for example, a party plus its allies) are not modelled.
- **"Others" is one group.** A seat that moves between two parties inside "Others" is not counted as a flip.
- **2026 turnout is blank** in `tn_2026_results.csv`, so there is no turnout analysis. Source it from the ECI Form 20 results if you need it.
- **Margin is measured in votes.** A vote margin is not comparable across constituencies of different size, so read it alongside vote share.
- The analysis shows what happened, not why. Explanations such as anti-incumbency or the effect of a new party need other evidence.

## Repository structure

```
.
├── README.md
├── tn_election_analysis.ipynb
├── data/                  # add the three CSV files here
├── outputs/               # HTML charts and exported CSVs
└── images/                # optional chart screenshots for this README
```

## Tools

Python, pandas, Plotly, Jupyter Notebook, Power BI (for the exported CSVs).

## Author
[Neelamma]

