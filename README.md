  # Final project: Analyzing the pitcher performance through years

## This file includes:



### Data file:
- [2023 MLB pitching raw data](https://github.com/ollill0823/102.UIUC_MS_CS-412-Introduction-to-Data-Mining/tree/main/Report) Raw data from [Baseball Savant](https://baseballsavant.mlb.com/statcast_search)


### Jupyter notebook
- [Code here](https://github.com/ollill0823/102.UIUC_MS_CS-412-Introduction-to-Data-Mining/blob/main/Report/Final_proeject_1205.ipynb)

### Introduction
- Major League Baseball (MLB) stands as a globally esteemed and iconic institution, celebrated for its capacity to draw talent from diverse corners of the world. Anticipating game outcomes through individual player analysis provides invaluable insights, empowering teams with informed references for selecting their starting players and refining strategic gameplay tactics.

### Motivation:
We aim to delve into baseball games, assessing the likelihood of our favored player securing victory. Leveraging data mining expertise, we can explore our areas of interest and assimilate the knowledge acquired in our classes to effectively implement it into our project.

### Empirical results:
#### Data Preprocessing: 
1. **Eliminate Missing Values:** Upon reviewing the dataset, it came to our attention that certain features contain missing values. Further examination revealed that the feature with the highest number of missing values amounts to approximately 500 out of 226,000 data points. Consequently, we have chosen to remove these instances from the dataset.
2.	**Enhance Feature Representation:** The existing "Pitch_type" feature encompasses 
various pitching postures, yet they are currently consolidated under a single feature. Recognizing the significance of pitch type for pitchers and individual pitches, we have opted to broaden this representation by transforming the singular "Pitch_type" feature into multiple categorical features. Leveraging label encoding, we expand and organize the distinct pitch types based on their individual names.

![Figure 1](https://github.com/ollill0823/102.UIUC_MS_CS-412-Introduction-to-Data-Mining/blob/main/Pictures/Figure1.png)

4.	Enhance Feature Representation: The existing "Pitch_type" feature encompasses 
various pitching postures, yet they are currently consolidated under a single feature. Recognizing the significance of pitch type for pitchers and individual pitches, we have opted to broaden this representation by transforming the singular "Pitch_type" feature into multiple categorical features. Leveraging label encoding, we expand and organize the distinct pitch types based on their individual names.

![Figure 2](https://github.com/ollill0823/102.UIUC_MS_CS-412-Introduction-to-Data-Mining/blob/main/Pictures/Figure2.png)

6.	Aggregate and Derive Predictive Features:
   *	In the pursuit of generating a comprehensive predictive model, we undertake the grouping and calculation of diverse features. Features that encapsulate the pitcher's overall performance in each game, such as "spin_rate" and "release_speed", are subject to a mean calculation. This involves averaging the data across individual games for each respective feature.
   *	In the case of features like "post_away_score" and "post_home_score," which directly influence the final points of each game, we seek the maximum value for these attributes. This maximal value indicates the final score that two teams achieve in each game, and it is pivotal in computing the point differential between the two teams. The resulting differentials serve as crucial inputs for the final prediction, enhancing our ability to gauge and anticipate outcomes based on game dynamics.
   *	In assessing the "reward" feature, we aim to aggregate the points a pitcher accrues based on the reward table. Summing up these points provides an overall measure of the pitcher's performance. A higher total indicates superior pitching qualities, offering a quantitative representation of the pitcher's effectiveness.
5.	Define Target Variable (y):
Our target variable is the score difference in each game, reflecting the outcome of the match. Building upon the results obtained during the aforementioned data preprocessing, we integrate information about the team the pitcher is representing and the features "post_away_score" and "post_home_score" to compute the points gained or lost by each pitcher in a game. For pitchers aligned with the home team, the calculation involves subtracting "post_away_score" from "post_home_score." Conversely, for pitchers associated with the away team, the calculation becomes "post_away_score" minus "post_home_score." Utilizing the derived results, we categorize a winning scenario as "1" and a losing scenario as "0." This categorization forms the basis of our target variable for further analysis.
6.	Implement Random Data Split for Training and Testing: To establish distinct training and testing datasets, we employ a random split method. Given the potential involvement of multiple pitchers in a single game, our dataset comprises a total of 2578 records for various games. In the case of the "score difference" method, we utilize the game-level data for the training and testing processes. Conversely, for the "reward" method, we employ data at the granularity of each ball for the training and testing procedures. This involves allocating 90% of the randomized datasets for training purposes, with the remaining 10% designated for testing. To avoid potential errors during the data split, we exclude grouping parameters such as "game_date" and "pitcher." Furthermore, we categorize the datasets into two types: one dedicated to predicting score differences and the other focused on predicting reward system outcomes. This segregation allows for targeted analysis and model training based on the specific prediction goals, enhancing the precision of our predictive models.

#### Regression analysis: 
We use several regression models to predict the results. The models we chose are:
   -	Linear Regression
   -	LASSO Regression
   -	SVR
   -	Random Forest Regressor
   -	KNN Regressor
   -	MLP Regressor (neural network)
   -	Decision Tree Regressor
   -	Gradient Boosting Regressor

We utilized GridSearchCV to fine-tune our hyperparameters, systematically exploring all possible combinations specified in a dictionary. This process evaluates the model's performance for each combination through Cross-Validation, providing accuracy or loss metrics. Consequently, employing this function enables us to pinpoint the hyperparameter configuration that exhibits optimal performance. In the context of the "reward" system, the Linear Regression model demonstrated superior performance, as evidenced by the smallest Mean Square Error among the models considered. Conversely, in the realm of the "score difference” system method, the MLP Regressor (neural network) emerged as the top performer, showcasing the smallest Mean Square Error in comparison to other models.

![Figure 3](https://github.com/ollill0823/102.UIUC_MS_CS-412-Introduction-to-Data-Mining/blob/main/Pictures/Figure3.png)

In the final phase, we present separate visualizations for the results obtained from the two systems. The graphical representation allows us to discern that the overall performance of the "reward" system correlates more closely with the actual data compared to the "score difference" system. Notably, the data points of the "score difference" system cluster around zero, indicating a lack of distinct clarity in illustrating the relationship between each feature and the target variable (y). Conversely, the data points of the "reward" system are positioned in closer proximity to the actual data. This alignment implies that the "reward" system method is more effective in elucidating the attributes of different features, providing a clearer representation of their impact on the target variable.

![Figure 4 and Figure](https://github.com/ollill0823/102.UIUC_MS_CS-412-Introduction-to-Data-Mining/blob/main/Pictures/Figure45.png)
### Conclusion and discussions:
When assessing system performances, it becomes evident that the "reward" system outperforms the "score difference" system. For the "score difference" system, the standard deviation of the actual target value (y) is 3.08, while the standard deviation for the predicted target value is 0.64. Notably, there is almost a fivefold difference between these two values. In contrast, analyzing the "reward" system reveals a more consistent performance. The standard deviation of the actual value is 8.28, and the standard deviation of the predicted target value is 3.01. In this case, the difference between the two is approximately 2.7 times. This suggests that the "reward" system exhibits a more stable and reliable predictive performance compared to the "score difference" system.There are several reasons that may contribute to the difference between the performance.

We have discussed several reasons leading to the results:
-	Our initial focus centers on the comprehensive pitching performance in each game. To achieve this, we calculate the average values for each feature across the entirety of our datasets, extracting the desired parameters. It's imperative to note that outliers, such as instances where pitching speed is exceptionally low or the pitching position deviates significantly from the norm, are identified and accounted for during this process. Since the outliers will be normalized, the outcomes will not be ideal if we use the average data of each feature. 
-	It's imperative to recognize that the outcome of a game is not solely determined by the pitcher. Factors such as the performance of batters and fielders play pivotal roles in shaping the final result. In our datasets, instances where fielder's inadvertently lose a ball contribute to the pitcher's record, though it may not necessarily be attributed to the pitcher's performance.Another noteworthy factor is the impact of the catcher's performance. A proficient catcher can diminish the likelihood of a batter hitting a ball, subsequently improving the Fielding Percentage and overall team performance. This underlines the interconnectedness of various team elements, emphasizing the need to consider a holistic approach when assessing individual player contributions and their impact on the game's outcome.
-	It's crucial to acknowledge that the outcome of each pitched ball by the pitcher is not independent. Throughout the course of the game, the player's physical strength gradually diminishes, leading to a potential decline in performance. As a result, the data quality may exhibit a deterioration, particularly as the game progresses towards its conclusion. This non-independence factor underscores the importance of accounting for the evolving physical condition of the player when interpreting performance data, particularly in the latter stages of a game.
From the preceding discussion, it becomes evident that the available datasets for the pitcher alone may not provide a sufficiently robust foundation for accurate predictions. The performance and ultimate outcome of a game are intricately tied to the collective efforts of the entire team, extending beyond the contributions of the pitcher alone. In the context of the "score difference," the normalization of outliers results in a more centralized dataset, potentially leading to less optimal outcomes. Conversely, the "reward" system, with its consideration of multiple aspects and detailed calculations on various outcomes, holds promise for generating more accurate results. To further enhance predictive accuracy, the inclusion of additional parameters, such as the performance of batters and pitchers, or the strategic decisions made by the coach for each game, could significantly contribute to refining and improving the precision of the "reward" system predictions.
       
### Summary file
- [See pdf file here](https://github.com/ollill0823/102.UIUC_MS_CS-412-Introduction-to-Data-Mining/blob/main/Final%20Project%20Report.pdf)


### References:
- [A Method of Analyzing a Baseball Pitcher's Performance Based on Statistical Data Mining](https://www.researchgate.net/publication/283722473_A_Method_of_Analyzing_a_Baseball_Pitcher's_Performance_Based_on_Statistical_Data_Mining) Ezra Sidran Nov. 2015
