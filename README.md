# learn_statsbomb

Learning repository for working with **StatsBomb open-data** (JSON) using Python.  
The notebooks in `myproj/` demonstrate a practical workflow to:

- Load local StatsBomb JSON files (`matches` and `events`)
- Flatten nested JSON into pandas DataFrames
- Filter specific matches/teams/players
- Build **pass maps** using `mplsoccer`
- Compute simple passing metrics (total passes, successful passes, accuracy)
in myproj file is analyze adn visualization for pass
---


### 1) `report.ipynb` — LaLiga transfers + standings → cleaned CSV + small analysis
**Goal:** Pull LaLiga data from LaLiga’s public web endpoints, clean nested JSON fields, export tables to CSV, and run a small “free transfer” summary + plot.

**Main inputs:**
- HTTP endpoints requested with `requests`:
  - Transfers endpoint:
    - `.../competitions/1/transfers?contentLanguage=en&subscription-key=...`
  - Standings endpoint (season subscription slug shown in the notebook):
    - `.../subscriptions/laliga-easports-2025/standing?&contentLanguage=en&subscription-key=...`
- Libraries:
  - `requests`
  - `pandas`
  - (Matplotlib is used for at least one plot output)

**Main steps (high level, but specific):**
- Fetch transfers JSON (`data.keys()` shows `transfers`)
- Convert `transfers` list into a pandas DataFrame (`df`)
- Build a cleaned table (`df_clean`) by extracting nested fields:
  - Extract club nickname/slug from `team_to` and `team_from`
  - Extract procedure name from `procedure` (e.g., `Free`, `Loan`, `Transfer`)
- Convert `date` and export transfers:
  - Writes: `transfers_laliga.csv`
- Fetch standings JSON (`data.keys()` shows `standings`)
- Convert standings into DataFrame (`df1`)
- Build a cleaned standings table (`df1_clean`) extracting:
  - Position, Team nickname, Played, Qualify name
- Export standings:
  - Writes: `standing_laliga.csv`
- Filter transfers where `procedure == "Free"` and compute:
  - `team_to` value counts to find which club has the most incoming free transfers
  - Prints summary in Indonesian (e.g., “Klub terbanyak menggunakan free transfer: ...”)
- Produce at least one bar chart (Matplotlib output image appears in notebook output)

**Outputs created by running the notebook:**
- `transfers_laliga.csv`
- `standing_laliga.csv`
- Inline notebook table previews and at least one plot figure
