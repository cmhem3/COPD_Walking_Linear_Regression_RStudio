# COPD and Walking Distance: 
**An MPH Graduate Project Peer Review – Interpreting Multiple Linear Regression Models in R**

### PROJECT INSTRUCTIONS: 
Fit a multiple regression model and to explore the relationships between Age and FVC on Walking distance (MWT1best).  FVC (Forced vital capacity) is the total amount of air exhaled during a pulmonary function test. This is a measure of lung capacity and health.  Units are measured in Liters.  MWT1best is the study's variable named for total distance walked by the participant.  Units are in meters.

*ESSAY QUESTIONS*
1.	What are the differences between the coefficients in simple and multiple regression the models? Why do they differ?
2.	How does the adjusted R2 statistic change and why?
3.	Which of the regression models would you choose as your final model and why?
- Mention any checks you performed or observations you had about model fit and assumptions.
- Did you have any concerns with collinearity?

4.	Discuss whether you would include FVC and FEV1 in the same multiple regression model with AGE and expand on why you may or may not want to do that.

**MODEL-1:  Walking distance and age: Identify the α and β coefficients**

    -MWT1Best_AGE <- lm(MWT1Best~AGE, data = COPD)
    -Summary(MWT1Best_AGE)

Residuals:
- Min -257.44
- 1Q  -84.40 
- Median 20.30 
- 3Q  67.87
- Max 250.16 


Coefficients:
- (Intercept) 616.453
- AGE         -3.104
  
Residual standard error: 104.2 on 98 degrees of freedom  (1 observation deleted due to missingness)

Multiple R-squared:  0.05294,	Adjusted R-squared:  0.04328 

F-statistic: 5.478 on 1 and 98 DF,  

p-value: 0.02128

95% Confidence Interval: 

    -confint(MWT1Best_AGE)  

- 2.5 %,        97.5 %
- (Intercept)        431.023080,    801.8819906
- AGE                 -5.735718,    -0.4722946

**MODEL-1: Scatter plot of Age and Walking Distance: 

    -plot(COPD$MWT1Best, COPD$AGE, xlab = “AGE”, ylab = “MWT1Best”)
![image](https://github.com/user-attachments/assets/28f12a44-2edb-4962-8f55-cb663d1cd7e9)

 
**Summarizing the above: Identify the α and β coefficients**

    -Equation for the line of regression: MWT1best = α + β ∗ AGE or y = 616.453 – (3.104) * AGE, where: 
- y-intercept:  α = 616.453, this is the “average y when x = 0”.  Average walking distance at 0 years old (just a reference point, not actually measuring babies).
- coefficient of y: β = -3.104, this is the average decrease in walking (y) for every one-year increase age (x).  For every one-year increase in age, it is estimated that walking distance will decrease by 3.1 meters.
- Adjusted R-squared:  0.04328:  The model explains 4.32% of the variance in the observations.  This suggests that the model is only explaining a small portion of the variance in our dependent variable, while a large amount of the variability remains unexplained.
- 95% CI:  -5.735718 to -0.4722946: This estimates that the population coefficient values likely occur within this range (i.e. this is estimated population decrease distance in walking per year of age gained).  Here, our coefficient of y is roughly the mean of our 95% CI.
- p-value:  0.02128:  Since the CI was set at 95%, and this is <5%, we can reject the null hypothesis (H0) stating there’s no correlation between age and walking ability.  Since there is a 2.128% chance of getting these results, it can likely be concluded that age is correlated with decreased walking ability (as the scatter plot confirms the number of MWT1Best data points <400 with age >70, or the older the member, the more likely their walking ability decreases, on average).


**MODEL-2:  FVC and MWT1Best: Identify the α and β coefficients for this model**

    -MWT1Best_FVC <- lm(MWT1Best~FVC, data = COPD)
    -Summary(MWT1Best_FVC)

Residuals:
- Min -251.663 
- 1Q -66.598
- Median 6.364
- 3Q 63.539
- Max 246.125
 

Coefficients:
- (Intercept)  254.951     
- FVC           48.630
  
Residual standard error: 95.87 on 98 degrees of freedom  (1 observation deleted due to missingness)

Multiple R-squared:  0.1987,	Adjusted R-squared:  0.1905 

F-statistic: 24.29 on 1 and 98 DF,  

p-value: 3.368e-06

95% Confidence Interval: 

    -confint(MWT1Best_FVC)

-             2.5 %,        97.5 %
- (Intercept) 193.87101,     316.03072
- FVC          29.05061,      68.20964

MODEL-2: Scatter plot of FVC and Walking Distance:

    -plot(COPD$MWT1Best, COPD$FVC, xlab = "FVC", ylab = "MWT1Best")
 
**Summarizing the above: Identify the α and β coefficients**
•	Equation for the line of regression: MWT1best = α + β ∗ FVC, or: y = 254.95 + (48.63) *FVC, where:
o	α = 254.95, this is the “average y when x = 0” (i.e. the average walking distance at 0 FVC).
o	β = 48.63, the average increase in walking distance (y) for every one unit increase FVC (x) (i.e. for every 1 unit increase in FVC, walking distance will increase by 48.63 meters).

•	 Adjusted R-squared:  0.1905
o	The model explains 19% of the variance in the observations, which shows this model fits the data a bit more closely than the previous model (i.e. the model explains variations in walking distance in relation to lung capacity better than the model explaining variations in walking when compared to age).

•	95% CI:  29.05061 to 68.20964
o	Detecting the likely population observation occurs in this range, showing that an average person in this population would likely experience 29 – 68 meters improvement in walking for every 1 unit increase in FVC.

•	p-value:  3.368e-06
o	this is <5% so we can likely reject H0.  Meaning, with our 95% CI, we have a less than 5% chance of getting these results randomly (i.e. there is a likely effect of FVC on walking ability).  
*MODEL-3:  Multi-Linear Regression Model for FVC, AGE, and MWT1Best: Identify the α and β coefficients 
>MWT1Best_FVC_AGE <- lm(MWT1Best~FVC+AGE, data = COPD)
>summary(MWT1Best_FVC_AGE)
Residuals:
    Min      1Q  Median      3Q     Max 
-236.89  -66.05   12.55   75.54  211.72 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)  425.377     94.099   4.521 1.74e-05 ***
FVC           46.058      9.827   4.687 9.06e-06 ***
AGE           -2.325      1.215  -1.914   0.0586 .  

Residual standard error: 94.59 on 97 degrees of freedom
  (1 observation deleted due to missingness)
Multiple R-squared:  0.2278,	Adjusted R-squared:  0.2119 
F-statistic: 14.31 on 2 and 97 DF,  p-value: 3.588e-06

>confint(MWT1Best_FVC_AGE)
   2.5 %       97.5 %
(Intercept) 238.616666 612.13818023
FVC          26.553107  65.56260023
AGE          -4.736637   0.08649919

>plot(COPD$FVC, COPD$AGE, xlab = "AGE", ylab = "FVC")
 
Summarizing the above: Note you now have two β coefficients to interpret:
•	Equation for the multi-linear regression:  MWT1best = α + (β1) ∗ FVC + (β2) ∗ AGE, or: y = 425.377 + β1(46.058) * FVC + β2(-2.325) * AGE
o	α = 425.377, this is the “average y when x = 0.”  Average walking distance at 0 FVC & AGE
o	β1 = 46.058 average increase in walking (y) for every one unit increase FVC (x).  Meaning, for every one unit increase in FVC, walking distance will increase by 46.058 meters.
o	β2 = -2.325, average decrease in walking (y) for every one-year increase in age (x).
 
•	 Adjusted R-squared:  0.2119
o	The model explains 21% of the variance in the observations.  Rather, the model with two predictor variables better explains the variance in our dependent variable (walking distance, “MTW1best”) than the previous single-regression models using only one predictor.  

•	95% CI:  29.05061 to 68.20964
o	Means the real population values likely lay within this range.  Or rather, this is the range to which both considering age and lung capacity impacts walking distance in the population from which the sample was pulled.

•	p-value:  3.588e-06
o	this is <5% so we can likely reject H0, thus showing our results were not likely due to chance alone and we can make assumptions about FVC and age with its impact on walking distance.


CORRELATION COEFFICIENT:  Pearson vs Spearman
>cor.test(COPD$AGE, COPD$FVC, use="complete.obs", method="pearson")
•	-0.1452257
>cor.test(COPD$AGE, COPD$FVC, use="complete.obs", method="spearman")
•	-0.1771108
o	Both correlations show a very weak relationship between age and lung function.
o	Both p-values were <0.05, which suggests results are not likely due to chance alone.
o	Collinearity is not likely to be problematic here as FVC is a measure of lung capacity and is not categorically similar to age.  Thus, the model is not at a high risk of modeling two overly similar predictor variables, which if it did would likely confound where the effect on walking is coming from.  

COMPARING MODEL ASSUMPTIONS:
1.	Linearity between outcome (y) and predictor (x).
2.	Outcome variable is normally distributed across the predictor values.
3.	Variance of outcomes are constant across predictor values.
>FVC_AGE <- lm(AGE~FVC, data = COPD)
>plot(FVC_AGE)
 
A.	Fitted Values: shows relatively constant variance across predictor x.
B.	Q-Q plot: shows the majority of observations stay on the line in the middle, indicating normality.

SUMMARY:
Of all three models, I would choose the multi-linear regression model based on a lower p-value and a better adjusted R-squared value.  As well, it is useful to model both predictor variables separately, prior to putting them in a multi-regression model; this helps to understand the individual effects on walking prior to comparing combined effects.  Finally, in any regression model, it is warranted that al variables must be carefully selected to ensure clear results.  For example, it is not advised to include both FVC and FEV1 within the same model, as both are measures of pulmonary health.  If two predictor variables are very similar and included in the model, issues of collinearity arise.  This is when there is difficulty accurately assessing or understanding results of the model.  FVC and Age are not highly similar, and thus make for good additions to a multiple regression model.

