# All-NBA-Team-Machine-Learning-Project
sdfdsfsff
![VORPplot](https://user-images.githubusercontent.com/16946556/64449333-7d73f780-d094-11e9-8b6a-e854a003b828.png)


![VORPxWSplot](https://user-images.githubusercontent.com/16946556/64449381-967ca880-d094-11e9-95c9-5ae6b8bc3714.png)

![WSxPPGplot](https://user-images.githubusercontent.com/16946556/64449372-9086c780-d094-11e9-8f2c-a2bd018fe49f.png)

![PPGhist](https://user-images.githubusercontent.com/16946556/64449384-9aa8c600-d094-11e9-936f-5ad4f48de43a.png)

![VORPhist](https://user-images.githubusercontent.com/16946556/64449386-9da3b680-d094-11e9-8a15-24d23d00f8a2.png)

![WShist](https://user-images.githubusercontent.com/16946556/64449389-a0061080-d094-11e9-83e4-699196c6571c.png)

![Winshist](https://user-images.githubusercontent.com/16946556/64449396-a1cfd400-d094-11e9-9ea4-30c3e9c4c427.png)

![PPGplot](https://user-images.githubusercontent.com/16946556/64449398-a4322e00-d094-11e9-81e5-12b8a8e77a52.png)

![ConfusionMatrix](https://user-images.githubusercontent.com/16946556/64449401-a85e4b80-d094-11e9-9fad-f94418b5adda.png)

![ROC Curve All-NBA](https://user-images.githubusercontent.com/16946556/64449408-aac0a580-d094-11e9-8a02-463cec5b2221.png)
------------------------------------------------------------------------------------------------------------------------------------------

Only 2 Guards, 2 Forwards, and 1 Center can make each of the All-NBA Teams.  This means that even if the best 5 players in the NBA are forwards that only 2 of them can be featured on the premiere 1st Team.  Sports Media votes on the All-NBA Team positions, so there is a human element to this analysis that cannot be accounted for (a reporter can easily be biased when voting).


| Position      | 1st  Team     |   2nd Team    |   3rd  Team   |
| ------------- | ------------- | ------------- | ------------- |
| Guard         | James Harden  (.97)            | Damian Lillard  (.74) | Russell Westbrook  (.65) |
| Guard         | Stephen Curry  (.84)           | Kyrie Irving  (.68)   | Kyle Lowry  (.42)        |
| Forward       | Kevin Durant*  (1.00)          | Paul George*  (1.00)  | LaMarcus Alridge  (.55)  |
| Forward       | Giannis Antetokounmpo  (1.00)  | Kawhi Leonard  (.87)  | LeBron James  (.52)      |  
| Center        | Nikola Jokic  (1.00)           | Rudy Gobert  (1.00)   | Joel Embiid  (.94)       | 


Above is the final KNN Model with the predicted All-NBA probability next to the players names.  Below are the actual results


| 1st  Team     |   2nd Team    |   3rd  Team   |
| ------------- | ------------- | ------------- |
| James Harden           | Damian Lillard | Russell Westbrook |
| Stephen Curry          | Kyrie Irving   | Kemba Walker      |
| Paul George            | Kevin Durant   | Blake Griffin     |
| Giannis Antetokounmpo  | Kawhi Leonard  | LeBron James      |  
| Nikola Jokic           | Joel Embiid    | Rudy Gobert       | 
