# 🧫 COTE Simulation Sandbox: Results & Data Dictionary

This folder documents the **economy simulator** of COTE App and publishes **aggregated** results of its latest run. Row-level logs (one line per simulated submission) stay in the private repository.

> Context and interpretation of the results: see the [main README](../README.md#-the-simulation-sandbox) · [version française](../README.fr.md#-le-bac-à-sable-de-simulation)

## Contents

| Path | What it is |
|---|---|
| [`results/summary_by_profile.csv`](results/summary_by_profile.csv) | One row per virtual-student profile: traffic, Points, radar progress |
| [`results/daily_points.csv`](results/daily_points.csv) | One row per simulated day: submissions and Points issued |
| [`samples/pool_actions_sample.csv`](samples/pool_actions_sample.csv) | 36 example actions from the pool (6 per type), text and type only |
| [`../docs/images/simulation/`](../docs/images/simulation/) | The charts used in the README (light and dark, English and French) |

## The run

| | |
|---|---|
| Virtual students | 200 (Innovator 42 · Random 42 · Follower 40 · Spammer 39 · Regular 37) |
| Action pool | 3,500 actions: 2,000 routine · 800 social · 500 innovation · 200 traps (80 anti-value, 80 unrealistic, 40 fully rejected) |
| Simulated period | 183 days |
| Submissions | 85,062 |
| Points transactions | 52,311 |
| Modules in the loop | 4, 5, 7, 8 (Modules 2 and 3 verdicts are pre-recorded on each action) |

The engine itself has been run for up to 365 simulated days; this is the run documented here.

## Reading the aggregated files

### `results/summary_by_profile.csv`

| Column | Meaning |
|---|---|
| `profile`, `profile_fr` | Virtual-student behavioural profile (English / French name) |
| `students` | Number of agents with this profile |
| `submissions` | Total submissions over the run |
| `submissions_per_student_per_day` | Average daily submissions per student |
| `share_of_submissions_pct` | Profile's share of all submissions |
| `valid_submission_share_pct` | Share of the profile's submissions that are not traps and earned PA |
| `points_total` | Points credited to the profile over the run |
| `share_of_points_pct` | Profile's share of all Points issued |
| `avg_points_per_student` | `points_total` ÷ `students` |
| `pa_yield_index_per_valid_submission` | Average radar progress (PA) per valid submission, after the first 30 days, relative to Innovators (= 100) |

### `results/daily_points.csv`

`day` (0 = first simulated day) · `submissions` · `points_issued` · `points_7day_avg` (trailing average).

### `samples/pool_actions_sample.csv`

`action_id` · `action_type` (`routine`, `social`, `innovation`, `trap_anti_value`, `trap_unrealistic`, `trap_rejected`) · `action_text_fr` (the pool is written in French).

## Data dictionary of the simulation database

The simulator runs on five tables:

| Table | One row per | Main content |
|---|---|---|
| `av_profils` | virtual student | profile type, registration date, current Points, current Tier |
| `av_radars` | virtual student | the 11 radar vertices (PA) and a last-update date |
| `pool_actions` | action | text, type, Module 2 and 3 verdicts, a static difficulty rating, an activation vector (which vertices the action involves) |
| `historique_soumissions` | submission | date, student, action, and the exact coefficients and PA gain applied at that moment |
| `ledger_points` | Points transaction | date, student, originating submission, amount |

Because each submission stores the coefficients that were applied at the time, past results stay readable even if the formulas are tuned later.

---

### 🇫🇷 En bref

Ce dossier documente le **simulateur d'économie** de COTE App et publie des résultats **agrégés** de sa dernière exécution (200 étudiants virtuels, 3 500 actions dont 200 pièges, 183 jours simulés, 85 062 soumissions). Les fichiers `results/` contiennent les agrégats par profil et par jour, `samples/` un échantillon de 36 textes d'actions (en français), et le dictionnaire ci-dessus décrit les cinq tables de la base de simulation. Les logs ligne par ligne restent dans le dépôt privé. Interprétation des résultats : voir le [README principal](../README.fr.md#-le-bac-à-sable-de-simulation).
