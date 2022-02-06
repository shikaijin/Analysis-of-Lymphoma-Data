# Analysis of Lymphoma Data ![visitor badge](https://visitor-badge.glitch.me/badge?page_id=shikaijin/STAT-486-Survival-Analysis.visitor-badge)


### Introduction
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Lymphoma data given data came from a randomized clinical trial of a new treatment for lymphoma. The variables in the lymphoma data set: performance status, age in year, cancer stage, sex, B-symptom, international rIPI score, received other drug before randomization, response to other treatments before randomization, overall survival status, overall survival time in months and treatment vs control were also recorded. Think of survival probabilities as a response and other variables as explanatory variables, I attempted to demonstrated that the new treatment performs as good as the standard treatment in term of overall survival. Further, I was interested to conduct exploratory analysis to study how these variables affect the survival time. I would first model the data using cox regression models of the form</p>
<p align="center">h(t|z) = h<sub>0</sub>(t)e<sup>β<sup>T</sup>z</sup>    (1)</p>
<p> with response (x<sub>i</sub>,δ<sub>i</sub>) and covariates z<sub>i</sub>, where x<sub>i</sub> = min(t<sub>i</sub>,c<sub>i</sub>) for subject I = 1,…, n. We will check whether the semi-parametric and non-parametric methods describe their association. If they work poorly for the data, we then apply the parametric methods. I would be looking for a simpler model to describe the relationship between the response variable and explanatory variables.</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;According to some research, stage of lymphoma, the presence of symptoms B, age over 45, and male may affect a person's prognosis, and some of these factors mean that the lymphoma may be more severe [2]. International rIPI score is a clinically useful prognostic indicator and is based on age, stage and LDH [3]. This is, we will expect to see international rIPI score is an important explanatory variable.</p>



* Data: [View here](https://github.com/shikaijin/Analysis-of-Lymphoma-Data/blob/1a10df0feeea003f9abe8036ec13389b8ecd2f9d/lymphoma.csv)
* R Code: [View here](https://github.com/shikaijin/Analysis-of-Lymphoma-Data/blob/1a10df0feeea003f9abe8036ec13389b8ecd2f9d/output.R)
* Paper: [View here](https://github.com/shikaijin/Analysis-of-Lymphoma-Data/blob/94b98acac60c343d5f773070e7a63d13090ed662/paper.md)

