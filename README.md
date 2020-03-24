# All NBA Team Machine Learning Project
## Introduction
This project outlines my steps taken to produce a KNN Model to predict what the All-NBA Teams would be.  Because most All-NBA Players are also All-Stars, I pulled data from basketball-reference.com using every All-Star and/or All-NBA player's season starting from the 1979-1980 Season.  There were 956 observations in total.  I then built a KNN Model from this dataset and used it to predict the All-NBA Teams from this past years All-Stars given their stats at the time of the All-Star Break (~February 15th, 2019).  

Below are all of the variables that were collected when pulling the data.  Not all of these variables will be used in the machine learning model.

| Box Score Stats  |  Team Stats         |  Shooting Stats          |  Advanced Stats       | Selections          |
| -------------    | ------------------- | ------------------------ | --------------------- | ------------------- |
| G                | Team Wins           |   FG%                    |   WS                  |   All-Star          |
| MPG              | Overall Seed        |   3P%                    |   VORP                |   All-NBA           |
| PPG              |                     |   FT%                    |   BPM                 |                     |
| TRB              |
| AST              |
| STL              |
| BLK              |

G - Games Played

MPG - Minutes per Game

PPG - Points per Game

TRB - Total Rebounds per Game

AST - Assists per Game

STL - Steals per Game

BLK - Blocks per Game


FG% - Field Goal Percentage of all shots taken

3P% - 3 Point Percentage

FT% - Free Throw Percentage


WS - Win Shares

VORP - Value over Replacement Player

BPM - Box Plus Minus


All-Star - A 0 represents that the player didn't make the All-Star Team, a 1 represents that they did

All-NBA - A 0 represents that the player didn't make the All-NBA Team, a 1 represents that they did

------------------------------------------------------------------------------------------------------------------------------------------
## Exploratory Data Analysis
Here are a series of scatterplots & histograms to get a sense of the distributions of these variables.  Of the variables collected, Shooting Stats will be removed and not shown here in this analysis because of the variability & inconsistency of using them to assess Player Value.  

![PPGplot](https://user-images.githubusercontent.com/16946556/64451250-a4342d00-d098-11e9-9bca-8d971425bbcc.png)
------------------------------------------------------------------------------------------------------------------------------------------

![VORPplot](https://user-images.githubusercontent.com/16946556/64449333-7d73f780-d094-11e9-8b6a-e854a003b828.png)
------------------------------------------------------------------------------------------------------------------------------------------

![WSxPPGplot](https://user-images.githubusercontent.com/16946556/64449372-9086c780-d094-11e9-8f2c-a2bd018fe49f.png)
------------------------------------------------------------------------------------------------------------------------------------------

![VORPxWSplot](https://user-images.githubusercontent.com/16946556/64449381-967ca880-d094-11e9-95c9-5ae6b8bc3714.png)

We can clearly see that VORP vs WS gives us the best visualization when trying to separate All-NBA and All-Star players.

------------------------------------------------------------------------------------------------------------------------------------------

![BPMplot](https://user-images.githubusercontent.com/16946556/64814117-b6f6a800-d557-11e9-8743-c10733f3cd1f.png)


------------------------------------------------------------------------------------------------------------------------------------------

![PPGhist](https://user-images.githubusercontent.com/16946556/64449384-9aa8c600-d094-11e9-936f-5ad4f48de43a.png)
------------------------------------------------------------------------------------------------------------------------------------------

![VORPhist](https://user-images.githubusercontent.com/16946556/64449386-9da3b680-d094-11e9-8a15-24d23d00f8a2.png)
------------------------------------------------------------------------------------------------------------------------------------------

![WShist](https://user-images.githubusercontent.com/16946556/64449389-a0061080-d094-11e9-83e4-699196c6571c.png)
------------------------------------------------------------------------------------------------------------------------------------------

![Winshist](https://user-images.githubusercontent.com/16946556/64449396-a1cfd400-d094-11e9-9ea4-30c3e9c4c427.png)
------------------------------------------------------------------------------------------------------------------------------------------

![BPMhist](https://user-images.githubusercontent.com/16946556/64814123-b9590200-d557-11e9-8d7c-3297a6b55426.png)

The histograms help show that All-NBA players tend to do everything better while also getting more wins.  Outside knowledge tells us that Sports Media also tends to favor voting for players who are playing on winning teams vs teams that are performing poorly, so we should make sure that Team Wins & Overall Seed are left in the Final Model.  

------------------------------------------------------------------------------------------------------------------------------------------

**Correlation Plot**

![nbacorrplot 2](https://user-images.githubusercontent.com/16946556/64814019-7f87fb80-d557-11e9-84f0-f7136972134e.png)


Here is a correlation matrix of the some of the final features to be selected for the model. Team Wins & Overall Seed have a high correlation with each other, as well Total Rebounds & Blocks.  This is totally normal, better teams get more wins and obviously a higher overall seed in their conference, and taller players typically get more rebounds and likely get more blocks as well.  There's an argument to be made that not all 4 of these features need to be included if they kind of overlap with each other, but I believe they're important dimensions to distinguish NBA players and should be left in the model.  

I decided to not use BPM in the final model because it has an extremely high correlation with both VORP and WS.  As shown in the scatterplot, VORP and WS are easily our best indicators of what separates the All-NBA players from the All-Star players.  Leaving BPM in would give us a lot of overlap and is simply not necessary.

Below is a list of the final variables to be used in the KNN Model.  

| Box Score Stats  |  Team Stats         | Advanced Stats       | Selections          |
| -------------    | ------------------- | ---------------------| ------------------- |
| PPG              | Team Wins           |  WS                  |   All-Star          |
| TRB              | Overall Seed        |  VORP                |   All-NBA           |
| AST              |                     | 
| STL              |
| BLK              |
 
------------------------------------------------------------------------------------------------------------------------------------------

## Modeling Building

The dataset was split into a 70% training data / 30% testing data split.  K Fold Cross Validation was performed (3 folds, repeated 10 times) to make sure the splits were as balanced as possible.  I also added a preprocessing step by scaling all data to Z-scores to ensure all features were equal in weight.

------------------------------------------------------------------------------------------------------------------------------------------
**ROC Curve**

![ROC Curve All-NBA](https://user-images.githubusercontent.com/16946556/64449408-aac0a580-d094-11e9-8a02-463cec5b2221.png)

I then printed out a simple ROC Curve, which showed that the best K would be equal to 31 neighbors.

------------------------------------------------------------------------------------------------------------------------------------------
**Confusion Matrix**

![ConfusionMatrix](https://user-images.githubusercontent.com/16946556/64449401-a85e4b80-d094-11e9-9fad-f94418b5adda.png)

Here is the Confusion Matrix from the final model.  I wanted to produce a graphical plot for it rather than just a text printout in R but didn't know how, so I googled code on how to produce one and found this which worked out well.  Of the 287 observations in the test set, the model correctly predicted 245 of them, with an acccuracy of 85.4% as shown above.  While not perfect this helps show that the model is reasonably accurate and will be a good indicator to help us figure out what the actual All-NBA Teams might be. 

------------------------------------------------------------------------------------------------------------------------------------------
## Results

Only 2 Guards, 2 Forwards, and 1 Center can make each of the All-NBA Teams. Sports Media votes on the All-NBA Team positions, so there is a human element to this analysis that cannot be accounted for (a reporter can easily have personal bias when voting).  The idea behind this categorical variable problem is the best players in the league (the ones most likely to make an All-NBA 1st Team) should have values of 1.00, and the farther away you get from 1.00 the less likely you are to be an All-NBA player.

I took the stats of this year's All-Stars at the All-Star break, and scaled them up to an 82 game season depending on how many games they played up until that point.

Final Model Predictions

| Position      | 1st  Team     |   2nd Team    |   3rd  Team   |
| ------------- | ------------- | ------------- | ------------- |
| Guard         | James Harden  (.97)            | Damian Lillard  (.74) | Russell Westbrook  (.68) |
| Guard         | Stephen Curry  (.87)           | Kyrie Irving  (.77)   | Kyle Lowry  (.45)        |
| Forward       | Kevin Durant*  (1.00)          | Paul George*  (1.00)  | Anthony Davis (.74)      |
| Forward       | Giannis Antetokounmpo*  (1.00) | Kawhi Leonard*  (1.00)| LeBron James  (.68)      |  
| Center        | Nikola Jokic  (1.00)           | Rudy Gobert  (1.00)   | Joel Embiid  (.90)       | 


------------------------------------------------------------------------------------------------------------------------------------------
The Actual All-NBA Teams

| 1st  Team     |   2nd Team    |   3rd  Team   |
| ------------- | ------------- | ------------- |
| James Harden           | Damian Lillard | Russell Westbrook |
| Stephen Curry          | Kyrie Irving   | Kemba Walker      |
| Paul George            | Kevin Durant   | Blake Griffin     |
| Giannis Antetokounmpo  | Kawhi Leonard  | LeBron James      |  
| Nikola Jokic           | Joel Embiid    | Rudy Gobert       | 

My KNN Model predicted 13 of the 15 players to make an All-NBA Team, which is 86.67% accurate and close to the 85.4% accuracy shown in the Classification Matrix.  Of these 13 players, 9 were correctly placed into the All-NBA Team that they ended up getting selected into at the end of the Season.  

The insights developed from this project are that we can more or less predict All-NBA Teams at the All-Star Break, which is roughly 2 months before the end of the season.  Team Wins & Overall Seed play a huge factor in placement.  Total Rebounds also seem to be weighted a little bit too high.  3 of the top 9 highest ranking players in the model are Centers.  Of all the box score stats, rebounds are easily the most misleading statistic in terms of using it to assess a player's value.  A possible improvement to the model would be to modify the TRB statistic to decrease its importance, or to remove it entirely.

------------------------------------------------------------------------------------------------------------------------------------------
2020 Update

I re-ran this same model using 2020 NBA All Star Break Data.  I made a few tweaks like excluding BPM and VORP to avoid multi-colinearity, but overall the second run seems just as promising as the first (although the actual results aren't available yet).  Below are my predicted top 15 list for who is going to make the All-NBA Team in the 2019-2020 NBA Season.

| Position      | 1st  Team     |   2nd Team    |   3rd  Team   |
| ------------- | ------------- | ------------- | ------------- |
| Guard         | James Harden  (.97)           | Damian Lillard  (.74) | Russell Westbrook  (.63) |
| Guard         | Luka Doncic  (.88)            | Jimmy Butler  (.77)   | Ben Simmons  (.56)       |
| Forward       | Lebron James  (1.00)          | Anthony Davis  (.95)  | Bam Adebayo (.51)        |
| Forward       | Giannis Antetokounmpo  (1.00) | Kawhi Leonard  (.88)  | Khris Middleton  (.44)   |  
| Center        | Nikola Jokic  (1.00)          | Rudy Gobert  (.65)    | Joel Embiid  (.63)       | 
