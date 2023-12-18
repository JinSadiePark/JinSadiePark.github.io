---
layout: post
title:  "NBA Status"
author: "Jinkyung Park"
description: "This is a project to Explore NBA Stats for Insights into Player Performances."
image: "https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/basketball_image%20Medium.png?raw=true"
---

## Celebrating Hoops Excellence: Unveiling Insights from NBA
This stats collection offers a fascinating look into player performances, from top scorers and shooting accuracy to team dynamics and defensive skills. Join me in exploring the numbers, uncovering standout players, and discovering the stories behind their on-court success. Let's break down the stats and find the hidden gems that make each player's journey in the NBA special.
<br></br>

* Which team has the highest average efficiency?<br>
* Who's leading in total points, and are there any surprising players in the top 5?<br>
* Which player has the most accurate field goal percentage among the top scorers?<br>
* Who are the most reliable free throw shooters?

<br>

To collect the data, I used the API of the NBA website.

    test_url = 'https://stats.nba.com/stats/leagueLeaders?LeagueID=00&PerMode=Totals&Scope=S&Season=2021-22&SeasonType=Regular%20Season&StatCategory=PTS'
    r = requests.get(url = test_url).json()
    table_headers = r['resultSet']['headers']
                
    df1 = pd.DataFrame(r['resultSet']['rowSet'], columns= table_headers)
    df2 = pd.DataFrame({'Year' : ['2021-22' for i in range(len(df1))],
                        'Season' : ['Regular%20Season' for i in range(len(df1))]})
    df3 = pd.concat([df2, df1], axis = 1)

    df_col = ['Year', 'Season_type'] + table_headers

    headers = {
    'Accept': '*/*',
    'Accept-Encoding': 'gzip, deflate, br',
    'Accept-Language': 'en-US,en;q=0.9,ko;q=0.8',
    'Connection': 'keep-alive',
    'Host': 'stats.nba.com',
    'Origin': 'https://www.nba.com',
    'Referer': 'https://www.nba.com/',
    'Sec-Ch-Ua': '"Google Chrome";v="117", "Not;A=Brand";v="8", "Chromium";v="117"',
    'Sec-Ch-Ua-Mobile': '?0',
    'Sec-Ch-Ua-Platform': '"macOS"',
    'Sec-Fetch-Dest': 'empty',
    'Sec-Fetch-Mode': 'cors',
    'Sec-Fetch-Site': 'same-site',
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36'}


    df = pd.DataFrame(columns = df_col)
    season_types = ['Regular%20Season', 'Playoffs']
    years = ['2021-22', '2022-23', '2023-24']

    for y in years:
      for s in season_types:
        api_url = 'https://stats.nba.com/stats/leagueLeaders?LeagueID=00&PerMode=Totals&Scope=S&Season='+y+'&SeasonType='+s+'&StatCategory=PTS'
        r = requests.get(url = api_url, headers = headers).json()
        df1 = pd.DataFrame(r['resultSet']['rowSet'], columns= table_headers)
        df2 = pd.DataFrame({'Year' : [y for i in range(len(df1))],
                                        'Season_type' : [s for i in range(len(df1))]})
        df3 = pd.concat([df2, df1], axis = 1)
        df = pd.concat([df, df3], axis = 0)

        lag = np.random.uniform(low = 5, high = 40)
        time.sleep(lag)

    df.to_csv('nba_player_data.csv', index = False)

                
<br>                

From the data, I was able to observe the graph related to the questions above.
Here's some EDA that I explored

### The Team That Has the Highest Average Efficiency

<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/team_efficiency_plot.png?raw=true" alt="Resized Image" width="600" height="400">

<br>

### The Top 5 NBA Players in Total Points

<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/Screenshot%202023-12-17%20at%206.02.13%20PM.png?raw=true" alt="Resized Image" width="600" height="400">
<br>

### The Most Accurate Field Goal Percentage Among the Top Scorers

<br>

    sorted_data = df.sort_values(by='PTS', ascending=False)

    # Select the top scorer
    top_scorer = sorted_data.iloc[0]['PLAYER']

    # Find the player with the most accurate field goal percentage among the top scorers
    most_accurate_fg_percentage_player = sorted_data.iloc[0]['PLAYER']
    fg_percentage = sorted_data.iloc[0]['FG_PCT']

<br>
When I ran the code above, I found that the player with the most accurate field goal percentage among the top scorers is Jayson Tatum with 46.60% field goal percentage.
<br>

### The Most Accurate Field Goal Percentage Among the Top Scorers

<br>

    import numpy as np

    df['STL_TOV'] = np.where(df['TOV'] == 0, np.inf, df['STL'] / df['TOV'])
    df['BLK_TOV'] = np.where(df['TOV'] == 0, np.inf, df['BLK'] / df['TOV'])

    df = df.replace([np.inf, -np.inf], np.nan).dropna(subset=['STL_TOV', 'BLK_TOV'])

    high_stl_tov_players = df.sort_values(by='STL_TOV', ascending=False).head(5)[['PLAYER', 'STL_TOV']]
    high_blk_tov_players = df.sort_values(by='BLK_TOV', ascending=False).head(5)[['PLAYER', 'BLK_TOV']]

<br>

<img src="https://github.com/JinSadiePark/JinSadiePark.github.io/blob/main/assets/images/Screenshot%202023-12-17%20at%206.52.10%20PM.png?raw=true" alt="Resized Image" width="600" height="400">

Keita Bates-Diop and John Butler Jr. stand out in both steals-to-turnover and blocks-to-turnover ratios, showcasing a well-rounded defensive impact with a focus on generating steals and blocks while minimizing turnovers.
<br>

## Conclusion

The NBA player dataset analysis highlights Jayson Tatum as a top scorer with efficient field goal shooting. Defensive stalwarts like Keita Bates-Diop and John Butler Jr. exhibit a rare blend of steals and shot-blocking. Versatile players, including Robert Covington and others, contribute to robust defensive strategies. The findings emphasize the significance of balanced skill sets, showcasing players' roles in both individual and team success.
