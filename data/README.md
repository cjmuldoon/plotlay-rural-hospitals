# The data

## tables/

| File | Rows | What |
|---|---:|---|
| `hospitals.csv` | 293 | Every hospital in the study area (Oklahoma and the counties within 100 km of it): `ccn` (CMS number, the key), name, town, state, type, rural or urban, `in_scenario`, `beds`, `patients` (average a day), `beds_source` (hhs, hcris, pos), `occupancy_today`, `added_patients` and `occupancy_scenario` (variant A), `added_patients_b` and `occupancy_scenario_b` (variant B), `loss_years` (of 2021-24), `medicaid_share` (%), `margin_2021` to `margin_2024` (total margin, %) |
| `blockgroups.csv` | 3374 | Oklahoma's block groups: `geoid` (key), `population` (ACS 2020-24), rural or urban (tract RUCA), `minutes_today`, `minutes_scenario`, `minutes_added`, the bands, `change`, the nearest hospital today and in the scenario |
| `counties.csv` | 77 | Oklahoma's counties rolled up from their block groups: people, people over 30 minutes today and in the scenario, the average drive (weighted by people) |
| `closures.csv` | 20 | Oklahoma's rural hospitals that stopped inpatient care since 2005: `closure` (its CMS number, with the year where one number closed twice), name, town, the date Medicare ended the agreement, what happened, the year it reopened |
| `closure_years.csv` | 440 | Each of them at the end of each year 2005 to 2026: Open, Inpatient care ended, Rural Emergency Hospital, Reopened |
| `states.csv` | 51 | Each state and DC: rural hospitals with cost reports 2021-24, with losses in 3 or more years, meeting the rule |
| `state_years.csv` | 1122 | Each state and year: rural inpatient closures and conversions so far since 2005, and in the year |
| `risk_by_state.csv` | | The same counts as `states.csv`, as the build wrote them |
| `rural_terminations_us.csv` | | Every rural short-term and critical access hospital whose Medicare agreement ended since 2005, with its class (`continued`, `closed`, `reopened`, `reh`) and successor |
| `cost_reports.csv` | | The cost report figures behind the rule for the study area's hospitals, fiscal years 2021-24 |
| `patient_moves.csv` | | Average patients a day each closing hospital would send to each other hospital, variants A and B (not people) |
| `drive_summary.json` | | The engine's summary of the three runs: network size, speeds, weighted means, people over each threshold |

## geometry/

`hospitals`, `blockgroups`, `counties`, `closures` and `states` as GeoJSON (WGS84), TopoJSON (for Power BI's Shape Map) and CSV with WKT (Azure Maps, Python), exported from Plotlay with their keys; `bands_today.geojson` and `bands_scenario.geojson`, the travel-time bands over Oklahoma (cells of 2 km).

Hospitals are drawn as discs 400 m across at their address points; the closures as discs 8 km across, so they show on a map of the whole state. Block group outlines are the Census Bureau's 1:500,000 cartographic boundaries, simplified.
