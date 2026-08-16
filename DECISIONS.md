# Decision Log

## Assignment 2: Dataset
- **Dataset:** NFL Big Data Bowl 2021 `plays.csv`, from Kaggle.
- **Main variable of interest:** explosive play, coded `1` for a gain of 15+ yards and `0` otherwise. We chose this because explosive plays are one of the strongest indicators of offensive success and winning football, which makes the outcome both analytically meaningful and practically valuable to coaching staffs.
- **Key decision:** we framed the outcome as a binary so the same dataset could support probability, inference, and regression work later in the term. We also capped each categorical variable at three categories (for example, defenders in the box grouped as 6 or fewer vs. more than 6) to keep the analysis clean.

## Assignment 3: Descriptive Stats
- **Cleaning done:** we used Python to clean the data. A few values were combined into single categories, rows with missing data were deleted, and the game clock was converted into a single continuous number showing total elapsed game time in minutes.
- **Most common patterns:** first down is the most common down (expected, since each series starts on first down), most plays occur in regulation with few in overtime, and 11 personnel and light boxes (6 or fewer defenders) are the most common alignments.
- **Most surprising pattern:** both pre-snap home and visitor scores are right-skewed, meaning high scores are uncommon when plays are run. Yardline and absolute yardline are fairly evenly distributed, and few plays gained a large number of yards, which is what motivated the explosive-play analysis.

## Assignment 4: Probability
- **Distribution shapes:** across our six variables, four were right-skewed (skewness above 0.5), one was bimodal (game time, with clear peaks at the end of each half), and one was approximately normal (close mean and mode, very low skew).
- **Normal vs. empirical, and why:** because most variables were skewed or bimodal rather than normal, we relied on the empirical distribution from the data rather than assuming normality. The one approximately normal variable was the only case where the normal assumption reasonably held.
- **Key insight:** about 1 in 3 passing plays gain 8 or more yards, and offenses produce explosive passing plays (15+ yards) more than 15% of the time, which gives play-callers and defensive coordinators concrete numbers to plan around.

## Assignment 5: Inference
- **Tests run and alpha (0.05):** we ran two hypothesis tests. First, whether average yards-to-go on a passing play equals 10: p-value below 0.05, so we rejected the null and concluded the average is not 10. Second, whether the average passing play begins past midfield: p-value above 0.05, so we failed to reject the null.
- **Confidence interval:** our 95% confidence interval for yards-to-go was 8.882 to 8.996, which excludes 10 and reinforces the first test's conclusion.
- **Assumptions:** the yards-to-go variable is skewed, but with a sample size of 18,600 the Central Limit Theorem lets us treat the sampling distribution of the mean as approximately normal. The absolute yard line variable was already normally distributed. Independence is reasonable since each row is a distinct play.

## Assignment 6: Regression
- **First predictors removed and why:** we removed the predictors that were not statistically significant. The first model had an R-squared of 0.73; after dropping the insignificant variables, the final model had an R-squared of 0.70, so it explains slightly less variation with fewer predictors.
- **Most useful predictor:** Third and Fourth Down had the largest coefficient and the smallest p-value in both models. preSnapHomeScore, yardsToGo, and preSnapVisitorScore had positive relationships with offensePlayResult, while game_time_elapsed, 11 personnel, and Third and Fourth Down were negative.
- **Interpretation and limits:** with R-squared at 0.70, most variation is still explained by factors outside the model, so results show relationships rather than causation. A possible improvement is adding an interaction between Down and yardsToGo, or narrowing to a single team.
