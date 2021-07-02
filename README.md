# Analysis of Lymphoma Data
#### by Zoe Jin

    
### Introduction
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Lymphoma data given data came from a randomized clinical trial of a new treatment for lymphoma. The variables in the lymphoma data set: performance status, age in year, cancer stage, sex, B-symptom, international rIPI score, received other drug before randomization, response to other treatments before randomization, overall survival status, overall survival time in months and treatment vs control were also recorded. Think of survival probabilities as a response and other variables as explanatory variables, I attempt to demonstrated that the new treatment performs as good as the standard treatment in term of overall survival. Further, I was interested to conduct exploratory analysis to study how these variables affect the survival time. I will first model the data using cox regression models of the form</p>
<p align="center">h(t|z) = h<sub>0</sub>(t)e<sup>β<sup>T</sup>z</sup>    (1)</p>
<p> with response (x<sub>i</sub>,δ<sub>i</sub>) and covariates z<sub>i</sub>, where x<sub>i</sub> = min(t<sub>i</sub>,c<sub>i</sub>) for subject I = 1,…, n. We will check whether the semi-parametric and non-parametric methods describe their association. If they work poorly for the data, we then apply the parametric methods. We will be looking for a simpler model to describe the relationship between the response variable and explanatory variables.</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;According to some research, stage of lymphoma, the presence of symptoms B, age over 45, and male may affect a person's prognosis, and some of these factors mean that the lymphoma may be more severe [2]. International rIPI score is a clinically useful prognostic indicator and is based on age, stage and LDH [3]. This is, we will expect to see international rIPI score is an important explanatory variable.</p>

### Missing data analysis
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I began to check whether the variables (B-symptom and Race) with missing values are important in explaining survival time distributions. The approach I used was model comparison by LR statistic. The observed LR statist is calculated as 
<p align="center">Λ = 2[l(𝛽̂)-l(𝛽̃)] ∼𝜒<sup>2</sup><sub>𝑣2−𝑣1</sub>   (2)</p>
<p> where ν<sub>1</sub>, ν<sub>2</sub> are the degrees of freedom (d.f.) of two comparison models. For each comparison, I fitted with cox regression models and omitted those patients with missing values. In the results that follow, we saw that Models 2 is significantly different in fitting the data than Model 1 so that we cannot drop B-symptom. The observed LR statistic of Model 4 is 0.02, and the p-value is 0.4440447 (Table 1), which implies Model 2 is as good as Model 1. This is, race does not play an important role, so we then did not consider the variable in the rest of analysis. There is a noticeable proportion of missing B-symptom values, thus, we will use imputation to make up for a missing data. A common approach is to find all the sample individuals who are similar on other variables, then choose one of their values on the missing variable [1]. We might have poorer results because imputation may introduce bias or affect the representativeness of results. In order to get more accurate results, more complete data is needed to replace those with missing data.</p>

<p>Table 1.1: Analysis of deviance table for cox regression models</p>

| Model         | Form          | LR statistic | D.F.  | p-value                  |
| ------------- |:-------------:|-------------:| -----:|:------------------------:|
| 1             | trt, b-symptom| 22.92        |  2    | NA                       |
| 2             | trt           | 0.02         |  1    |1.705426e-06 (vs Model 1) |
| 3             | trt, race     | 2.7          |  4    | NA                       |
| 4             | trt           | 0.02         |  1    |0.4440447 (vs Model 3)    |


### Initial Exploration
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I examined the data by scatter plots to explore the connection between each variable and survival time. There are some differences for survival time in each variable, but some levels have different survival time within each variable. It is obvious that score 0,1 and DU >1 have different mean effects from other levels within each group. Examining in this way, I noticed the scatter plot of log failure time versus treatment shows no substantial difference in the mean effects between treatment group. Similarly, levels in cancer stage, sex, received other drug before randomization and response to other treatments before randomization also have similar mean effect. We can easily see the difference within each group, however, it is difficult to tell how these factors affect failure time together and which factors are the most important explanatory variables, hence, we are looking for a representation of the relationship between response and explanatory variables.</p>
<img src="https://user-images.githubusercontent.com/79543449/123740547-9efc2f80-d876-11eb-8e69-c3b2cbdaf27a.png">


### Semi-parametric model analysis
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To seek which variables might affect the survival probability of Lymphoma patients, my approach for selecting a suitable model for the data was to use LR statistic as described above.</p>
<p>I performed model selection procedure as follow:</p>
<p>1. Start with a Cox regression model with all covariates as the best model.</p>
<p>2. Construct a new model by dropping variables with greater p-value and set a null hypothesis H0 (e.g. Model 1 is as good as Model 0).</p>
<p>3. Apply LR statistic to find the p-value.</p>
<p>4. If null hypothesis H0 reject, then the new model is different in fitting the data than the model with more terms. STOP.</p>
<p>5. If null hypothesis H0 cannot reject, use the new model instead, and then repeat steps 2-4. </p>
<p>I deduced the relationship between the ratio of the hazard at time t to the baseline hazard and exp(coefficient) from equation (1), which turns out to be
<p align="center"> h(t|z) / h<sub>0</sub>(t) = e<sup>β<sup>T</sup>z</sup>    (3)</p>
<p> It indicates that predictor (a level of the covariate) does not affect survival when the ratio is close to 1. When the ratio is less than 1, the predictor is related to the increase in survival rate and when the hazard ratio is greater than 1, the predictor is related to the decrease in survival rate.</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In the results that follow, the exp(coefficient) of treatment is 0.9915560 in Model 0, which implies the new treatment performs as good as the standard treatment in term of overall survival. Both International rIPI score at 0 or 1 and response with duration > 1 year gives exp(coefficient) around 0.4 in Model 8, this is said that patients with these two factors are more likely to survival. Besides, ratios of all other variables in Model 8 have either are close or greater than 1. In other words, predictor from these groups does not affect survival or decrease survival rate. This implies patients with performance status 0, did not receive radiotherapy, with no B-symptom, response to other treatments with duration > 1 year and r score 0,1 are more like to survival. The observed LR statistic of Model 8 is 188.7, and the p-value is 0.1062229 (Table 1.2), so we concluded that Model 8 is as good as Model 0, Model 6 and Model 7 for the data, based on likelihood ratio test. We saw that Models 9 is a little different (worse) in fitting the data than Model 8 so that we cannot fit the data with Model 9. Therefore, the final cox regression model chosen was the one with performance status, B-symptom, international rIPI score, received other drug before randomization and response to other treatments before randomization.</p>

<p>Table 1.2: Analysis of deviance table for cox regression models</p>

| Model         | Form                                                                   | LR statistic| D.F.| p-value          |
| ------------- |:----------------------------------------------------------------------:|-----:| -----:|:------------------------:|
| 0             | PERF_STA, AGE STAGE, SEX, B_SYM, r_score, PR_RAD, pr_drug, pr_resp, trt| 198|  16    | NA                       |
| 6             | PERF_STA, STAGE, SEX, B_SYM, r_score, PR_RAD, pr_drug, pr_resp        | 197.9  | 14   |0.9811855 (vs Model 0) |
| 7             | PERF_STA, B_SYM, r_score, PR_RAD, pr_drug, pr_resp|191.3  |  10    | 0.1556166 (vs Model 6)          |
| 8             | PERF_STA, B_SYM, r_score, PR_RAD, pr_resp           | 188.7        |  9    |0.1062229 (vs Model 7)    |
| 9             | PERF_STA, B_SYM, r_score, pr_resp         | 182.5       | 8    |0.01313057 (vs Model 8)    |


### Nonparametric model analysis
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I then used Kaplan-Meier estimates plot to compare new treatment performs with the standard treatment. It suggests that the new treatment performs as good as the standard treatment since their survival functions are nearly overlapping.</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To check how each variable in the final Cox regression model (Model 8) might affect the survival probability graphically, and which variables have the most influence, I compared survival functions for different factors in the variables, we observed patients with response with duration > 1 year are much different (higher) survival probability than the other two levels. In addition, patients with performance status 0 and international rIPI score 0 or 1 are more likely to survival than those with other levels, while there was no significant difference between the patients who received radiotherapy before randomization and those who did not. Through graphic exploration, it seems like Kaplan-Meier estimates agree with the Cox regression model, in which response to other treatments before randomization, international rIPI score and performance status play significant role for survival probability (Figure 1). Besides, I modeled variables in Model 8 again used the Kaplan-Meier estimates, and its result gives that patients with performance status 0, did not receive radiotherapy, with no B-symptom ,response to other treatments with duration > 1 year and r score 0,1 have the highest survival probability.</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Furthermore, I applied log rank test to confirm these observations. In each test, I first set the null hypothesis that each level has the same survival time distribution. Log rank test for treatment has p-values much greater than 0.001 (Table 2). There is no evidence against the null hypothesis. It follows that the survival time distribution of the treatment group is similar to the distribution of the control group. For response to other treatments before randomization, international rIPI score, B-symptom and performance, these variables have p-values smaller than 0.001 (Table 2). There are very strong evidences against the null hypothesis resulting in a significant difference in survival distribution among levels. However, the status survival functions interest with each other in performance so that log rank test does not works for these two variables. Therefore, we concluded response to other treatments before randomization and international rIPI score have more significant influence on the survival time.</p>

<p>Table 2: log rank test</p>

| Variables         | P value                                                                   | 
| ------------- |:----------------------------------------------------------------------:|
| trt             | 0.9| 
| PERF_STA             | 2e-15      | 
| PR_RAD             | 0.7  |  
|B_SYM             | 2e-06         | 
| r_score             | 1e-15        |
| pr_resp            | <2e-16       |
