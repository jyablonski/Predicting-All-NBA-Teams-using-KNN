# All-NBA-Team-Machine-Learning-Project
This project outlines my steps taken to produce a KNN Model to predict what the All-NBA Teams would be.  Because most All-NBA Players are also All-Stars, I pulled data from basketball-reference using every All-Star and/or All-NBA player's season.  There were 956 observations in total.  I then built a KNN Model from this dataset and used it to predict the All-NBA Teams from this past years All-Stars given  their stats at the time of the All-Star Break (~February 15th, 2019).  

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



![PPGplot](https://user-images.githubusercontent.com/16946556/64451250-a4342d00-d098-11e9-9bca-8d971425bbcc.png)
------------------------------------------------------------------------------------------------------------------------------------------

![VORPplot](https://user-images.githubusercontent.com/16946556/64449333-7d73f780-d094-11e9-8b6a-e854a003b828.png)
------------------------------------------------------------------------------------------------------------------------------------------

![WSxPPGplot](https://user-images.githubusercontent.com/16946556/64449372-9086c780-d094-11e9-8f2c-a2bd018fe49f.png)
------------------------------------------------------------------------------------------------------------------------------------------

![VORPxWSplot](https://user-images.githubusercontent.com/16946556/64449381-967ca880-d094-11e9-95c9-5ae6b8bc3714.png)
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

**Data partition**

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


Only 2 Guards, 2 Forwards, and 1 Center can make each of the All-NBA Teams. Sports Media votes on the All-NBA Team positions, so there is a human element to this analysis that cannot be accounted for (a reporter can easily be biased when voting).

Final Model

| Position      | 1st  Team     |   2nd Team    |   3rd  Team   |
| ------------- | ------------- | ------------- | ------------- |
| Guard         | James Harden  (.97)            | Damian Lillard  (.74) | Russell Westbrook  (.65) |
| Guard         | Stephen Curry  (.84)           | Kyrie Irving  (.68)   | Kyle Lowry  (.42)        |
| Forward       | Kevin Durant*  (1.00)          | Paul George*  (1.00)  | LaMarcus Alridge  (.55)  |
| Forward       | Giannis Antetokounmpo  (1.00)  | Kawhi Leonard  (.87)  | LeBron James  (.52)      |  
| Center        | Nikola Jokic  (1.00)           | Rudy Gobert  (1.00)   | Joel Embiid  (.94)       | 


------------------------------------------------------------------------------------------------------------------------------------------
The Actual All-NBA Teams

| 1st  Team     |   2nd Team    |   3rd  Team   |
| ------------- | ------------- | ------------- |
| James Harden           | Damian Lillard | Russell Westbrook |
| Stephen Curry          | Kyrie Irving   | Kemba Walker      |
| Paul George            | Kevin Durant   | Blake Griffin     |
| Giannis Antetokounmpo  | Kawhi Leonard  | LeBron James      |  
| Nikola Jokic           | Joel Embiid    | Rudy Gobert       | 
