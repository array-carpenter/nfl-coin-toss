# nfl-coin-toss

Every NFL coin toss since 2008, parsed from the official game books: who won the toss, what they
chose, who received, and which goal each team defended. Regular season and playoffs, 4,976 games.

```r
toss <- read.csv("https://raw.githubusercontent.com/array-carpenter/nfl-coin-toss/main/coin_toss.csv")
```

```python
import pandas as pd
toss = pd.read_csv("https://raw.githubusercontent.com/array-carpenter/nfl-coin-toss/main/coin_toss.csv")
```

`game_id` is the nflverse game id, so it joins straight to nflfastR play-by-play.

## Columns

One row per toss decision: `opening`, `2nd_half`, and `ot1` for overtime.

| column | notes |
|---|---|
| `game_id` | nflverse game id |
| `season`, `game_type`, `week`, `gameday` | `game_type` is REG, WC, DIV, CON or SB |
| `away_team`, `home_team` | nflverse team abbreviations |
| `period` | `opening`, `2nd_half`, `ot1` |
| `toss_winner` | team that won the toss; empty for `2nd_half` |
| `choice` | `receive`, `defer`, `kick` or `defend`; empty for `2nd_half` |
| `receiving_team` | team that received the kickoff |
| `goal_team` | team that picked a goal to defend |
| `goal` | `north`, `south`, `east` or `west` |

## Notes

- `receiving_team` comes from the kickoff that follows the toss, not the toss sentence. The two
  disagree now and then, and the kickoff is what happened. Opening and 2nd half receivers match
  nflfastR kickoffs in every game.
- `goal` is empty when the game book doesn't name a direction. Some 2009-2013 books say
  "defend the kick goal".
- The 2nd half row has no toss. The team that didn't choose at the opening toss gets the choice.

Updated weekly during the season.
