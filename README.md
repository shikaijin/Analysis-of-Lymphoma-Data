# Analysis of Lymphoma Data ![visitor badge](https://visitor-badge.glitch.me/badge?page_id=shikaijin/STAT-486-Survival-Analysis.visitor-badge)


### Introduction
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The lymphoma data provided comes from a randomized clinical trial of a new treatment for lymphoma. As part of the lymphoma data set, the following variables were recorded: performance status, age, stage of cancer, gender, B-symptom, international rIPI score, receiving other drugs before randomization, responding to other treatments before randomization, overall survival status, overall survival time in months, and treatment versus control. Assuming survival probabilities as a response and other variables as explanatory variables, I attempted to demonstrate that the new treatment performs similarly to the conventional treatment in terms of overall survival. Also, I would like to conduct exploratory analysis in order to determine the effect of these variables on the survival time. I would first model the data using cox regression models of the form</p>
<p align="center">h(t|z) = h<sub>0</sub>(t)e<sup>β<sup>T</sup>z</sup>    (1)</p>
<p> with response (x<sub>i</sub>,δ<sub>i</sub>) and covariates z<sub>i</sub>, where x<sub>i</sub> = min(t<sub>i</sub>,c<sub>i</sub>) for subject I = 1,…, n. It would be valuable for me to check whether the semi-parametric and non-parametric methods describe their relationship. When these methods do not work well for the data, I can then apply parametric methods. My objective is to find a simpler model to describe the relationship between the response variable and explanatory variables.</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Some researchers have found that stage of lymphoma, the presence of symptoms B, age over 45, and being male may affect one's prognosis, and some of these factors may indicate a more severe case of lymphoma[2]. Based on age, stage, and LDH, the International rIPI score is a clinically useful prognostic indicator[3]. Therefore, I expect the international rIPI score to be an important explanatory variable.</p>



* Data: [View here](https://github.com/shikaijin/Analysis-of-Lymphoma-Data/blob/1a10df0feeea003f9abe8036ec13389b8ecd2f9d/lymphoma.csv)
* R Code: [View here](https://github.com/shikaijin/Analysis-of-Lymphoma-Data/blob/1a10df0feeea003f9abe8036ec13389b8ecd2f9d/output.R)
* Paper: [View here](https://github.com/shikaijin/Analysis-of-Lymphoma-Data/blob/94b98acac60c343d5f773070e7a63d13090ed662/paper.md)

