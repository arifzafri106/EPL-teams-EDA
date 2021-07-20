# EPL Teams EDA
The project is to perform EDA on EPL teams during the 2020/2021 season. Based on that we can find the different statistics of each football team and see which stats affects the performance of each team.

![Logo](/images/premierleague.png)  

## Datasets Used for this project
[Football Teams Dataset 2020/2021](https://www.kaggle.com/ankurkaiser/football-dataset-20202021) - This dataset shows the Football Dataset for teams in the Top 5 Leagues for the 2020/21 season such as Goals, Shots pg etc.  
[European Football Database](https://www.kaggle.com/groleo/european-football-database) - This database contains all the matches results since the season 2005-2006 for 21 different league in 11 different countries, comes as sqlite file.

## Loading Dataset and Manipulating Data
First, we have to load the dataset using the European Football Database which is an sqlite type file. So, the file needs to be converted into a dataframe by using the following code.
```
import sqlite3
import pandas as pd


conn = sqlite3.connect('european_database.sqlite')

query = """
SELECT 
    m.*, d.name, d.country
FROM matchs m 
JOIN divisions d ON d.division == m.Div
"""

df = (
    pd.read_sql_query(query, conn)
    .assign(Date = lambda x: pd.to_datetime(x.Date))
)
```
Sort out the EPL Teams results from the database
![My image](https://github.com/arifzafri106/EPL-teams-EDA/blob/main/images/df.head.PNG)

Then to sort out the results for only the 2020/2021 season for EPL
![My image](https://github.com/arifzafri106/EPL-teams-EDA/blob/main/images/epl2021.PNG)  


From there we are able to manipulate and clean the data to determine the Home Wins, Away Wins and Draws of each team in the EPL and then able to determine the Win Percentage of all teams.
![image](https://user-images.githubusercontent.com/84439768/126381678-b1157ea7-d32f-4114-a489-f5ca8735e748.png)  

After that we can import the dataset from the Football Teams Dataset 2020/2021 using the following code.
![image](https://user-images.githubusercontent.com/84439768/126381883-2fd1d533-8777-4b66-9baf-4930762c23e7.png)

From there we sort out the EPL teams only and clean the data to be used to merge with previous dataframe.
![image](https://user-images.githubusercontent.com/84439768/126382134-6b21d4e7-d70e-4def-bab6-a88a8cbc90f0.png)
![image](https://user-images.githubusercontent.com/84439768/126382229-0711497a-c7aa-4f32-80e1-8f2d7dcb80d8.png)


## EDA
Now the datasets have been merged, manipulated and cleaned, we are able to perform EDA on the dataframes such as to determine the team with the most goals during the season 
```
goals_scored = EPL_merged[['Team_x','Goals']].sort_values('Goals', ascending=False).head()
goals_scored
```
Using seaborn we would be able to put the data in a clearer view as a table
![image](https://user-images.githubusercontent.com/84439768/126382691-1b1c3611-e204-4a34-89eb-d702359b6dc8.png)

![image](https://user-images.githubusercontent.com/84439768/126382924-7525a0d4-2df4-48a1-bba8-8d81b9b2ce15.png)








