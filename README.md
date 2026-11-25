# Winter Olympics 2026: Freestyle Ski & Snowboard Medal Model

Estimates each athlete's chance of winning gold and of reaching the podium in every 2026 Olympic freestyle skiing
and snowboard event, from their results at past Olympics, World Championships and World Cups. The probabilities fed
the gold and podium prices in the Excel sheets.

## Approach

1. **Results history**: finishing positions at Beijing 2022, PyeongChang 2018, the 2023 and 2025 FIS World
   Championships and the 2023–2025 World Cups, plus 2026 World Cup standings, per event and gender.
2. **Scores**: run-by-run judged scores (the `Tricks` files) are cleaned, pivoted to one row per athlete, and
   normalized within each competition so different judging scales are comparable.
3. **Medal probabilities**: Monte Carlo simulation (20,000–50,000 runs) of each athlete's Olympic score from a
   normal distribution with their mean and spread, with a floor on the spread and only the top 25 athletes
   eligible. Three variants per event:
   - **probs1**: all normalized scores.
   - **probs2**: "ceiling" view that drops low scores (below 50 for snowboard), so falls don't drag down
     an athlete who can win.
   - **probs3**: each athlete's top 3 scores only.
4. **Prices**: final gold and podium odds (decimal) for every athlete in every event.

Events: aerials, moguls, halfpipe, slopestyle, big air and ski cross (freestyle skiing); halfpipe, slopestyle,
big air, snowboard cross and parallel slalom (snowboard); men's and women's for each.

## Files

| Path | What it is |
|---|---|
| [`Ski/Ski.Rmd`](Ski/Ski.Rmd) | Freestyle skiing: load, clean, normalize, average-position summaries, the three medal-probability models |
| [`Snow/Board.Rmd`](Snow/Board.Rmd) | Snowboard: same pipeline |
| `Ski/FreeSki - <M/W> <event>.csv`, `Snow/Snowboard - <M/W> <event>.csv` | Finishing positions by competition, top-10/top-3 counts, World Cup standings, win/podium probabilities |
| `Ski/FreeSki Tricks - ...csv`, `Snow/Snowboard Tricks - ...csv` | Judged scores by competition |
| `*/Winter Olympics - ... Gold.xlsx`, `... Podium.xlsx` | Gold and podium odds by event and athlete, with event times |

## Running

Open either Rmd in RStudio and knit or run all chunks. The `read.csv()` calls use absolute paths under
`C:/Users/c.travasos/Downloads/Olympics/`; change them if the folder moves. Packages: `dplyr`, `tidyr`,
`readr`, `tidyverse`.
