# Opening the Power BI report

`RuralHospitals.pbip` is a Power BI Project: the report (`RuralHospitals.Report`, PBIR format) and the semantic model (`RuralHospitals.SemanticModel`, TMDL) saved as text, so the repo can show every change. Power BI Desktop opens it like a `.pbix`.

## What you need

- Power BI Desktop for Windows, a recent version (2026). Projects and the PBIR report format are standard in current versions. If Desktop is older than about mid 2025, turn on **File, Options and settings, Options, Preview features, Power BI Project (.pbip) save option** and **Store reports using enhanced metadata format (PBIR)**, then restart Desktop.
- The repo folder on the Windows machine. In Parallels the Mac home folder is usually shared as `\\Mac\Home`.

## Open it

1. In Windows, go to the repo's `powerbi` folder and double-click `RuralHospitals.pbip`, or in Desktop use **File, Open report, Browse reports** with the file type set to *Power BI project files (\*.pbip)*.
2. The visuals are empty the first time. Select **Refresh** on the Home ribbon.
   - By default the data is read from the repo's public copy on GitHub (`DataFolder` is `https://raw.githubusercontent.com/cjmuldoon/plotlay-rural-hospitals/main/data/`). If Desktop asks how to connect, choose **Anonymous** and then **Connect**.
   - To read the files from disk instead, go to **Home, Transform data, Edit parameters** and set `DataFolder` to the full path of the repo's `data` folder, **ending with a backslash** (for example `\\Mac\Home\plotlay-rural-hospitals\data\`). Then select **OK** and **Apply changes**.
   - If Desktop warns about privacy levels, choose **Ignore privacy levels** (all the sources are public open data).
3. Check the numbers (below).

If the report was updated while open, close Power BI and reopen the .pbip rather than using Apply external changes.

## Check the numbers after Refresh

After **Refresh**:

| Page | Card | Should read |
|---|---|---|
| The rule by state | Meet the rule, United States | 212 |
| The rule by state | Rural hospitals with cost reports | 2,371 |
| Closures since 2005 | Oklahoma since 2005 | 20 |
| The drive | Average drive today (min) | 10.7 |
| The drive | If they closed (min) | 12.8 |
| The drive | Over 30 min today | 132,970 |
| The drive | Over 30 min if they closed | 348,649 |
| Beds | Hospitals that meet the rule | 16 |
| Beds | Their patients a day | 215 |
| Beds | Taking patients, 85% full or more after | 12 |

On **The rule by state**, Oklahoma is the darkest state (20 hospitals) and tops the bar chart.

## The model

- **Hospitals**: one row per hospital of Oklahoma and the counties within 100 km of it (`data/tables/hospitals.csv`): CMS number, name, town, state, type, rural or urban, what happens to it in the scenario, beds, patients a day, beds in use today and in the two versions of the scenario, and the rule's inputs. Measures: `Meet the rule`, `Beds of those meeting the rule`, `Patients of those meeting the rule`, `In use today`, `In use if they closed` (variant A), `In use, to a general hospital` (variant B), `In use if they closed, taking 5 or more`, `Receiving 85% or more`.
- **BlockGroups**: one row per Oklahoma block group (`blockgroups.csv`): people (ACS 2020-24) and minutes to the nearest hospital today and if the 16 closed. The bands sort by `band_order` and `band_today_order`. Measures: `People`, `Average drive today`, `Average drive if they closed` (weighted by people), `Over 30 min today`, `Over 30 min if they closed`, `Over 45 min if they closed`, `Driving longer`.
- **Counties**: one row per Oklahoma county (`counties.csv`), rolled up from its block groups. Measures: `Minutes added`, `County average today`, `County average if they closed`.
- **Closures**: Oklahoma's 20 rural hospitals that stopped inpatient care since 2005 (`closures.csv`). Measure: `Inpatient care ended`.
- **States** and **StateYears**: each state's rural hospitals and how many meet the rule (`states.csv`), and its closures each year (`state_years.csv`), related by `state`. `name_short` is a Power Query column with shorter state names for the bar chart.

## The maps

- **Shape Maps** (pages 1, 3 and 4). The custom maps are saved inside the report (`RuralHospitals.Report/StaticResources/RegisteredResources/`): the lower 48 states and DC (`states_lower48.topojson`, made from `data/geometry/states.topojson` without Alaska and Hawaii, which would leave the rest of the map small), Oklahoma's block groups and its counties (`blockgroups.topojson`, `counties.topojson`, each with the neighbouring states drawn round them in a pale ground tone, from `data/geometry/states.geojson`). If a map shows the world instead (an older Desktop can ignore a saved map): select it, then **Format visual**, **Visual**, **Map settings**, **Map type: Custom map**, **Add map type**, and choose the file from `..\data\geometry\`. If the Shape Map is not in the Visualizations pane, turn it on in **File, Options and settings, Options, Preview features, Shape map visual** and restart Desktop.

## Save a .pbix too

After the refresh, use **File, Save as** with the type **Power BI file (\*.pbix)** to save `powerbi\RuralHospitals.pbix`. It includes the data, so it opens without a refresh.

## Publish (only if you choose to)

Use **Home, Publish**. In the Power BI service, set the semantic model's **Data source credentials** for the GitHub address to **Anonymous**. Scheduled refresh then works with no gateway. **Publish to web** makes a public link, so only use it if you mean the report to be public.

## Shot list for the website and the video

| # | Shot | How | Length |
|---|---|---|---|
| 1 | The rule by state | As it opens | still |
| 2 | Closures since 2005 | As it opens | still |
| 3 | The drive | As it opens; hover a block group in Pittsburg County | still |
| 4 | Counties | As it opens | still |
| 5 | Beds | As it opens | still |

Save page images into `powerbi/Screenshots/` (a PDF export of all pages is fine too).
