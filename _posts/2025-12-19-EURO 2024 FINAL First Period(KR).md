#**Install relevant packages**


```python
%%capture
!pip install statsbombpy
!pip install mplsoccer
!pip install highlight_text
```

#**Import packages**


```python
%%capture
from statsbombpy import sb
import pandas as pd
import numpy as np
from mplsoccer import VerticalPitch,Pitch
from highlight_text import ax_text, fig_text
from matplotlib.colors import LinearSegmentedColormap
import matplotlib.pyplot as plt
import matplotlib.patheffects as path_effects
from matplotlib.lines import Line2D
from matplotlib.offsetbox import OffsetImage, AnnotationBbox
import seaborn as sns
```

#**Import API's**


```python
#Call Statsbombpy API
free_comps = sb.competitions()
#Print a list of free competitions
free_comps
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>competition_id</th>
      <th>season_id</th>
      <th>country_name</th>
      <th>competition_name</th>
      <th>competition_gender</th>
      <th>competition_youth</th>
      <th>competition_international</th>
      <th>season_name</th>
      <th>match_updated</th>
      <th>match_updated_360</th>
      <th>match_available_360</th>
      <th>match_available</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9</td>
      <td>281</td>
      <td>Germany</td>
      <td>1. Bundesliga</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>2023/2024</td>
      <td>2024-09-28T20:46:38.893391</td>
      <td>2025-07-06T04:26:07.636270</td>
      <td>2025-07-06T04:26:07.636270</td>
      <td>2024-09-28T20:46:38.893391</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>27</td>
      <td>Germany</td>
      <td>1. Bundesliga</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>2015/2016</td>
      <td>2024-05-19T11:11:14.192381</td>
      <td>None</td>
      <td>None</td>
      <td>2024-05-19T11:11:14.192381</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1267</td>
      <td>107</td>
      <td>Africa</td>
      <td>African Cup of Nations</td>
      <td>male</td>
      <td>False</td>
      <td>True</td>
      <td>2023</td>
      <td>2024-09-28T01:57:35.846538</td>
      <td>None</td>
      <td>None</td>
      <td>2024-09-28T01:57:35.846538</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16</td>
      <td>4</td>
      <td>Europe</td>
      <td>Champions League</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>2018/2019</td>
      <td>2025-05-08T15:10:50.835274</td>
      <td>2021-06-13T16:17:31.694</td>
      <td>None</td>
      <td>2025-05-08T15:10:50.835274</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>1</td>
      <td>Europe</td>
      <td>Champions League</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>2017/2018</td>
      <td>2024-02-13T02:35:28.134882</td>
      <td>2021-06-13T16:17:31.694</td>
      <td>None</td>
      <td>2024-02-13T02:35:28.134882</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>35</td>
      <td>75</td>
      <td>Europe</td>
      <td>UEFA Europa League</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>1988/1989</td>
      <td>2024-02-12T14:45:05.702250</td>
      <td>2021-06-13T16:17:31.694</td>
      <td>None</td>
      <td>2024-02-12T14:45:05.702250</td>
    </tr>
    <tr>
      <th>71</th>
      <td>53</td>
      <td>315</td>
      <td>Europe</td>
      <td>UEFA Women's Euro</td>
      <td>female</td>
      <td>False</td>
      <td>True</td>
      <td>2025</td>
      <td>2025-07-28T14:19:20.467348</td>
      <td>2025-07-29T16:03:07.355174</td>
      <td>2025-07-29T16:03:07.355174</td>
      <td>2025-07-28T14:19:20.467348</td>
    </tr>
    <tr>
      <th>72</th>
      <td>53</td>
      <td>106</td>
      <td>Europe</td>
      <td>UEFA Women's Euro</td>
      <td>female</td>
      <td>False</td>
      <td>True</td>
      <td>2022</td>
      <td>2024-02-13T13:27:17.178263</td>
      <td>2024-02-13T13:30:52.820588</td>
      <td>2024-02-13T13:30:52.820588</td>
      <td>2024-02-13T13:27:17.178263</td>
    </tr>
    <tr>
      <th>73</th>
      <td>72</td>
      <td>107</td>
      <td>International</td>
      <td>Women's World Cup</td>
      <td>female</td>
      <td>False</td>
      <td>True</td>
      <td>2023</td>
      <td>2025-07-14T10:07:06.620906</td>
      <td>2025-07-14T10:10:27.224586</td>
      <td>2025-07-14T10:10:27.224586</td>
      <td>2025-07-14T10:07:06.620906</td>
    </tr>
    <tr>
      <th>74</th>
      <td>72</td>
      <td>30</td>
      <td>International</td>
      <td>Women's World Cup</td>
      <td>female</td>
      <td>False</td>
      <td>True</td>
      <td>2019</td>
      <td>2024-08-08T15:57:56.748740</td>
      <td>2021-06-13T16:17:31.694</td>
      <td>None</td>
      <td>2024-08-08T15:57:56.748740</td>
    </tr>
  </tbody>
</table>
<p>75 rows × 12 columns</p>
</div>




```python
#call the statsbombpy API to get a list of matches for a given competition
#Euro 2024 competition id, season id
#competition_id=55, season_id=282
euro_2024_matches = sb.matches(competition_id=55, season_id=282)

row_count = len(euro_2024_matches)

row_count
```




    51




```python
#create a variable for the team you want to look into
team="England"

#filter for only matches that the focus team played in
matches_df = euro_2024_matches[(euro_2024_matches['home_team'] == team)|(euro_2024_matches['away_team'] == team)]

#sort by match date to get the most recent match
matches_df=matches_df.sort_values(by='match_date', ascending=False)
```


```python
#create a variable containing the first match id in the data frame
latest_match_id = matches_df.match_id.iloc[0]

#latest_match_id=3943043
```


```python
#call the statsbombpy events API to bring in the event data for the match
events_df = sb.events(match_id=latest_match_id)


events_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>50_50</th>
      <th>ball_receipt_outcome</th>
      <th>ball_recovery_recovery_failure</th>
      <th>block_deflection</th>
      <th>block_offensive</th>
      <th>block_save_block</th>
      <th>carry_end_location</th>
      <th>clearance_aerial_won</th>
      <th>clearance_body_part</th>
      <th>clearance_head</th>
      <th>...</th>
      <th>substitution_outcome</th>
      <th>substitution_outcome_id</th>
      <th>substitution_replacement</th>
      <th>substitution_replacement_id</th>
      <th>tactics</th>
      <th>team</th>
      <th>team_id</th>
      <th>timestamp</th>
      <th>type</th>
      <th>under_pressure</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>{'formation': 4231, 'lineup': [{'player': {'id...</td>
      <td>Spain</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>{'formation': 4231, 'lineup': [{'player': {'id...</td>
      <td>England</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>England</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Spain</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>England</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 92 columns</p>
</div>




```python
#print a list of columns available in the event data
events_df.columns
```




    Index(['50_50', 'ball_receipt_outcome', 'ball_recovery_recovery_failure',
           'block_deflection', 'block_offensive', 'block_save_block',
           'carry_end_location', 'clearance_aerial_won', 'clearance_body_part',
           'clearance_head', 'clearance_left_foot', 'clearance_right_foot',
           'counterpress', 'dribble_nutmeg', 'dribble_outcome', 'dribble_overrun',
           'duel_outcome', 'duel_type', 'duration', 'foul_committed_advantage',
           'foul_committed_card', 'foul_committed_offensive', 'foul_won_advantage',
           'foul_won_defensive', 'goalkeeper_body_part', 'goalkeeper_end_location',
           'goalkeeper_outcome', 'goalkeeper_position', 'goalkeeper_technique',
           'goalkeeper_type', 'id', 'index', 'injury_stoppage_in_chain',
           'interception_outcome', 'location', 'match_id', 'minute', 'off_camera',
           'out', 'pass_aerial_won', 'pass_angle', 'pass_assisted_shot_id',
           'pass_body_part', 'pass_cross', 'pass_cut_back', 'pass_end_location',
           'pass_goal_assist', 'pass_height', 'pass_inswinging', 'pass_length',
           'pass_no_touch', 'pass_outcome', 'pass_outswinging', 'pass_recipient',
           'pass_recipient_id', 'pass_shot_assist', 'pass_switch',
           'pass_technique', 'pass_through_ball', 'pass_type', 'period',
           'play_pattern', 'player', 'player_id', 'position', 'possession',
           'possession_team', 'possession_team_id', 'related_events', 'second',
           'shot_aerial_won', 'shot_body_part', 'shot_deflected',
           'shot_end_location', 'shot_first_time', 'shot_freeze_frame',
           'shot_key_pass_id', 'shot_one_on_one', 'shot_outcome',
           'shot_statsbomb_xg', 'shot_technique', 'shot_type',
           'substitution_outcome', 'substitution_outcome_id',
           'substitution_replacement', 'substitution_replacement_id', 'tactics',
           'team', 'team_id', 'timestamp', 'type', 'under_pressure'],
          dtype='object')



#**Preprocessing**


```python
#separate start and end locations from coordinates
events_df[['x', 'y']] = events_df['location'].apply(pd.Series)
events_df[['pass_end_x', 'pass_end_y']] = events_df['pass_end_location'].apply(pd.Series)
events_df[['carry_end_x', 'carry_end_y']] = events_df['carry_end_location'].apply(pd.Series)
```


```python
print(events_df['pass_outcome'].unique())
print(events_df['duel_outcome'].unique())
print(events_df['duel_type'].unique())
print(events_df['dribble_outcome'].unique())
print(events_df['position'].unique())
print(events_df['possession'].unique())
```

    [nan 'Out' 'Incomplete' 'Unknown' 'Pass Offside']
    [nan 'Won' 'Success In Play' 'Lost Out' 'Lost In Play' 'Success Out']
    [nan 'Tackle' 'Aerial Lost']
    [nan 'Incomplete' 'Complete']
    [nan 'Right Defensive Midfield' 'Goalkeeper' 'Right Center Back'
     'Right Back' 'Center Forward' 'Center Attacking Midfield' 'Left Wing'
     'Left Center Back' 'Left Back' 'Left Defensive Midfield' 'Right Wing'
     'Right Center Midfield' 'Center Defensive Midfield' 'Left Center Forward'
     'Right Center Forward']
    [  1  79   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  46  47  48  49  50  51  52  53  54
      56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  72  73  74
      75  77  78  80  81  82  83  84  85  86  87  88  89  90  91  92  93  94
      95  96  97  98  99 100 101 102 103 104 105 106 107 108 109 110 111 112
     113 114 115 117 119 120 121 122 123 124 125 126 127 128 129 130 132 133
     134 135 136 137 138 139 140 141 142 143 144 145 146 147  71 131 118  45
      76 116  55]
    


```python
events_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>50_50</th>
      <th>ball_receipt_outcome</th>
      <th>ball_recovery_recovery_failure</th>
      <th>block_deflection</th>
      <th>block_offensive</th>
      <th>block_save_block</th>
      <th>carry_end_location</th>
      <th>clearance_aerial_won</th>
      <th>clearance_body_part</th>
      <th>clearance_head</th>
      <th>...</th>
      <th>team_id</th>
      <th>timestamp</th>
      <th>type</th>
      <th>under_pressure</th>
      <th>x</th>
      <th>y</th>
      <th>pass_end_x</th>
      <th>pass_end_y</th>
      <th>carry_end_x</th>
      <th>carry_end_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 98 columns</p>
</div>




```python
#separate the period
sel_period = 1

df = events_df[events_df['period'] == sel_period].copy()

#sort the DataFrame by timestamp in descending order
fp = df.sort_values(by='timestamp', ascending=True)

fp.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>50_50</th>
      <th>ball_receipt_outcome</th>
      <th>ball_recovery_recovery_failure</th>
      <th>block_deflection</th>
      <th>block_offensive</th>
      <th>block_save_block</th>
      <th>carry_end_location</th>
      <th>clearance_aerial_won</th>
      <th>clearance_body_part</th>
      <th>clearance_head</th>
      <th>...</th>
      <th>team_id</th>
      <th>timestamp</th>
      <th>type</th>
      <th>under_pressure</th>
      <th>x</th>
      <th>y</th>
      <th>pass_end_x</th>
      <th>pass_end_y</th>
      <th>carry_end_x</th>
      <th>carry_end_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>768</td>
      <td>00:00:00.340</td>
      <td>Pass</td>
      <td>NaN</td>
      <td>60.0</td>
      <td>40.0</td>
      <td>25.4</td>
      <td>38.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 98 columns</p>
</div>



#**Player & Team xG**


```python
# 페널티 제외
df1 = fp[fp['shot_type'] != 'Penalty'].copy()

# --- 선수별 xG 합계 ---
p_xg = df1.groupby('player')['shot_statsbomb_xg'].sum().round(2)

# --- 선수별 슈팅 횟수 (결측이 아닌 shot_outcome만 카운트) ---
p_shots = df1[df1['shot_outcome'].notna()].groupby('player').size()

# --- 두 결과를 하나로 합치기 ---
p_stats = pd.concat([p_xg, p_shots], axis=1)
p_stats.columns = ['xG_sum', 'Shots']
p_stats = p_stats.sort_values('xG_sum', ascending=False)

# --- 팀별 xG ---
t_xg = df1.groupby('team')['shot_statsbomb_xg'].sum().round(2)

# --- 출력 ---
print(f'Player & Team xG in {sel_period} Period')
print('-----------------------------------------------')
print(p_stats.head(12))
print('-----------------------------------------------')
print(t_xg)

```

    Player & Team xG in 1 Period
    -----------------------------------------------
                                  xG_sum  Shots
    player                                     
    Phil Foden                      0.18    1.0
    Robin Aime Robert Le Normand    0.12    1.0
    Álvaro Borja Morata Martín      0.08    1.0
    Nicholas Williams Arthuer       0.07    1.0
    Declan Rice                     0.05    1.0
    Fabián Ruiz Peña                0.05    1.0
    Harry Kane                      0.05    1.0
    Daniel Olmo Carvajal            0.03    1.0
    Luke Shaw                       0.00    NaN
    Unai Simón Mendibil             0.00    NaN
    Rodrigo Hernández Cascante      0.00    NaN
    Marc Guehi                      0.00    NaN
    -----------------------------------------------
    team
    England    0.28
    Spain      0.34
    Name: shot_statsbomb_xg, dtype: float64
    

#**England‘s Passsing Map**


```python
TEAM_NAME = 'England'
TEAM_COLOR = 'white' #darkred or white

# --- 데이터 전처리 ---
df = fp.copy()

# 좌표와 id만 숫자로, outcome들은 문자열 그대로 두기
num_cols = ['x','y','pass_end_x','pass_end_y','player_id','pass_recipient_id','period']
for c in num_cols:
    if c in df.columns:
        df[c] = pd.to_numeric(df[c], errors='coerce')

# 성공 패스만, StatsBomb에서는 pass_outcome이 NaN이면 성공
team_passes = (
    df[(df['team'] == TEAM_NAME)
       & (df['type'] == 'Pass')
       & (df['pass_outcome'].isna())]
    .dropna(subset=['x','y','pass_end_x','pass_end_y','player_id','pass_recipient_id'])
)

# 슛, 골 표기, shot_outcome으로 골 판단
team_shots = df[(df['team'] == TEAM_NAME) & (df['type'] == 'Shot')].copy()
team_shots['sx'] = team_shots['x']
team_shots['sy'] = team_shots['y']

id_to_name = (df[['player_id','player']].dropna()
              .drop_duplicates('player_id')
              .set_index('player_id')['player'].to_dict())

def make_network(team_df, min_edge_count=1):
    # 엣지, 패스 송수신 쌍과 횟수
    edges = (team_df
             .dropna(subset=['player_id','pass_recipient_id'])
             .groupby(['player_id','pass_recipient_id']).size()
             .reset_index(name='count'))
    edges = edges[edges['count'] >= min_edge_count].copy()

    # 노드, 평균 위치
    out_pos = (team_df.groupby('player_id')[['x','y']]
               .mean().rename(columns={'x':'x_out','y':'y_out'}))
    in_pos  = (team_df.groupby('pass_recipient_id')[['pass_end_x','pass_end_y']]
               .mean().rename(columns={'pass_end_x':'x_in','pass_end_y':'y_in'}))

    node_ids = pd.Index(out_pos.index).union(pd.Index(in_pos.index))
    nodes = (pd.DataFrame(index=node_ids)
             .join(out_pos, how='left')
             .join(in_pos, how='left'))
    nodes['x'] = nodes[['x_out','x_in']].mean(axis=1, skipna=True)
    nodes['y'] = nodes[['y_out','y_in']].mean(axis=1, skipna=True)

    sent = team_df.groupby('player_id').size().rename('sent')
    recv = team_df.groupby('pass_recipient_id').size().rename('received')
    nodes = nodes.join(sent, how='left').join(recv, how='left')
    nodes[['sent','received']] = nodes[['sent','received']].fillna(0)
    nodes['count'] = nodes['sent'] + nodes['received']

    nodes['name'] = nodes.index.map(lambda pid: id_to_name.get(pid, str(int(pid)) if pd.notna(pid) else 'NA'))
    nodes = nodes.dropna(subset=['x','y'])
    return nodes, edges

pitch = Pitch(pitch_type='statsbomb', pitch_color='grass', line_color='white')
fig, ax = pitch.draw(ncols=1, nrows=1, figsize=(7, 6.5))
fig.subplots_adjust(top=0.85)

period = 1
half_passes = team_passes[team_passes['period'] == period]
nodes, edges = make_network(half_passes, min_edge_count=1)

# 패스 라인
if not edges.empty and not nodes.empty:
    edges = edges.merge(nodes[['x','y']], left_on='player_id', right_index=True)
    edges = edges.merge(nodes[['x','y']], left_on='pass_recipient_id', right_index=True, suffixes=('_sx','_rx'))
    maxc = edges['count'].max()
    lw_scale = (4.0/maxc) if maxc and maxc > 0 else 1.5
    for _, r in edges.iterrows():
        pitch.lines(r['x_sx'], r['y_sx'], r['x_rx'], r['y_rx'],
                    ax=ax, lw=max(0.8, r['count']*lw_scale),
                    alpha=0.75, color=TEAM_COLOR, zorder=3)

# 노드
if not nodes.empty:
    maxn = nodes['count'].max()
    size_scale = (350/maxn) if maxn and maxn > 0 else 120
    pitch.scatter(nodes['x'], nodes['y'],
                  s=np.clip(nodes['count']*size_scale, 80, 800),
                  ax=ax, color=TEAM_COLOR, edgecolors='black', linewidth=0.8, zorder=4)
    for _, r in nodes.iterrows():
        ax.text(r['x'], r['y'], r['name'], fontsize=8, ha='center', va='center',
                color='black',
                bbox=dict(facecolor='white', alpha=0.7, boxstyle='round,pad=0.2'),
                zorder=5)

# 슛, 골 표기, shot_outcome으로 구분
hs = team_shots[team_shots['period'] == period]
if not hs.empty:
    g = hs[hs['shot_outcome'] == 'Goal']
    if not g.empty:
        pitch.scatter(g['sx'], g['sy'], s=90, ax=ax, color='blue',
                      edgecolors='black', linewidth=0.8, marker='o', zorder=6)
    m = hs[hs['shot_outcome'] != 'Goal']
    if not m.empty:
        pitch.scatter(m['sx'], m['sy'], s=90, ax=ax, color='red',
                      edgecolors='black', linewidth=0.8, marker='o', zorder=6)

# 범례와 제목
pass_proxy = Line2D([0],[0], color=TEAM_COLOR, lw=3, label='Pass success')
goal_proxy = Line2D([0],[0], marker='o', color='blue', lw=0, markersize=8,
                    markerfacecolor='blue', markeredgecolor='black', label='Goal')
miss_proxy = Line2D([0],[0], marker='o', color='red', lw=0, markersize=8,
                    markerfacecolor='red', markeredgecolor='black', label='Miss')
ax.legend(handles=[pass_proxy, goal_proxy, miss_proxy], loc='upper right', frameon=True, fontsize=8)
ax.set_title(f"{TEAM_NAME} Passing Map, Period {period}", fontsize=12, pad=8)

plt.show()
plt.savefig(f"England_Passing_Map_{period}.png",dpi=200, bbox_inches="tight")
![England Passing Map]("C:/Users/HP/Downloads/Euro_2024_Final/output_19_0.png")
```


    
![png](output_19_0.png)
    



    <Figure size 640x480 with 0 Axes>


#**Spain’s Passing Map**


```python
TEAM_NAME = 'Spain'
TEAM_COLOR = 'darkred' #darked or white

# --- 데이터 전처리 ---
df = fp.copy()

# 좌표와 id만 숫자로, outcome들은 문자열 그대로 두기
num_cols = ['x','y','pass_end_x','pass_end_y','player_id','pass_recipient_id','period']
for c in num_cols:
    if c in df.columns:
        df[c] = pd.to_numeric(df[c], errors='coerce')

# 성공 패스만, StatsBomb에서는 pass_outcome이 NaN이면 성공
team_passes = (
    df[(df['team'] == TEAM_NAME)
       & (df['type'] == 'Pass')
       & (df['pass_outcome'].isna())]
    .dropna(subset=['x','y','pass_end_x','pass_end_y','player_id','pass_recipient_id'])
)

# 슛, 골 표기, shot_outcome으로 골 판단
team_shots = df[(df['team'] == TEAM_NAME) & (df['type'] == 'Shot')].copy()
team_shots['sx'] = team_shots['x']
team_shots['sy'] = team_shots['y']

id_to_name = (df[['player_id','player']].dropna()
              .drop_duplicates('player_id')
              .set_index('player_id')['player'].to_dict())

def make_network(team_df, min_edge_count=1):
    # 엣지, 패스 송수신 쌍과 횟수
    edges = (team_df
             .dropna(subset=['player_id','pass_recipient_id'])
             .groupby(['player_id','pass_recipient_id']).size()
             .reset_index(name='count'))
    edges = edges[edges['count'] >= min_edge_count].copy()

    # 노드, 평균 위치
    out_pos = (team_df.groupby('player_id')[['x','y']]
               .mean().rename(columns={'x':'x_out','y':'y_out'}))
    in_pos  = (team_df.groupby('pass_recipient_id')[['pass_end_x','pass_end_y']]
               .mean().rename(columns={'pass_end_x':'x_in','pass_end_y':'y_in'}))

    node_ids = pd.Index(out_pos.index).union(pd.Index(in_pos.index))
    nodes = (pd.DataFrame(index=node_ids)
             .join(out_pos, how='left')
             .join(in_pos, how='left'))
    nodes['x'] = nodes[['x_out','x_in']].mean(axis=1, skipna=True)
    nodes['y'] = nodes[['y_out','y_in']].mean(axis=1, skipna=True)

    sent = team_df.groupby('player_id').size().rename('sent')
    recv = team_df.groupby('pass_recipient_id').size().rename('received')
    nodes = nodes.join(sent, how='left').join(recv, how='left')
    nodes[['sent','received']] = nodes[['sent','received']].fillna(0)
    nodes['count'] = nodes['sent'] + nodes['received']

    nodes['name'] = nodes.index.map(lambda pid: id_to_name.get(pid, str(int(pid)) if pd.notna(pid) else 'NA'))
    nodes = nodes.dropna(subset=['x','y'])
    return nodes, edges

pitch = Pitch(pitch_type='statsbomb', pitch_color='grass', line_color='white')
fig, ax = pitch.draw(ncols=1, nrows=1, figsize=(7, 6.5))
fig.subplots_adjust(top=0.85)

period = 1
half_passes = team_passes[team_passes['period'] == period]
nodes, edges = make_network(half_passes, min_edge_count=1)

# 패스 라인
if not edges.empty and not nodes.empty:
    edges = edges.merge(nodes[['x','y']], left_on='player_id', right_index=True)
    edges = edges.merge(nodes[['x','y']], left_on='pass_recipient_id', right_index=True, suffixes=('_sx','_rx'))
    maxc = edges['count'].max()
    lw_scale = (4.0/maxc) if maxc and maxc > 0 else 1.5
    for _, r in edges.iterrows():
        pitch.lines(r['x_sx'], r['y_sx'], r['x_rx'], r['y_rx'],
                    ax=ax, lw=max(0.8, r['count']*lw_scale),
                    alpha=0.75, color=TEAM_COLOR, zorder=3)

# 노드
if not nodes.empty:
    maxn = nodes['count'].max()
    size_scale = (350/maxn) if maxn and maxn > 0 else 120
    pitch.scatter(nodes['x'], nodes['y'],
                  s=np.clip(nodes['count']*size_scale, 80, 800),
                  ax=ax, color=TEAM_COLOR, edgecolors='black', linewidth=0.8, zorder=4)
    for _, r in nodes.iterrows():
        ax.text(r['x'], r['y'], r['name'], fontsize=8, ha='center', va='center',
                color='black',
                bbox=dict(facecolor='white', alpha=0.7, boxstyle='round,pad=0.2'),
                zorder=5)

# 슛, 골 표기, shot_outcome으로 구분
hs = team_shots[team_shots['period'] == period]
if not hs.empty:
    g = hs[hs['shot_outcome'] == 'Goal']
    if not g.empty:
        pitch.scatter(g['sx'], g['sy'], s=90, ax=ax, color='blue',
                      edgecolors='black', linewidth=0.8, marker='o', zorder=6)
    m = hs[hs['shot_outcome'] != 'Goal']
    if not m.empty:
        pitch.scatter(m['sx'], m['sy'], s=90, ax=ax, color='red',
                      edgecolors='black', linewidth=0.8, marker='o', zorder=6)

# 범례와 제목
pass_proxy = Line2D([0],[0], color=TEAM_COLOR, lw=3, label='Pass success')
goal_proxy = Line2D([0],[0], marker='o', color='blue', lw=0, markersize=8,
                    markerfacecolor='blue', markeredgecolor='black', label='Goal')
miss_proxy = Line2D([0],[0], marker='o', color='red', lw=0, markersize=8,
                    markerfacecolor='red', markeredgecolor='black', label='Miss')
ax.legend(handles=[pass_proxy, goal_proxy, miss_proxy], loc='upper right', frameon=True, fontsize=8)
ax.set_title(f"{TEAM_NAME} Passing Map, Period {period}", fontsize=12, pad=8)

plt.show()
plt.savefig(f"Spain Passing Map {period}.png", dpi=200, bbox_inches="tight")
![Spain Passing Map]("C:/Users/HP/Downloads/Spain_Passing_Map_1.png")
```


    
![png](output_21_0.png)
    



    <Figure size 640x480 with 0 Axes>


#**England‘s Passsing Sucess Rates**


```python
Team = 'England'

passes_in_period = fp[fp['type'] == 'Pass'].copy()
successful_passes_count = passes_in_period['pass_outcome'].isna().sum()
total_passes_count = len(passes_in_period)

if total_passes_count > 0:
    tsr = ((successful_passes_count / total_passes_count) * 100).round(2)
else:
    tsr = None # Handle cases with no passes, e.g., set to None or np.nan

print('---------------------------------------------------------------------')
print(f'{Team} Pass Success Rate Per Team:', tsr, '%')
print('---------------------------------------------------------------------')

# Calculate pass success rate per player
player_passes_df = fp[(fp['type'] == 'Pass') & (fp['team'] == Team )].copy()

# Group by player and calculate successful passes and total passes
pass_stats_per_player = player_passes_df.groupby('player').agg(
    successful_passes=('pass_outcome', lambda x: x.isna().sum()),
    total_passes=('type', 'count')
)

# Calculate success rate per player
pass_stats_per_player['success_rate'] = ((pass_stats_per_player['successful_passes'] / pass_stats_per_player['total_passes']) * 100).round(2)

print(f'{Team} Pass Success Rate Per Player:')
print(pass_stats_per_player.sort_values(by='success_rate', ascending=False).head(20))
```

    ---------------------------------------------------------------------
    England Pass Success Rate Per Team: 82.64 %
    ---------------------------------------------------------------------
    England Pass Success Rate Per Player:
                     successful_passes  total_passes  success_rate
    player                                                        
    Marc Guehi                       8             8        100.00
    Bukayo Saka                      8             9         88.89
    John Stones                     15            18         83.33
    Luke Shaw                        9            11         81.82
    Kyle Walker                     16            20         80.00
    Phil Foden                       8            10         80.00
    Kobbie Mainoo                    9            12         75.00
    Jordan Pickford                 13            19         68.42
    Jude Bellingham                 10            15         66.67
    Declan Rice                     11            18         61.11
    Harry Kane                       5            10         50.00
    

#**Spain‘s Passsing Sucess Rates**


```python
Team = 'Spain'

passes_in_period = fp[fp['type'] == 'Pass'].copy()
successful_passes_count = passes_in_period['pass_outcome'].isna().sum()
total_passes_count = len(passes_in_period)

if total_passes_count > 0:
    tsr = ((successful_passes_count / total_passes_count) * 100).round(2)
else:
    tsr = None # Handle cases with no passes, e.g., set to None or np.nan

print('---------------------------------------------------------------------')
print(f'{Team} Pass Success Rate Per Team:', tsr, '%')
print('---------------------------------------------------------------------')

# Calculate pass success rate per player
player_passes_df = fp[(fp['type'] == 'Pass') & (fp['team'] == Team )].copy()

# Group by player and calculate successful passes and total passes
pass_stats_per_player = player_passes_df.groupby('player').agg(
    successful_passes=('pass_outcome', lambda x: x.isna().sum()),
    total_passes=('type', 'count')
)

# Calculate success rate per player
pass_stats_per_player['success_rate'] = ((pass_stats_per_player['successful_passes'] / pass_stats_per_player['total_passes']) * 100).round(2)

print(f'{Team} Pass Success Rate Per Player:')
print(pass_stats_per_player.sort_values(by='success_rate', ascending=False).head(20))
```

    ---------------------------------------------------------------------
    Spain Pass Success Rate Per Team: 82.64 %
    ---------------------------------------------------------------------
    Spain Pass Success Rate Per Player:
                                  successful_passes  total_passes  success_rate
    player                                                                     
    Robin Aime Robert Le Normand                 48            49         97.96
    Marc Cucurella Saseta                        25            26         96.15
    Aymeric Laporte                              48            50         96.00
    Unai Simón Mendibil                          17            18         94.44
    Rodrigo Hernández Cascante                   29            32         90.62
    Daniel Carvajal Ramos                        37            43         86.05
    Fabián Ruiz Peña                             24            30         80.00
    Nicholas Williams Arthuer                    24            31         77.42
    Daniel Olmo Carvajal                         10            13         76.92
    Lamine Yamal Nasraoui Ebana                  13            22         59.09
    Álvaro Borja Morata Martín                    8            14         57.14
    

#**England’s Pass Failed Endpoints**


```python
TEAM_NAME = 'England'
DOT_COLOR = 'white'  # 팀 톤

# 데이터: 실패 패스(Outcome=0)의 종료 지점만 사용
df = fp.copy()
for c in ['pass_end_x','pass_end_y']:
    if c in df.columns:
        df[c] = pd.to_numeric(df[c], errors='coerce')

fail = df[(df['team']==TEAM_NAME) & (df['type']=='Pass') & (df['pass_outcome'].notna())]
fail = fail.dropna(subset=['pass_end_x','pass_end_y'])

# 그리기
pitch = Pitch(pitch_type='statsbomb', pitch_color='grass', line_color='white')
fig, ax = pitch.draw(ncols=1, nrows=1, figsize=(13, 6.5))
fig.subplots_adjust(top=0.83, wspace=0.18)

period = 1
dat = fail[fail['period'] == period]
if not dat.empty:
        # 원형 점: 투명도 누적 → 밀집도 직관적
        ax.scatter(dat['pass_end_x'], dat['pass_end_y'],
                   s=75, facecolor=DOT_COLOR, edgecolor='black',
                   linewidths=0.3, alpha=0.28, zorder=4)
    # 간단한 범례(원형 샘플)
dot_proxy = plt.Line2D([0],[0], marker='o', linestyle='',
                           markersize=8, markerfacecolor=DOT_COLOR,
                           markeredgecolor='black', label='Failed pass end')
ax.legend(handles=[dot_proxy], loc='upper right', fontsize=8, frameon=True)
ax.set_title(f"{TEAM_NAME} Failed Pass Endpoints (Period {period})", fontsize=11, pad=6)

plt.show()
plt.savefig(f"{TEAM_NAME} Failed Pass Endpoints {period}", dpi=200, bbox_inches="tight")
```


    
![png](output_27_0.png)
    



    <Figure size 640x480 with 0 Axes>


#**Spain’s Pass Failed Endpoints**


```python
TEAM_NAME = 'Spain'
DOT_COLOR = 'darkred'  # 팀 톤

# 데이터: 실패 패스(Outcome=0)의 종료 지점만 사용
df = fp.copy()
for c in ['pass_end_x','pass_end_y']:
    if c in df.columns:
        df[c] = pd.to_numeric(df[c], errors='coerce')

fail = df[(df['team']==TEAM_NAME) & (df['type']=='Pass') & (df['pass_outcome'].notna())]
fail = fail.dropna(subset=['pass_end_x','pass_end_y'])

# 그리기
pitch = Pitch(pitch_type='statsbomb', pitch_color='grass', line_color='white')
fig, ax = pitch.draw(ncols=1, nrows=1, figsize=(13, 6.5))
fig.subplots_adjust(top=0.83, wspace=0.18)

period = 1
dat = fail[fail['period'] == period]
if not dat.empty:
        # 원형 점: 투명도 누적 → 밀집도 직관적
        ax.scatter(dat['pass_end_x'], dat['pass_end_y'],
                   s=75, facecolor=DOT_COLOR, edgecolor='black',
                   linewidths=0.3, alpha=0.28, zorder=4)
    # 간단한 범례(원형 샘플)
dot_proxy = plt.Line2D([0],[0], marker='o', linestyle='',
                           markersize=8, markerfacecolor=DOT_COLOR,
                           markeredgecolor='black', label='Failed pass end')
ax.legend(handles=[dot_proxy], loc='upper right', fontsize=8, frameon=True)
ax.set_title(f"{TEAM_NAME} Failed Pass Endpoints (Period {period})", fontsize=11, pad=6)

plt.show()
plt.savefig(f"{TEAM_NAME} Failed Pass Endpoints {period}", dpi=200, bbox_inches="tight")
```


    
![png](output_29_0.png)
    



    <Figure size 640x480 with 0 Axes>


#**Duel Stats**


```python
#선수별 경합 성공률
df = fp.copy()

duel_won_cd = df[df['duel_outcome'].isin(['Won', 'Success In Play', 'Success Out']) | df['clearance_aerial_won'].isin([True])]
duel_won = duel_won_cd.groupby('player').size()
duel_lost_cd = df[df['duel_outcome'].isin(['Lost In Play', 'Lost Out']) | df['duel_type'].isin(['Aerial Lost'])]
duel_lost = duel_lost_cd.groupby('player').size()


# Combine duel_won and duel_lost into a single DataFrame indexed by player
duel_stat = pd.concat([duel_won.rename('Duel Won'), duel_lost.rename('Duel Lost')], axis=1).fillna(0)

duel_stat['Duel Success Rate'] = (duel_stat['Duel Won'] / (duel_stat['Duel Won'] + duel_stat['Duel Lost']) * 100).fillna(0).round(2)
duel_stat = duel_stat.sort_values(by='Duel Success Rate', ascending=False)

# To include team information and filter by team:
# First, get a player-to-team mapping from the original events dataframe
player_team_map = df[['player', 'team']].drop_duplicates(subset=['player']).set_index('player')['team']
# Merge this map with the duel_stat DataFrame
duel_stat = duel_stat.merge(player_team_map, left_index=True, right_index=True, how='left')


print(f'{sel_period} Period Duel Success Rate Per Player:')
print('-------------------------------------------------')
#print(duel_stat.head(30)) # Print top 30 overall

eng_duel_stat = duel_stat[duel_stat['team'] == 'England']
spa_duel_stat = duel_stat[duel_stat['team'] == 'Spain']

print('\nEngland Duel Stats:')
print('-------------------------------------------------')
print(eng_duel_stat)

print('\nSpain Duel Stats:')
print('-------------------------------------------------')
print(spa_duel_stat)
```

    1 Period Duel Success Rate Per Player:
    -------------------------------------------------
    
    England Duel Stats:
    -------------------------------------------------
                     Duel Won  Duel Lost  Duel Success Rate     team
    player                                                          
    Kyle Walker           2.0        0.0             100.00  England
    Marc Guehi            1.0        0.0             100.00  England
    John Stones           2.0        1.0              66.67  England
    Jude Bellingham       3.0        4.0              42.86  England
    Luke Shaw             1.0        2.0              33.33  England
    Bukayo Saka           0.0        2.0               0.00  England
    Harry Kane            0.0        4.0               0.00  England
    Kobbie Mainoo         0.0        2.0               0.00  England
    Phil Foden            0.0        1.0               0.00  England
    
    Spain Duel Stats:
    -------------------------------------------------
                                  Duel Won  Duel Lost  Duel Success Rate   team
    player                                                                     
    Daniel Carvajal Ramos              4.0        1.0              80.00  Spain
    Fabián Ruiz Peña                   1.0        1.0              50.00  Spain
    Robin Aime Robert Le Normand       1.0        1.0              50.00  Spain
    Aymeric Laporte                    1.0        2.0              33.33  Spain
    Daniel Olmo Carvajal               1.0        2.0              33.33  Spain
    Álvaro Borja Morata Martín         1.0        3.0              25.00  Spain
    Rodrigo Hernández Cascante         0.0        1.0               0.00  Spain
    

#**Duel Success Rates**


```python
#duel_won = df[df['duel_outcome'].isin(['Won', 'Success In Play', 'Success Out'])].groupby('team').size()
#duel_lost_cd = df[df['duel_outcome'].isin(['Lost In Play', 'Lost Out']) | df['duel_type'].isin(['Aerial Lost'])]
#duel_lost = duel_lost_cd.groupby('team').size()
#duel_won = df[df['duel_type'].isin(['Tackle'])].groupby('team').size()
#duel_lost = df[df['duel_type'].isin(['Aerial Lost'])].groupby('team').size()
duel_won_cd = df[df['duel_outcome'].isin(['Won', 'Success In Play', 'Success Out']) | df['clearance_aerial_won'].isin([True])]
duel_won = duel_won_cd.groupby('team').size()
duel_lost_cd = df[df['duel_outcome'].isin(['Lost In Play', 'Lost Out']) | df['duel_type'].isin(['Aerial Lost'])]
duel_lost = duel_lost_cd.groupby('team').size()


duel_stat = pd.concat([duel_won, duel_lost], axis=1).fillna(0)
duel_stat.columns = ['Duel Won', 'Duel Lost']

duel_stat['Duel Success Rate'] = (duel_stat['Duel Won'] / (duel_stat['Duel Won'] + duel_stat['Duel Lost']) * 100).fillna(0).round(2)
duel_stat = duel_stat.sort_values(by='Duel Success Rate', ascending=False)

print(f'{sel_period} Period Duel Success Rate Per Team')
print('-------------------------------------------------')
print(duel_stat.head(30))
```

    1 Period Duel Success Rate Per Team
    -------------------------------------------------
             Duel Won  Duel Lost  Duel Success Rate
    team                                           
    Spain           9         11               45.0
    England         9         16               36.0
    

#**Dribble Stats**


```python
df = fp.copy()
dribble_suc = df[df['dribble_outcome'] == 'Complete'].groupby('player').size()
dribble_fail = df[df['dribble_outcome'] == 'Incomplete'].groupby('player').size()
dribble_success_rate = (dribble_suc / (dribble_suc + dribble_fail) * 100).fillna(0).round(2)

dribble_stat = pd.concat([dribble_suc.rename('Dribble Success'), dribble_fail.rename('Dribble Fail'), dribble_success_rate.rename('Dribble Success Rate')], axis=1).fillna(0)

player_index = df[['player', 'team']].drop_duplicates(subset=['player']).set_index('player')['team']
dribble_stat = dribble_stat.merge(player_index, left_index=True, right_index=True, how='left')

dribble_stat  = dribble_stat.sort_values(by='Dribble Success Rate', ascending=False)

eng_dribble_stat = dribble_stat[dribble_stat['team'] == 'England']
spa_dribble_stat = dribble_stat[dribble_stat['team'] == 'Spain']

print(f'{sel_period} Period Dribble Success Rate by Player')
print('-------------------------------------------------------')
print(eng_dribble_stat.head(20))
print('-------------------------------------------------------')
print(spa_dribble_stat.head(20))
```

    1 Period Dribble Success Rate by Player
    -------------------------------------------------------
                     Dribble Success  Dribble Fail  Dribble Success Rate     team
    player                                                                       
    Declan Rice                  1.0           1.0                  50.0  England
    Luke Shaw                    1.0           1.0                  50.0  England
    Jude Bellingham              1.0           0.0                   0.0  England
    Kobbie Mainoo                0.0           1.0                   0.0  England
    Phil Foden                   0.0           1.0                   0.0  England
    -------------------------------------------------------
                                 Dribble Success  Dribble Fail  \
    player                                                       
    Nicholas Williams Arthuer                1.0           1.0   
    Fabián Ruiz Peña                         1.0           0.0   
    Lamine Yamal Nasraoui Ebana              0.0           1.0   
    Álvaro Borja Morata Martín               0.0           1.0   
    
                                 Dribble Success Rate   team  
    player                                                    
    Nicholas Williams Arthuer                    50.0  Spain  
    Fabián Ruiz Peña                              0.0  Spain  
    Lamine Yamal Nasraoui Ebana                   0.0  Spain  
    Álvaro Borja Morata Martín                    0.0  Spain  
    


```python
eng_player = 'Declan Rice'
spa_player = 'Martín Zubimendi Ibáñez'

eng_duel_one = eng_duel_stat.reindex([eng_player]).fillna(0)
spa_duel_one = spa_duel_stat.reindex([spa_player]).fillna(0)

eng_dribble_one = eng_dribble_stat.reindex([eng_player]).fillna(0)
spa_dribble_one = spa_dribble_stat.reindex([spa_player]).fillna(0)

eng_stat = eng_duel_one.merge(eng_dribble_one, left_index=True, right_index=True, how='left')
spa_stat = spa_duel_one.merge(spa_dribble_one, left_index=True, right_index=True, how='left')

print('First Period Player Stats Comparison')
print('---------------------------------------------------------------------------')
print(f'{eng_player} Stats:')
print(eng_stat)
print('---------------------------------------------------------------------------')
print(f'{spa_player} Stats:')
print(spa_stat)
print('---------------------------------------------------------------------------')
```

    First Period Player Stats Comparison
    ---------------------------------------------------------------------------
    Declan Rice Stats:
                 Duel Won  Duel Lost  Duel Success Rate  team_x  Dribble Success  \
    player                                                                         
    Declan Rice       0.0        0.0                0.0       0              1.0   
    
                 Dribble Fail  Dribble Success Rate   team_y  
    player                                                    
    Declan Rice           1.0                  50.0  England  
    ---------------------------------------------------------------------------
    Martín Zubimendi Ibáñez Stats:
                             Duel Won  Duel Lost  Duel Success Rate  team_x  \
    player                                                                    
    Martín Zubimendi Ibáñez       0.0        0.0                0.0       0   
    
                             Dribble Success  Dribble Fail  Dribble Success Rate  \
    player                                                                         
    Martín Zubimendi Ibáñez              0.0           0.0                   0.0   
    
                             team_y  
    player                           
    Martín Zubimendi Ibáñez       0  
    ---------------------------------------------------------------------------
    

    C:\Users\HP\AppData\Local\Temp\ipykernel_25868\1330070284.py:4: FutureWarning: Downcasting object dtype arrays on .fillna, .ffill, .bfill is deprecated and will change in a future version. Call result.infer_objects(copy=False) instead. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      eng_duel_one = eng_duel_stat.reindex([eng_player]).fillna(0)
    C:\Users\HP\AppData\Local\Temp\ipykernel_25868\1330070284.py:5: FutureWarning: Downcasting object dtype arrays on .fillna, .ffill, .bfill is deprecated and will change in a future version. Call result.infer_objects(copy=False) instead. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      spa_duel_one = spa_duel_stat.reindex([spa_player]).fillna(0)
    C:\Users\HP\AppData\Local\Temp\ipykernel_25868\1330070284.py:8: FutureWarning: Downcasting object dtype arrays on .fillna, .ffill, .bfill is deprecated and will change in a future version. Call result.infer_objects(copy=False) instead. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      spa_dribble_one = spa_dribble_stat.reindex([spa_player]).fillna(0)
    


```python
#from google.colab import drive
#drive.mount('/content/drive')
```


```python
#!jupyter nbconvert --to markdown "/content/drive/MyDrive/Colab Notebooks/Euro_2024_Final.ipynb"
```
