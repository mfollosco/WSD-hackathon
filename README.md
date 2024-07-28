# WSD-hackathon
## Introduction
Hello we are team MILT (Maddie, Irene, Lindsey,  and Tiffany) and we are rising junior Computer Science students at Santa Clara University. Participating in the Women in Sports Data Hackathon was a really cool learning experience as most of our team is new to baseball and data analysis and Python, and we are excited to share our product with you!

## Purpose and Motivation 
We wanted to take advantage of the detailed data about ball path, velocity, and launch angle we got with this data. Initially the idea was to analyze an at bat and correlate that with the behavior of a specific player, but since there was no guarantee of linking those factors together amongst the files, we decided to execute this vision more generally. Since this data was given based on a series, we wanted to create a tool that would best prepare a team for an upcoming series against a team based on data from that team’s previous series. 

## Solution
We present our Series Prediction Tool, SPT by MILT enterprises. This tool will provide predictions using a random forest model. It will provide information that is favorable to players, especially the pitcher.
Furthermore, we also present several graphs to visualize the relationship between the variables we use to give players and coaches alike more insights into what factors seem to have the biggest impact on a play’s result along with trends in the data.

## Context for how and when to use your project
Our project is meant to be used when teams are preparing for an upcoming series with a particular team. Data from the last time they encountered the opposing team or from when the opposing team most recently played can be analyzed with our tool.

## Difficulties & challenges faced during the design/development process
One of the major challenges we faced while trying to develop a model was struggling to find strong correlations in the data. Initially, we wanted to predict the result (strike, ball, or hit into play) of a play based on factors such as the pitch type, speed, and spin. However, our model had relatively low accuracy at about 47%, and, after making graphs to visualize the relationship between these different features and the result, we realized that the low accuracy was because there was not a strong correlation in the data. As a result, we tried to run a correlation analysis on all of the variables we were given, though we found that most of the factors with a high correlation coefficient were fields that were inherently connected (such as velocity and acceleration) rather than factors that would be useful for coaches or players. Similarly, we were working with a very limited set of variables, so many of the other features that may impact the result of the play (player position, which teams/players were pitching and hitting, etc.) couldn't be factored into our analysis.

Furthermore, we would like better quality data with more fields filled to have a larger sample size while performing data analysis. For example, since a lot of our analysis depended on pitch type, we had to filter out the data where pitch type wasn’t included, decreasing our sample size from the 1,200 files we were searching through to just 152 rows with pitch type, pitch speed, and pitch result. While we did consider using techniques like imputation to fill in the missing data, we ultimately decided to just filter out the data since the fact that the overwhelming majority of our rows had missing data meant that the imputed data would not be accurate.

## Next steps 
We believe with more data samples with the non-empty fields we need for our analysis we could improve our model accuracy. Moreover, we believe our product could become more advanced and tailored to specific player trends and behaviors assuming we had access to anonymized data.

## Components
### Pitch Tracking
We visualize relationships between different pitch data features (pitch type, initial spin, initial speed, result, etc.) using various graphs, such as heatmaps and histograms, which are shown on the website.

### Hit Classification
We used the launch angle and exit velocity data for every pitch that had a ‘Hit into Play’ result and a nonempty pitch type and pitch speed result. The angle and exit velocity information gave us insight on different hit types. Once we sorted hit type information from each pitch, we analyzed the relationship of each type to a certain type of pitch and pitch speed to determine the best outcome in the pitcher’s favor. Power hits, fly balls, and hard hit line drives were deemed ‘bad’ for the pitcher while other hit types such as light ground balls and pop ups were deemed ‘good’. We then trained a random forest model to make a prediction/recommendation of what pitches to avoid or throw. With more data we believe the model would be more accurate and provide a helpful analysis for the pitcher to prepare for a series against a certain team. Conversely, a batter could look at such an analysis when studying a certain pitcher and know what hit types did or did not fair well against certain pitches. At the moment the measurement for “success” of the hit was the fact that the result itself was ‘Hit into Play’, however we know we could improve it and would have liked to use the final distance of the ball to more clearly define a successful hit. It was a bit of a challenge to clearly determine where the ball ended up when we were given the whole path of the ball, including after a play was made. Furthermore, the current data heavily favors pitches that are good for the pitcher, so having a larger sample set could help our model encompass a larger range of scenarios as well. 

Sources:
- https://www.mlb.com/news/what-you-need-to-know-about-statcast-bat-tracking
- https://www.mlb.com/glossary/statcast/launch-angle

### Correlation:
After making a program to assemble all of the data in an easy-to-process pandas dataframe, we ran an analysis on most of the factors provided to us to see which factors were most strongly correlated, including (but not limited to):
- Pitch eventId/type/result/speed/spin
- Hit eventId/speed/spin/start angle
- Event type
- TeamId
- PersonId
- EventId
- Pitch start time/position/velocity/acceleration
- Pitch end time/position/velocity/acceleration
- Swing start time/end time
- Bat head/handle start/end position/velocity/acceleration
- Hit type
- Hit grade

Pearson and spearman correlations were calculated between most given variables (all quantitative given variables with 2 unique outcomes were assigned boolean variables of 0 and 1), and we highlighted variables in an acceptable range (-0.7 > r > 0.7).
Two methods were used to calculate the correlations between the additional calculated variables and the given factors:
- Method 1 (enumeration): each non-quantitative factor is assigned a unique number on a scale of 1 through n (n being the number of possible outcomes) and pearson correlation coefficients are calculated. No solid conclusions resulted from this method as correlation coefficients were in an acceptable range (-0.7 > r > 0.7).
- Method 2 (boolean): each unique quantitative outcome is turned into its own factor, and the elements in each column are boolean values determining if each unique quantitative outcome applies or not. The relationship between the hit resulting in a fly ball and the hit grade had an acceptable negative correlation coefficient of r = -0.736379.

### Display/HTML:
We compiled all of our findings into an easily accessible html file for coaches and staff to be able to analyze their series predictions and analytics all in one place

### Model
We were able to train a model with a 87% accuracy to predict whether a pitch was favorable to the pitcher or not depending on pitch type and pitch speed.
We also allowed the the user (likely the pitcher) to input a pitch type and pitch speed and determine if the outcome is in their favor or not. In the future we would have a whole table output of results and percentages of favorability, rather than one result at a time (assuming the model trained on a larger sample size)




