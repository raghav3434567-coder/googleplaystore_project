# Google Play Store Apps Analysis

An exploratory data analysis (EDA) of 10,841 Google Play Store app listings using **Python, pandas and NumPy**. The notebook inspects the data, finds and removes a corrupted row, and answers questions about ratings, reviews, categories, and free vs paid apps.

## Project Structure

```
.
├── googleplaystore_project.ipynb     # Analysis notebook
├── googleplaystore.csv               # Dataset (10,841 rows x 13 columns)
├── GooglePlayStore_Project_Report.pdf  # Detailed project report
└── README.md                         # This file
```

> Place `googleplaystore.csv` in the same folder as the notebook; it is read with a relative path.

## Dataset

| Column | Description |
|---|---|
| App | App name |
| Category | App category (e.g. ART_AND_DESIGN, FAMILY, EVENTS) |
| Rating | Average user rating (9,367 non-null values) |
| Reviews | Number of reviews (stored as text) |
| Size | App size, e.g. `19M` or `Varies with device` |
| Installs | Install bracket, e.g. `10,000+` (text) |
| Type | Free or Paid |
| Price | Price (text) |
| Content Rating | Everyone, Teen, Mature 17+, etc. |
| Genres | Genre label(s) |
| Last Updated | Date of last update (text) |
| Current Ver | Current app version |
| Android Ver | Minimum Android version |

## What the Notebook Does

1. Loads the data and inspects it (`head`, `tail`, shape, dtypes, `info`, `describe`).
2. Searches app titles for the word "Astrology".
3. Counts unique categories and ranks categories by average rating.
4. Counts apps with a perfect 5.0 rating.
5. Cleans the data: drops one corrupted row (index 10472) and converts `Reviews` to numbers.
6. Counts free vs paid apps.
7. Finds the apps with the most reviews (top 1 and top 10).
8. Compares average reviews of free and paid apps.

## Key Results

| Metric | Result |
|---|---|
| Rows / columns | 10,841 / 13 |
| Mean rating (before cleaning) | 4.19 (max shows 19, a data error) |
| Unique categories | 34 (includes one corrupted value, `1.9`) |
| Highest-rated real category | EVENTS (4.44) |
| Apps with a 5.0 rating | 274 |
| Free / paid apps | 10,039 / 800 |
| Apps with "Astrology" in the title | 3 |
| Most reviewed app | Facebook |
| Average reviews (all / free / paid) | 444,153 / 478,661 / 11,673 |

## How to Run

```bash
pip install numpy pandas jupyter
jupyter notebook googleplaystore_project.ipynb
```

Python 3.12+ is recommended, because the notebook nests same-type quotes inside f-strings.

## Known Limitations

- Row 10472 is corrupted (its columns are shifted, giving a rating of 19 and a category of `1.9`). It is removed by hard-coded index in four separate cells, but the first few results (mean rating, category ranking, unique categories) are computed before it is removed.
- Duplicate apps are not removed. The top 10 by reviews lists Facebook twice, WhatsApp three times and Instagram four times, which also inflates average reviews.
- The second line of the free vs paid average prints "For free apps" for the paid group.
- `Size`, `Installs` and `Price` remain text, so no numeric analysis is done on them.
- 1,474 apps have no rating; this is not handled or reported.
- The top review app is found with a hard-coded index (`loc[2544]`).

See `GooglePlayStore_Project_Report.pdf` for details and recommended fixes.

## Tech Stack

Python, pandas, NumPy, Jupyter Notebook
