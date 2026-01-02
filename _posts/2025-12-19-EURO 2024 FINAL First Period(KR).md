---
layout: single
title:  "EURO 2024 Finals Analytics Period 1 (KOR)"
categories: [Football Analysis (KOR)]
tag: [EURO 2024]
toc: true
---

# Data Analysis

## **Introduction**

이 글은 Statsbomb API를 통한 데이터와 중계 영상 분석에 기반해 잉글랜드와 스페인이 맞붙은 EURO 2024 결승전을 다룹니다. 본격적으로 경기 영상을 분석하기에 앞서, 먼저 데이터와 시각화 자료를 간단히 살펴보며 경기의 흐름을 미리 짚어보고, 이를 바탕으로 몇 가지 질문을 던져 보고자 합니다.

이후 이어지는 영상 분석 파트에서는 앞서 제기한 질문들에 답하는 데 초점을 맞춰 설명하겠습니다.

## **Preprocessing**


```python
#separate start and end locations from coordinates
events_df[['x', 'y']] = events_df['location'].apply(pd.Series)
events_df[['pass_end_x', 'pass_end_y']] = events_df['pass_end_location'].apply(pd.Series)
events_df[['carry_end_x', 'carry_end_y']] = events_df['carry_end_location'].apply(pd.Series)
```


```python
#separate the period
sel_period = 1

df = events_df[events_df['period'] == sel_period].copy()

#sort the DataFrame by timestamp in descending order
fp = df.sort_values(by='timestamp', ascending=True)

fp.head()
```

## **Player & Team xG**


```python
# 페널티 제외
df1 = fp[fp['shot_type'] != 'Penalty'].copy()

# 선수별 xG 합계
p_xg = df1.groupby('player')['shot_statsbomb_xg'].sum().round(2)

# 선수별 슈팅 횟수 (결측이 아닌 shot_outcome만 카운트)
p_shots = df1[df1['shot_outcome'].notna()].groupby('player').size()

# 두 결과 합치기
p_stats = pd.concat([p_xg, p_shots], axis=1)
p_stats.columns = ['xG_sum', 'Shots']
p_stats = p_stats.sort_values('xG_sum', ascending=False)

# 팀별 xG
t_xg = df1.groupby('team')['shot_statsbomb_xg'].sum().round(2)

# 출력
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

## **Duel Stats**

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
```

## **Duel Success Rates**

```python
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

```
1 Period Duel Success Rate Per Team
-------------------------------------------------
         Duel Won  Duel Lost  Duel Success Rate
team                                           
Spain           9         11               45.0
England         9         16               36.0
```

## **Dribble Stats**

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
```

전반전의 xG를 보면 양 팀 모두 본격적인 결정력을 보여 주기보다는 탐색전 성격이 강했다고 볼 수 있습니다. 잉글랜드는 0.28, 스페인은 그보다 약간 높은 0.34를 기록했지만, 둘 다 1 이하의 수치이기 때문에 사실상 ***위협적인 찬스를 만들어냈다고 보기는 어렵습니다.***

경합 성공률을 보면 스페인이 우위를 점했습니다. 스페인은 총 20번의 경합 중 9번을 성공하며 45%를 기록했고, 잉글랜드는 25번 중 9번 성공으로 36%에 그쳤습니다. 여기서 말하는 경합은 공중 볼 경합과 태클 경합을 모두 포함합니다.

## **England‘s Passing Map**


```python
TEAM_NAME = 'England'
TEAM_COLOR = 'white' #darkred or white

# 데이터 전처리
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

![output_19_0]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/output_19_0.png)

## **England‘s Passing Success Rates**

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
```

**England’s Pass Failed Endpoints**

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

![output_27_0]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/output_27_0.png)

잉글랜드의 패싱 맵을 보면 빌드업은 골키퍼부터 시작되는 흐름이었습니다. 조던 픽포드가 팀 내 두 번째로 많은 19개의 패스를 기록한 점을 보면, ***골키퍼를 적극적으로 빌드업에 포함시켜 수적 우위를 만들고자 했던 의도가 읽힙니다.***

또한 시각화에서 선수 위치 원의 크기가 보여주듯이 점유는 주로 오른쪽에서 유지되었습니다. 좌측 조합, 즉 마크 게히, 루크 쇼, 주드 벨링엄이 만든 패스는 팀 전체 150개 중 34개였던 반면, 우측의 존 스톤스, 카일 워커, 부카요 사카는 47개의 패스를 기록하며 시각화에서 예측된 흐름을 확인시켜 줍니다.

여기에 더해 미드필더 세 명 중 두 명, 필 포든과 코비 마이누의 평균 위치도 오른쪽으로 기울어 있었기 때문에 ***우측에 더 많은 인원을 배치하려는 전략적 의도***가 분명하게 드러납니다.

이러한 데이터와 시각화를 바탕으로 두 가지 질문이 생깁니다.
 첫 번째, ***우측에 과밀하게 배치한 공격이 실제로 효과적이었는가**.*
 두 번째, ***중앙과 아이솔레이션 전술을 적용한 좌측 공격은 효율적이었는가**.*

이후 이어지는 스페인의 전반전 프리뷰에서는 이 질문들을 중심으로 분석을 전개해 보겠습니다.

## **Spain’s Passing Map**


```python
TEAM_NAME = 'Spain'
TEAM_COLOR = 'darkred' #darked or white

# 데이터 전처리
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

![output_21_0]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/output_21_0.png)

## **Spain‘s Passing Success Rates**


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

## **Spain’s Pass Failed Endpoints**


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

![output_29_0]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/output_29_0.png)

스페인의 패싱 맵을 보면, 빌드업은 주로 두 센터백에서 시작되는 흐름이었습니다. 잉글랜드는 두 풀백을 거의 윙어처럼 전진 배치하는 경향이 있었기 때문에, ***센터백 둘이 압박에 고스란히 노출되지 않도록 골키퍼가 빌드업에 적극 관여하는 것이 필수적이었죠.***

반면 스페인은 상황이 조금 달랐습니다. 우나이 시몬 골키퍼는 빌드업에 적극적으로 관여하지 않았고, 단 18개의 패스만 전개했습니다. 이에 비해 두 센터백의 평균 패스 숫자는 49.5개로 크게 높습니다. 또 스페인은 ***인버티드 풀백 시스템***을 사용했습니다. 즉, 왼쪽 풀백은 전진 배치하고 오른쪽 풀백은 뒤에 머물며 사실상 세 번째 센터백 역할을 맡는 구조입니다.

미드필더들의 평균 위치도 왼쪽으로 기울어 있었고, 이를 종합해 보면 스페인은 ***왼쪽에서 공격적으로 나가기 위해 중원 자원을 집중적으로 배치하려 했다는 점***을 유추할 수 있습니다. 이 움직임은 동시에 잉글랜드의 공격 전략을 억제하기 위한 대응일 수도 있습니다..

시각화에서는 이해를 돕기 위해 양 팀 모두 왼쪽에서 오른쪽으로 진행하는 것처럼 표현되지만, 실제 경기에서는 잉글랜드가 오른쪽으로, 스페인은 왼쪽으로 공격을 전개했습니다. 앞서 언급했듯이 잉글랜드는 우측의 수적 우위를 노렸고, 그에 맞춰 양 팀 모두 같은 공간에 더 많은 선수를 배치할 수밖에 없는 구조가 만들어졌습니다.

스페인은 여기에 더해 ***라민 야말이라는 뛰어난 우측 윙어***가 있었기 때문에 자신들의 우측을 의도적으로 고립시키는 전술적 움직임을 가져갈 수 있었습니다.

정리하자면, 잉글랜드와 스페인은 모두 한쪽 측면을 주된 공격 루트로 설정했고, 공교롭게도 그 공간이 동일했습니다. 따라서 이 지역이 경기의 핵심 전장이 될 것이라는 예측이 가능합니다.

또 하나의 관점은, ***고립된 측면 공격이 실제로 효과적이었는가*** 하는 점입니다. 패스 실패 지점과 패스 지표를 보면, 양 팀의 고립된 윙어들은 모두 약 60퍼센트의 패스 성공률을 기록했으며, 이는 시각화된 패스 실패 지점이 각각의 고립된 공간에 집중되어 나타난 것과 일치합니다.

결국 영상 분석에서 답해야 할 핵심 질문은 두 가지입니다.
 첫 번째, ***양 팀은 어떻게 과부하가 걸린 측면 싸움에서 우위를 가져갔는가**.*
 두 번째, ***양 팀의 고립된 측면 공격 중 어느 쪽이 더 효율적이었으며, 그 이유는 무엇인가**.*

이 두 질문에 답하게 되면, 전반적으로 양 팀의 낮은 xG와 제한적인 슈팅 시도에 대한 의문도 자연스럽게 해소될 것입니다.

# **Video Analysis**

![image-20251223164735656]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/image-20251223164735656.png)

위의 장면처럼, 전반전에는 영국 측은 조심스럽게 경기에 임했고 압박을 통해 상대가 상대 진영에서 볼을 탈취하기 보다는 위의 사진처럼 중앙 선수들을 맨마킹을 통해 ***중앙을 봉쇄하고 상대를 측면으로 유도***합니다. 

![장면 0]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/장면 0.png)

반면, 처음에 스페인측은 빌드업 시에 로드리가 포백이 넓이를 주고 벌리고 로드리는 중앙으로 내려와 볼 배급을 도와주려는 했지만 언급했듯이 잉글랜드 진영에서 헤리 케인과 필 포든이 적극적으로 마킹을 하며 빌드업을 방해하는 양상을 띕니다. 다음 장면에서 나오는, 이에 대응하기 위한 로드리 선수의 포지셔닝이 굉장히 인상적입니다. 로드리는 포든의 맨마킹을 떨치기 위해 ***센터백 라인까지 내려와 빌드업에 관여***하기를 선택했고 이를 통해 아래의 장면처럼 ***중앙에서 2대 3대의 상황을 발생***시켜 상대가 쉽사리 압박하지 못하게 했고 자연스럽게 점유율을 늘립니다.

![장면 2-1]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/장면 2-1.png)

위 장면에서는 로드리 선수가 우측 풀백인 카르바할 선수가 위쪽으로 이동한 지역으로 내려가 마치 쓰리백의 우측 센터백처럼 위치하는 장면입니다. 이 포지셔닝은 이 영국의 중앙을 사수하기 위한 투자를 역이용할 수 있는 움직임입니다. 두 선수가 중앙에 위치해 있기 때문에 로드리가 공을 몰고 카르바할쪽으로 전진할 경우 순간적으로 상대 ***윙어인 벨링엄과 2대1 상황이 발생***하고 이를 통해 보다 수월하게 상대 진영으로 전진할 수 있고 이와 비슷한 장면이 지속적으로 발생합니다.

![장면 1]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/장면 1.png)

다른 예로는 위 장면이 있습니다. 영국의 좌측 윙어 벨링엄이 중앙 사이 공간으로 패스가 들어가지 않도록 중앙에 위치의 포든과 케인쪽으로 가까이 붙어 있었고 이를 통해 스페인 우측 풀백 카르바할이 보다 쉽게 공을 받았고 이후 벨링엄이 따라가는 양상입니다. 이때 순간적으로 우측 윙어 야말이 공을 받으러 내려오면서 순간적을 ***벨링엄을 상대로 2대1 상황을 만들어 내고 결과적으로 보다 쉽게 점유***를 이어 갑니다. 

![image-20251223165214409]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/image-20251223165214409.png)

다음 장면 또한 비슷한 예로, 로드리가 중원에서 두 명 사이에 위치하기 보다 ***쓰리백의 중앙 수비수처럼 내려와*** 상대가 쉽게 압박하지 못하게 하고 ***기존 두 센터백이 각각 좌측 우측으로 움직여 사이드에서 수적 우위를 점하게 유도***합니다. 

![장면 2]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/장면 2.png)

그렇기에 이어지는 장면에서 라포르테가 상대에 압박을 받지 않고 좌측 공간을 향해 전진합니다. 로드리의 빌드업 관여가 고무적인 이유는 위 상황에서 라포르테가 빠르게 쿠쿠렐라한테 볼을 전달하고 왼쪽 윙어 니코 윌리엄스가 먼저 내려오고 순간적으로 ***사카를 상대로 2대1 상황이 발생***하기 때문입니다.

![장면 3]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/장면 3.png)

이 장면에서도 직접 좌측 사이드로 이동해 쿠쿠렐라의 기존 포지션에 위치해 ***쿠쿠렐라가 한 칸 더 전진이 가능하게 하고*** 동시에 센터백의 패스 선택지가 되어 줍니다. 

이런 식으로 스페인은 전반전 내내 비교적 쉽게 볼을 상대 진영으로 전진시킬 수 있었습니다.

반면에 영국의 경우, 자신들의 시스템에 기반하여 움직이려고 했습니다. 앞서 설명했듯이 중원을 틀어 막고 아래의 연속되는 두 장면처럼 상대를 ***사이드로 유도 후 더블 팀을 붙여 상대를 고립***시킵니다.  

![image-20251223165503586]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/image-20251223165503586.png)

![image-20251223165509024]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/image-20251223165509024.png)

![그림9]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/그림9.png)

또한 빌드업을 거치기 보다는 우측에 하프 라인을 넘은 상대 진영에 선수들을 모아서 경합을 통해 빠르게 상대 진영에서 공을 소유하고자 하는 골기퍼의 골킥이 꽤 많았습니다. 잦은 롱볼 시도로 이전에 언급한 ***픽 포드 골기퍼의 패스 성공률이 68.42%로 비교적 낮을 수 밖에 없는 이유***이기도 합니다. 

![그림10]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/그림10.png)

위 장면은 골킥이 아닌 후방에서부터 빌드업을 할 경우에는 골키퍼를 올려 스페인과 비슷하게 3명의 인원으로 빌드업 시도합니다. 다만 ***차이점이 있다면 선수 간 간격이 훨씬 넓습니다.***

이에 대해 ***스페인은 영국과는 다르게 타이트한 압박 기조***를 보여줍니다. 위 장면에서는 넓은 영국 진영의 간격이 공략 당하는 장면입니다. 스페인 최전방 공격수가 볼을 가진 선수를 압박 후 ***패스 라인을 막고 한 쪽 측면으로 몰아 넣은 뒤 맨마킹 형식으로 압박을 걸고 볼 탈취를 시도***합니다. 

![그림11]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/그림11.png)

이어지는 장면인 위 상황에서 빠른 압박 속에서 게히의 패스가 뒤는 게 내려오는 루크 쇼에 이어지지만 공을 받은 후에는 모든 팀 동료가 마킹 되어 있어 활로를 찾지 못하고 소유권을 내줍니다. 

![그림12]({{site.url}}/images/2025-12-19-EURO 2024 FINAL First Period(KR)/그림12.png)

이 장면도 비슷한 장면으로 위로 올라가 있다가 센터백이 압박을 받자, 윙어 벨링엄이 급하게 받아주러 내려옵니다.

전반전을 보면서 스페인의 압박 전술이 좋았던 것도 맞지만 ***영국이 힘든 경기 양상이 지속되도록 빌미를 제공***했다는 결론에 다다랐습니다. ***준비한 규율과 시스템만을 고집했지만 시스템 자체의 완성도가 높지 않았다***는 게 여실히 드러나는 전반이었다는 게 제 결론입니다.  

주요 요인으로는 ***빌드업 시 측면에서의 너무 넓은 간격***, 골키퍼 ***롱킥을 통한 우측의 경합에 적합하지 않은 선수들의 신장***, ***미흡한 빌드업 체계***가 눈에 뜨는 문제점이라고 보여집니다. 먼저, England Passing Map에서 보여지듯이 기본적으로 좌측 루크쇼의 위치가 굉장히 높습니다. 윙어인 주드 벨링엄과 거의 동일한 포지션이죠. 이 때문에 빌드업시에 너무 넓은 간격으로 압박에 취약해집니다. 루크 쇼와 벨링엄은 둘 다 높이 올라가 있는 상태에서 빌드업이 시작되고 영국의 좌측은 자연스럽게 숫자가 부족해집니다. 뒤늦게 루크 쇼나 벨링엄이 받아주러 내려오지만 내려오는 시간이 결려 수비들은 이미 자리를 잡고 영국 선수들에 밀착 마킹이 된 상태로 영국 선수들은 돌아서 정면을 볼 수 없어 ***어렵게 백패스를 하거나 시간이 끌리면 고립될 수 있는 리스크를 감수하더라도 등져서 버텨내야 하는 딜레마에 빠집니다.***

다시 말하면 몇몇 선수들의 포지셔닝은 롱볼을 위한 포지셔닝인데 골키퍼와 센터백은 짧게 가능 빌드업을 선택하는 엇박자가 나오는 상황들을 반복해서 포착할 수 있었습니다. 명확하지 않은 전술의 결과입니다. 두 번째로는 우측 공간의 선수들을 몰아 넣어 경합을 통해 상대 진영에서 공을 소유하겠다는 목적을 가지고 골키퍼의 롱킥 처리가 잦았지만 그 지역의 영국 선수들의 신장은 경합에 적합하지 않습니다. 영국 우측의 경합 선수들로는 부카요 사카, 코비 마이누, 필 포든, 그리고 케인. 상대는 이를 파악하고 센터백 두 명, 풀백 그리고 세 명의 미드필더를 같은 공간에 배치하는 대응을 보여주는데 이때 케인을 제외하면 모두 180 cm 미만의 신장으로 180 후반에서 190 초반인 스페인 센터백들과 장신의 미드필더들과 경합을 해서 이겨내야 합니다. 그 결과 앞서 데이터를 확인했듯이 ***경합에 참여한 네 명의 영국 선수들은 경합 성공률은 처참합니다***. 적합하지 않은 선수 조건과 단순한 전술인 만큼 상대도 ***수비 숫자를 늘리며 쉽게 대처하게 됩니다.*** 

정리를 하자면 ***영국은 소극적인 압박과 정해진 틀에 갇혀 전반전을 주도하지 못했고***, 반대로 ***스페인은 상대의 노림수에 맞게 대응을 하고 유연성을 발휘해*** 상대가 유도한 측면에 선수를 더 배치함으로서 순각적인 수적 우위를 활용해 전번 전 내내 점유에서의 우위와 공격 주도권을 유지합니다. 그리고 데이터를 통해 얻은 두 질문에 답하자면 스페인은 설명했 던 것처럼 로드리의 포지션을 기점으로 측면에 숫자를 투자해 수적 우위를 가져갔고 영국은 미드필더 세 명 중 두 명이 우측으로 쏠리면서 숫자를 더했지만 이렇다 할 결과를 가져오지 못합니다.  그리고 숫자를 투자하지 않은 반대편의 공격이 효율적이었냐고 묻는다면, 두 팀 모두 한 쪽에 숫자를 집중시킨 후 의도적으로 상대를 끌어드려 반대편 공격 자원에게 공간을 만들어 주고 큰 전환 패스로 넘어가 윙어가 1대1을 시도하게 하는 그림이나 한 쪽 측면을 의도적으로 고립하는 장면은 없었고 센터백과 미드필더를 거쳐 단게적으로 전환을 해 숫자를 늘려 상대를 파훼하려는 시도가 주된 방식이었음을 확인했습니다. 

결론적으로 ***전반전은 스페인의 전술적 완승***이었고 후반전에 영국이 어떤 변화를 가져와 반전을 꾀할지에 집중하면서 후반전을 분석하겠습니다. 

다음 편에서 이어서. 
