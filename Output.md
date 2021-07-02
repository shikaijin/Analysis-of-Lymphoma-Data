```
> dat<-read.csv("lymphoma.csv",header = T)
> library(survival)
> dat1<-dat[-c(2,37,50,61,73,146,151,195,202,384,405,420,424,435,513,514,525,528,554,565,568,572,575,593,600,611),]
> fit1<-coxph(Surv(os_time,os_event)~as.factor(trt)+as.factor(B_SYM),data = dat1)
> summary(fit1)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(trt) + as.factor(B_SYM), 
    data = dat1)

  n= 593, number of events= 391 

                             coef exp(coef)  se(coef)      z Pr(>|z|)    
as.factor(trt)treatment -0.007254  0.992772  0.101300 -0.072    0.943    
as.factor(B_SYM)N       -0.501584  0.605571  0.102900 -4.874 1.09e-06 ***
as.factor(B_SYM)Y              NA        NA  0.000000     NA       NA    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

                        exp(coef) exp(-coef) lower .95 upper .95
as.factor(trt)treatment    0.9928      1.007     0.814    1.2108
as.factor(B_SYM)N          0.6056      1.651     0.495    0.7409
as.factor(B_SYM)Y              NA         NA        NA        NA

Concordance= 0.576  (se = 0.014 )
Likelihood ratio test= 22.92  on 2 df,   p=1e-05
Wald test            = 23.78  on 2 df,   p=7e-06
Score (logrank) test = 24.28  on 2 df,   p=5e-06

> fit2<-coxph(Surv(os_time,os_event)~as.factor(trt),data = dat1)
> summary(fit2)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(trt), data = dat1)

  n= 593, number of events= 391 

                          coef exp(coef) se(coef)     z Pr(>|z|)
as.factor(trt)treatment 0.0135    1.0136   0.1012 0.133    0.894

                        exp(coef) exp(-coef) lower .95 upper .95
as.factor(trt)treatment     1.014     0.9866    0.8312     1.236

Concordance= 0.499  (se = 0.013 )
Likelihood ratio test= 0.02  on 1 df,   p=0.9
Wald test            = 0.02  on 1 df,   p=0.9
Score (logrank) test = 0.02  on 1 df,   p=0.9

> 1-pchisq(2*(fit1$loglik[2]-fit2$loglik[2]),1)
[1] 1.705426e-06
> dat2<-dat[-c(66,74,117,140,235,236,238,379,380,439,440,486,607,616,316,345,359,360,361,367,368,369,434,510,614),]
> 
> fit3<-coxph(Surv(os_time,os_event)~as.factor(trt)+as.factor(RACE),data = dat2)
> summary(fit3)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(trt) + as.factor(RACE), 
    data = dat2)

  n= 594, number of events= 391 

                            coef exp(coef) se(coef)      z Pr(>|z|)
as.factor(trt)treatment -0.00837   0.99167  0.10168 -0.082    0.934
as.factor(RACE)3         0.26215   1.29972  0.30663  0.855    0.393
as.factor(RACE)5         0.24971   1.28365  0.18057  1.383    0.167
as.factor(RACE)6         0.26180   1.29927  0.41247  0.635    0.526

                        exp(coef) exp(-coef) lower .95 upper .95
as.factor(trt)treatment    0.9917     1.0084    0.8125     1.210
as.factor(RACE)3           1.2997     0.7694    0.7126     2.371
as.factor(RACE)5           1.2836     0.7790    0.9011     1.829
as.factor(RACE)6           1.2993     0.7697    0.5789     2.916

Concordance= 0.516  (se = 0.014 )
Likelihood ratio test= 2.7  on 4 df,   p=0.6
Wald test            = 2.87  on 4 df,   p=0.6
Score (logrank) test = 2.89  on 4 df,   p=0.6

> fit4<-coxph(Surv(os_time,os_event)~as.factor(trt),data = dat2)
> summary(fit4)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(trt), data = dat2)

  n= 594, number of events= 391 

                            coef exp(coef) se(coef)      z Pr(>|z|)
as.factor(trt)treatment -0.01435   0.98575  0.10116 -0.142    0.887

                        exp(coef) exp(-coef) lower .95 upper .95
as.factor(trt)treatment    0.9857      1.014    0.8085     1.202

Concordance= 0.506  (se = 0.013 )
Likelihood ratio test= 0.02  on 1 df,   p=0.9
Wald test            = 0.02  on 1 df,   p=0.9
Score (logrank) test = 0.02  on 1 df,   p=0.9

> 1-pchisq(2*(fit3$loglik[2]-fit4$loglik[2]),3)
[1] 0.4440447
> fit0<-coxph(Surv(os_time,os_event)~as.factor(PERF_STA)+AGE+as.factor(STAGE)+as.factor(SEX)+as.factor(PR_RAD)+as.factor(B_SYM)+as.factor(r_score)+as.factor(pr_resp)+as.factor(pr_drug)+as.factor(trt),data = dat)
> summary(fit0)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA) + 
    AGE + as.factor(STAGE) + as.factor(SEX) + as.factor(PR_RAD) + 
    as.factor(B_SYM) + as.factor(r_score) + as.factor(pr_resp) + 
    as.factor(pr_drug) + as.factor(trt), data = dat)

  n= 619, number of events= 409 

                              coef  exp(coef)   se(coef)      z Pr(>|z|)    
as.factor(PERF_STA)1     0.4068774  1.5021199  0.1166653  3.488 0.000487 ***
as.factor(PERF_STA)2     0.2768054  1.3189097  0.1913758  1.446 0.148066    
as.factor(PERF_STA)3     0.5430003  1.7211632  0.2765965  1.963 0.049629 *  
AGE                      0.0009183  1.0009187  0.0050895  0.180 0.856816    
as.factor(STAGE)II       0.1886699  1.2076423  0.2308251  0.817 0.413716    
as.factor(STAGE)III     -0.2224421  0.8005614  0.2494785 -0.892 0.372592    
as.factor(STAGE)IV      -0.0555523  0.9459625  0.2484071 -0.224 0.823042    
as.factor(SEX)M          0.0851666  1.0888985  0.1050964  0.810 0.417729    
as.factor(PR_RAD)Y       0.2947663  1.3428125  0.1175858  2.507 0.012182 *  
as.factor(B_SYM)Y        0.3112282  1.3651006  0.1045379  2.977 0.002909 ** 
as.factor(r_score)0, 1  -0.9967294  0.3690846  0.1915599 -5.203 1.96e-07 ***
as.factor(r_score)2     -0.2281887  0.7959741  0.1373246 -1.662 0.096578 .  
as.factor(pr_resp)DU>1  -0.9568619  0.3840963  0.1485822 -6.440 1.20e-10 ***
as.factor(pr_resp)SDPD   0.2325563  1.2618214  0.1143084  2.034 0.041905 *  
as.factor(pr_drug)Y      0.1580154  1.1711842  0.1178515  1.341 0.179985    
as.factor(trt)treatment -0.0084799  0.9915560  0.0997102 -0.085 0.932225    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

                        exp(coef) exp(-coef) lower .95 upper .95
as.factor(PERF_STA)1       1.5021     0.6657    1.1951    1.8880
as.factor(PERF_STA)2       1.3189     0.7582    0.9064    1.9192
as.factor(PERF_STA)3       1.7212     0.5810    1.0009    2.9598
AGE                        1.0009     0.9991    0.9910    1.0110
as.factor(STAGE)II         1.2076     0.8281    0.7682    1.8985
as.factor(STAGE)III        0.8006     1.2491    0.4910    1.3054
as.factor(STAGE)IV         0.9460     1.0571    0.5813    1.5393
as.factor(SEX)M            1.0889     0.9184    0.8862    1.3380
as.factor(PR_RAD)Y         1.3428     0.7447    1.0664    1.6908
as.factor(B_SYM)Y          1.3651     0.7325    1.1122    1.6755
as.factor(r_score)0, 1     0.3691     2.7094    0.2536    0.5373
as.factor(r_score)2        0.7960     1.2563    0.6081    1.0418
as.factor(pr_resp)DU>1     0.3841     2.6035    0.2871    0.5139
as.factor(pr_resp)SDPD     1.2618     0.7925    1.0086    1.5787
as.factor(pr_drug)Y        1.1712     0.8538    0.9296    1.4755
as.factor(trt)treatment    0.9916     1.0085    0.8155    1.2056

Concordance= 0.718  (se = 0.012 )
Likelihood ratio test= 198  on 16 df,   p=<2e-16
Wald test            = 183  on 16 df,   p=<2e-16
Score (logrank) test = 194.6  on 16 df,   p=<2e-16

> fit6<-coxph(Surv(os_time,os_event)~as.factor(PERF_STA)+as.factor(STAGE)+as.factor(SEX)+as.factor(PR_RAD)+as.factor(B_SYM)+as.factor(r_score)+as.factor(pr_resp)+as.factor(pr_drug),data = dat)
> summary(fit6)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA) + 
    as.factor(STAGE) + as.factor(SEX) + as.factor(PR_RAD) + as.factor(B_SYM) + 
    as.factor(r_score) + as.factor(pr_resp) + as.factor(pr_drug), 
    data = dat)

  n= 619, number of events= 409 

                           coef exp(coef) se(coef)      z Pr(>|z|)    
as.factor(PERF_STA)1    0.40630   1.50125  0.11666  3.483 0.000496 ***
as.factor(PERF_STA)2    0.27347   1.31451  0.19034  1.437 0.150795    
as.factor(PERF_STA)3    0.53794   1.71248  0.27512  1.955 0.050546 .  
as.factor(STAGE)II      0.18870   1.20768  0.23082  0.818 0.413622    
as.factor(STAGE)III    -0.22302   0.80010  0.24960 -0.894 0.371579    
as.factor(STAGE)IV     -0.06059   0.94121  0.24693 -0.245 0.806163    
as.factor(SEX)M         0.08747   1.09141  0.10444  0.838 0.402308    
as.factor(PR_RAD)Y      0.29321   1.34073  0.11725  2.501 0.012391 *  
as.factor(B_SYM)Y       0.31084   1.36458  0.10449  2.975 0.002932 ** 
as.factor(r_score)0, 1 -1.00748   0.36514  0.18201 -5.535 3.10e-08 ***
as.factor(r_score)2    -0.23379   0.79153  0.13320 -1.755 0.079230 .  
as.factor(pr_resp)DU>1 -0.95431   0.38508  0.14800 -6.448 1.13e-10 ***
as.factor(pr_resp)SDPD  0.23216   1.26132  0.11423  2.032 0.042108 *  
as.factor(pr_drug)Y     0.16091   1.17458  0.11689  1.377 0.168646    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

                       exp(coef) exp(-coef) lower .95 upper .95
as.factor(PERF_STA)1      1.5012     0.6661    1.1944    1.8869
as.factor(PERF_STA)2      1.3145     0.7607    0.9052    1.9089
as.factor(PERF_STA)3      1.7125     0.5839    0.9987    2.9363
as.factor(STAGE)II        1.2077     0.8280    0.7682    1.8986
as.factor(STAGE)III       0.8001     1.2498    0.4905    1.3050
as.factor(STAGE)IV        0.9412     1.0625    0.5801    1.5271
as.factor(SEX)M           1.0914     0.9162    0.8894    1.3393
as.factor(PR_RAD)Y        1.3407     0.7459    1.0655    1.6871
as.factor(B_SYM)Y         1.3646     0.7328    1.1119    1.6747
as.factor(r_score)0, 1    0.3651     2.7387    0.2556    0.5217
as.factor(r_score)2       0.7915     1.2634    0.6097    1.0277
as.factor(pr_resp)DU>1    0.3851     2.5969    0.2881    0.5147
as.factor(pr_resp)SDPD    1.2613     0.7928    1.0083    1.5778
as.factor(pr_drug)Y       1.1746     0.8514    0.9341    1.4770

Concordance= 0.718  (se = 0.012 )
Likelihood ratio test= 197.9  on 14 df,   p=<2e-16
Wald test            = 182.8  on 14 df,   p=<2e-16
Score (logrank) test = 194.5  on 14 df,   p=<2e-16

> 1-pchisq(2*(fit0$loglik[2]-fit6$loglik[2]),16-14)
[1] 0.9811855
> fit7<-coxph(Surv(os_time,os_event)~as.factor(PERF_STA)+as.factor(PR_RAD)+as.factor(B_SYM)+as.factor(r_score)+as.factor(pr_resp)+as.factor(pr_drug),data = dat)
> summary(fit7)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA) + 
    as.factor(PR_RAD) + as.factor(B_SYM) + as.factor(r_score) + 
    as.factor(pr_resp) + as.factor(pr_drug), data = dat)

  n= 619, number of events= 409 

                          coef exp(coef) se(coef)      z Pr(>|z|)    
as.factor(PERF_STA)1    0.4181    1.5190   0.1162  3.598  0.00032 ***
as.factor(PERF_STA)2    0.3343    1.3970   0.1872  1.785  0.07419 .  
as.factor(PERF_STA)3    0.6054    1.8321   0.2738  2.211  0.02701 *  
as.factor(PR_RAD)Y      0.2968    1.3455   0.1158  2.563  0.01037 *  
as.factor(B_SYM)Y       0.3170    1.3730   0.1039  3.050  0.00229 ** 
as.factor(r_score)0, 1 -0.8351    0.4338   0.1368 -6.107 1.02e-09 ***
as.factor(r_score)2    -0.1981    0.8203   0.1290 -1.536  0.12447    
as.factor(pr_resp)DU>1 -0.9403    0.3905   0.1474 -6.381 1.76e-10 ***
as.factor(pr_resp)SDPD  0.2571    1.2932   0.1125  2.285  0.02233 *  
as.factor(pr_drug)Y     0.1846    1.2027   0.1156  1.596  0.11044    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

                       exp(coef) exp(-coef) lower .95 upper .95
as.factor(PERF_STA)1      1.5190     0.6583    1.2097    1.9075
as.factor(PERF_STA)2      1.3970     0.7158    0.9678    2.0164
as.factor(PERF_STA)3      1.8321     0.5458    1.0712    3.1332
as.factor(PR_RAD)Y        1.3455     0.7432    1.0724    1.6883
as.factor(B_SYM)Y         1.3730     0.7283    1.1199    1.6832
as.factor(r_score)0, 1    0.4338     2.3051    0.3318    0.5672
as.factor(r_score)2       0.8203     1.2191    0.6370    1.0562
as.factor(pr_resp)DU>1    0.3905     2.5607    0.2926    0.5213
as.factor(pr_resp)SDPD    1.2932     0.7733    1.0372    1.6124
as.factor(pr_drug)Y       1.2027     0.8315    0.9588    1.5086

Concordance= 0.714  (se = 0.012 )
Likelihood ratio test= 191.3  on 10 df,   p=<2e-16
Wald test            = 175.3  on 10 df,   p=<2e-16
Score (logrank) test = 186.9  on 10 df,   p=<2e-16

> 1-pchisq(2*(fit6$loglik[2]-fit7$loglik[2]),4)
[1] 0.1556166
> fit8<-coxph(Surv(os_time,os_event)~as.factor(PERF_STA)+as.factor(PR_RAD)+as.factor(B_SYM)+as.factor(r_score)+as.factor(pr_resp),data = dat)
> summary(fit8)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA) + 
    as.factor(PR_RAD) + as.factor(B_SYM) + as.factor(r_score) + 
    as.factor(pr_resp), data = dat)

  n= 619, number of events= 409 

                          coef exp(coef) se(coef)      z Pr(>|z|)    
as.factor(PERF_STA)1    0.4047    1.4988   0.1157  3.496 0.000472 ***
as.factor(PERF_STA)2    0.3058    1.3577   0.1859  1.645 0.099993 .  
as.factor(PERF_STA)3    0.5822    1.7900   0.2734  2.130 0.033196 *  
as.factor(PR_RAD)Y      0.2936    1.3413   0.1158  2.535 0.011241 *  
as.factor(B_SYM)Y       0.3185    1.3751   0.1038  3.068 0.002155 ** 
as.factor(r_score)0, 1 -0.8506    0.4271   0.1362 -6.244 4.27e-10 ***
as.factor(r_score)2    -0.2050    0.8146   0.1287 -1.593 0.111235    
as.factor(pr_resp)DU>1 -0.9948    0.3698   0.1435 -6.931 4.17e-12 ***
as.factor(pr_resp)SDPD  0.2635    1.3015   0.1125  2.342 0.019174 *  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

                       exp(coef) exp(-coef) lower .95 upper .95
as.factor(PERF_STA)1      1.4988     0.6672    1.1946    1.8805
as.factor(PERF_STA)2      1.3577     0.7366    0.9431    1.9544
as.factor(PERF_STA)3      1.7900     0.5587    1.0475    3.0587
as.factor(PR_RAD)Y        1.3413     0.7456    1.0689    1.6831
as.factor(B_SYM)Y         1.3751     0.7272    1.1219    1.6854
as.factor(r_score)0, 1    0.4271     2.3412    0.3270    0.5579
as.factor(r_score)2       0.8146     1.2275    0.6330    1.0484
as.factor(pr_resp)DU>1    0.3698     2.7043    0.2791    0.4899
as.factor(pr_resp)SDPD    1.3015     0.7683    1.0439    1.6227

Concordance= 0.714  (se = 0.012 )
Likelihood ratio test= 188.7  on 9 df,   p=<2e-16
Wald test            = 172  on 9 df,   p=<2e-16
Score (logrank) test = 183.7  on 9 df,   p=<2e-16

> 1-pchisq(2*(fit7$loglik[2]-fit8$loglik[2]),1)
[1] 0.1062229
> fit9<-coxph(Surv(os_time,os_event)~as.factor(PERF_STA)+as.factor(B_SYM)+as.factor(r_score)+as.factor(pr_resp),data = dat)
> summary(fit9)
Call:
coxph(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA) + 
    as.factor(B_SYM) + as.factor(r_score) + as.factor(pr_resp), 
    data = dat)

  n= 619, number of events= 409 

                          coef exp(coef) se(coef)      z Pr(>|z|)    
as.factor(PERF_STA)1    0.4011    1.4934   0.1161  3.456 0.000548 ***
as.factor(PERF_STA)2    0.3239    1.3825   0.1859  1.743 0.081397 .  
as.factor(PERF_STA)3    0.5967    1.8161   0.2730  2.185 0.028854 *  
as.factor(B_SYM)Y       0.3164    1.3722   0.1037  3.050 0.002285 ** 
as.factor(r_score)0, 1 -0.8585    0.4238   0.1362 -6.304 2.89e-10 ***
as.factor(r_score)2    -0.2137    0.8076   0.1282 -1.667 0.095553 .  
as.factor(pr_resp)DU>1 -0.9316    0.3939   0.1410 -6.609 3.87e-11 ***
as.factor(pr_resp)SDPD  0.2490    1.2827   0.1122  2.220 0.026438 *  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

                       exp(coef) exp(-coef) lower .95 upper .95
as.factor(PERF_STA)1      1.4934     0.6696    1.1896    1.8749
as.factor(PERF_STA)2      1.3825     0.7233    0.9604    1.9901
as.factor(PERF_STA)3      1.8161     0.5506    1.0635    3.1014
as.factor(B_SYM)Y         1.3722     0.7288    1.1197    1.6815
as.factor(r_score)0, 1    0.4238     2.3595    0.3245    0.5535
as.factor(r_score)2       0.8076     1.2383    0.6281    1.0383
as.factor(pr_resp)DU>1    0.3939     2.5385    0.2988    0.5193
as.factor(pr_resp)SDPD    1.2827     0.7796    1.0296    1.5982

Concordance= 0.711  (se = 0.012 )
Likelihood ratio test= 182.5  on 8 df,   p=<2e-16
Wald test            = 164.7  on 8 df,   p=<2e-16
Score (logrank) test = 176.7  on 8 df,   p=<2e-16

> 1-pchisq(2*(fit8$loglik[2]-fit9$loglik[2]),1)
[1] 0.01313057
> fit.km <-survfit(Surv(os_time, os_event)~trt, data=dat)
> plot(fit.km,xlab="Time", ylab="Estimated SurvivalProbability")
> fit.km1<-survfit(Surv(os_time,os_event)~ PERF_STA,data = dat)
> fit.km2<-survfit(Surv(os_time,os_event)~ PR_RAD, data = dat)
> fit.km3<-survfit(Surv(os_time,os_event)~ B_SYM,data = dat)
> fit.km4<-survfit(Surv(os_time,os_event)~ r_score,data = dat)
> fit.km5<-survfit(Surv(os_time,os_event)~ pr_resp,data = dat)
> plot(fit.km1,xlab="Time", ylab="Estimated SurvivalProbability")
> plot(fit.km2,xlab="Time", ylab="Estimated SurvivalProbability")
> plot(fit.km3,xlab="Time", ylab="Estimated SurvivalProbability")
> text(100,0.2,"Y")
> text(100,0.5,"N")
> plot(fit.km4,xlab="Time", ylab="Estimated SurvivalProbability")
> text(100,0.15,">=3" )
> text(100,0.4,"2" )
> text(100,0.6,"0, 1" )
> plot(fit.km5,xlab="Time", ylab="Estimated SurvivalProbability")
> text(100,0.15,"SDPD")
> text(100,0.35,"DU<1")
> text(100,0.6,"DU>1")
> logrk1<-survdiff(Surv(os_time,os_event)~as.factor(PERF_STA),data = dat)
> logrk0<-survdiff(Surv(os_time,os_event)~as.factor(trt),data = dat)
> logrk0
Call:
survdiff(formula = Surv(os_time, os_event) ~ as.factor(trt), 
    data = dat)

                           N Observed Expected (O-E)^2/E (O-E)^2/V
as.factor(trt)=control   309      201      202    0.0105    0.0208
as.factor(trt)=treatment 310      208      207    0.0103    0.0208

 Chisq= 0  on 1 degrees of freedom, p= 0.9 

> logrk1
Call:
survdiff(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA), 
    data = dat)

                        N Observed Expected (O-E)^2/E (O-E)^2/V
as.factor(PERF_STA)=0 257      133   209.50      27.9      58.0
as.factor(PERF_STA)=1 278      208   163.86      11.9      20.0
as.factor(PERF_STA)=2  64       51    28.33      18.1      19.6
as.factor(PERF_STA)=3  20       17     7.31      12.8      13.1

 Chisq= 71.7  on 3 degrees of freedom, p= 2e-15

> logrk2<-survdiff(Surv(os_time,os_event)~as.factor(PR_RAD),data = dat)
> logrk2
Call:
survdiff(formula = Surv(os_time, os_event) ~ as.factor(PR_RAD), 
    data = dat)

                      N Observed Expected (O-E)^2/E (O-E)^2/V
as.factor(PR_RAD)=N 467      302      305    0.0343     0.136
as.factor(PR_RAD)=Y 152      107      104    0.1009     0.136

 Chisq= 0.1  on 1 degrees of freedom, p= 0.7 
> logrk3<-survdiff(Surv(os_time,os_event)~as.factor(B_SYM),data = dat)
> logrk3
Call:
survdiff(formula = Surv(os_time, os_event) ~ as.factor(B_SYM), 
    data = dat)

                     N Observed Expected (O-E)^2/E (O-E)^2/V
as.factor(B_SYM)=N 393      241      285      6.86      22.8
as.factor(B_SYM)=Y 226      168      124     15.80      22.8

 Chisq= 22.8  on 1 degrees of freedom, p= 2e-06 
> logrk4<-survdiff(Surv(os_time,os_event)~as.factor(r_score),data = dat)
> logrk4
Call:
survdiff(formula = Surv(os_time, os_event) ~ as.factor(r_score), 
    data = dat)

                          N Observed Expected (O-E)^2/E (O-E)^2/V
as.factor(r_score)=>=3  211      170      105    39.489    53.665
as.factor(r_score)=0, 1 230      115      187    27.919    52.134
as.factor(r_score)=2    178      124      116     0.521     0.731

 Chisq= 68.8  on 2 degrees of freedom, p= 1e-15 
> logrk5<-survdiff(Surv(os_time,os_event)~as.factor(pr_resp),data = dat)
> logrk5
Call:
survdiff(formula = Surv(os_time, os_event) ~ as.factor(pr_resp), 
    data = dat)

                          N Observed Expected (O-E)^2/E (O-E)^2/V
as.factor(pr_resp)=DU<1 261      188    165.9      2.94      4.96
as.factor(pr_resp)=DU>1 165       71    147.7     39.86     63.63
as.factor(pr_resp)=SDPD 193      150     95.3     31.33     41.42

 Chisq= 75.8  on 2 degrees of freedom, p= <2e-16 

> delta<-dat$os_event
> x<-dat$os_time
> PS<-dat$PERF_STA
> PR<-dat$PR_RAD
> BS<-dat$B_SYM
> rs<-dat$r_score
> pr_resp<-dat$pr_resp
> PERF_STA<-dat$PERF_STA
> AGE<-dat$AGE
> STAGE<-dat$STAGE
> SEX<-dat$SEX
> B_SYM<-dat$B_SYM
> r_score<-dat$r_score
> PR_RAD<-dat$PR_RAD
> pr_drug<-dat$pr_drug
> pr_resp<-dat$pr_resp
> trt<-dat$trt
> plot(PS[delta==1], log(x[delta==1]),pch=4,xlab="performance status: 0, 1, 2,3", ylab="log time")
> points(PS[delta==0], log(x[delta==0]),pch=1)
> plot(AGE[delta==1], log(x[delta==1]),pch=4,xlab="age in year", ylab="log time")
> points(AGE[delta==0], log(x[delta==0]),pch=1)
> plot(STAGE[delta==1], log(x[delta==1]),pch=4,xlab="cancer stage; I, II, III", ylab="log time")
> points(STAGE[delta==0], log(x[delta==0]),pch=1)
> plot(SEX[delta==1], log(x[delta==1]),pch=4,xlab="Female vs male", ylab="log time")
> plot(SEX[delta==1], log(x[delta==1]),pch=4,xlab="cancer stage; I, II, III", ylab="log time")
> points(SEX[delta==0], log(x[delta==0]),pch=1)
> plot(SEX[delta==1], log(x[delta==1]),pch=4,xlab="Female vs male", ylab="log time")
> points(SEX[delta==0], log(x[delta==0]),pch=1)
> plot(B_SYM[delta==1], log(x[delta==1]),pch=4,xlab="B-symptom, Yes vs No", ylab="log time")
> points(B_SYM[delta==0], log(x[delta==0]),pch=1)
> plot(r_score[delta==1], log(x[delta==1]),pch=4,xlab="International rIPI score: 0 or 1 vs 2 vs 3 or more", ylab="log time")
> points(r_score[delta==0], log(x[delta==0]),pch=1)
> plot(PR_RAD[delta==1], log(x[delta==1]),pch=4,xlab="Received radiotherapy before randomization", ylab="log time")
> points(PR_RAD[delta==0], log(x[delta==0]),pch=1)
> plot(PR_RAD[delta==1], log(x[delta==1]),xlab="Received radiotherapy before randomization", ylab="log time")
> plot(pr_drug[delta==1], log(x[delta==1]),pch=4,xlab="Received other drug before randomization", ylab="log time")
> points(pr_drug[delta==0], log(x[delta==0]),pch=1)
> plot(pr_resp[delta==1], log(x[delta==1]),pch=4,xlab="Response to other treatments before randomization", ylab="log time")
> points(pr_resp[delta==0], log(x[delta==0]),pch=1)
> plot(trt[delta==1], log(x[delta==1]),pch=4,xlab="treatment vs control", ylab="log time")
> points(trt[delta==0], log(x[delta==0]),pch=1)
> summary(fit.km)
Call: survfit(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA) + 
    as.factor(PR_RAD) + as.factor(B_SYM) + as.factor(r_score) + 
    as.factor(pr_resp), data = dat)

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.78     12       1    0.917  0.0798        0.773        1.000
  6.31     11       1    0.833  0.1076        0.647        1.000
 10.58     10       1    0.750  0.1250        0.541        1.000
 12.48      9       1    0.667  0.1361        0.447        0.995
 17.94      8       1    0.583  0.1423        0.362        0.941
 29.83      7       1    0.500  0.1443        0.284        0.880
 60.39      5       1    0.400  0.1461        0.196        0.818
 64.72      4       1    0.300  0.1396        0.120        0.747

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
  9.1      7       1    0.857   0.132        0.633            1
 41.6      6       1    0.714   0.171        0.447            1
 71.7      4       1    0.536   0.201        0.257            1
 81.3      3       1    0.357   0.198        0.121            1

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 28.8      3       1    0.667   0.272       0.2995            1
 30.1      2       1    0.333   0.272       0.0673            1

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.98     38       1    0.974  0.0260        0.924        1.000
  4.53     37       1    0.947  0.0362        0.879        1.000
  6.77     36       1    0.921  0.0437        0.839        1.000
  6.87     35       1    0.895  0.0498        0.802        0.998
  9.46     34       1    0.868  0.0548        0.767        0.983
 10.12     33       1    0.842  0.0592        0.734        0.966
 14.88     31       1    0.815  0.0632        0.700        0.949
 15.24     30       1    0.788  0.0667        0.667        0.930
 15.80     29       1    0.761  0.0697        0.636        0.910
 15.97     28       1    0.733  0.0723        0.605        0.890
 16.20     27       1    0.706  0.0745        0.574        0.869
 16.23     26       1    0.679  0.0765        0.545        0.847
 16.46     25       1    0.652  0.0781        0.516        0.824
 16.69     24       1    0.625  0.0794        0.487        0.802
 21.06     23       1    0.598  0.0805        0.459        0.778
 28.95     22       1    0.570  0.0813        0.431        0.754
 29.77     20       1    0.542  0.0821        0.403        0.729
 29.83     19       1    0.513  0.0825        0.375        0.704
 31.64     18       1    0.485  0.0827        0.347        0.677
 31.93     17       1    0.456  0.0826        0.320        0.651
 44.65     16       1    0.428  0.0823        0.294        0.624
 57.00     13       1    0.395  0.0822        0.263        0.594
 58.32     11       1    0.359  0.0822        0.229        0.562
 75.20     10       1    0.323  0.0815        0.197        0.530

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.81     27       1    0.963  0.0363        0.894        1.000
 10.81     24       1    0.923  0.0525        0.825        1.000
 16.23     23       1    0.883  0.0637        0.766        1.000
 45.96     21       1    0.841  0.0733        0.709        0.997
 49.77     19       1    0.796  0.0817        0.651        0.974

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=SDPD 
   time n.risk n.event survival std.err lower 95% CI upper 95% CI
   5.39     18       1    0.944  0.0540        0.844        1.000
   6.04     17       1    0.889  0.0741        0.755        1.000
  10.32     16       1    0.833  0.0878        0.678        1.000
  11.11     15       1    0.778  0.0980        0.608        0.996
  45.60     13       1    0.718  0.1072        0.536        0.962
  78.36      7       1    0.615  0.1321        0.404        0.937
 130.07      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.07     16       1    0.938  0.0605        0.826        1.000
  5.98     15       1    0.875  0.0827        0.727        1.000
  6.01     14       1    0.812  0.0976        0.642        1.000
  9.33     13       1    0.750  0.1083        0.565        0.995
 10.51     12       1    0.688  0.1159        0.494        0.957
 11.70     11       1    0.625  0.1210        0.428        0.914
 16.00     10       1    0.562  0.1240        0.365        0.867
 18.73      9       1    0.500  0.1250        0.306        0.816
 26.81      8       1    0.438  0.1240        0.251        0.763
 36.50      7       1    0.375  0.1210        0.199        0.706
 41.76      6       1    0.312  0.1159        0.151        0.646

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  9.43     12       1    0.917  0.0798        0.773            1
 38.70     11       1    0.833  0.1076        0.647            1
 42.61     10       1    0.750  0.1250        0.541            1

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  4.57     11       1    0.909  0.0867       0.7541        1.000
  5.16     10       1    0.818  0.1163       0.6192        1.000
  5.91      9       1    0.727  0.1343       0.5064        1.000
  6.11      8       1    0.636  0.1450       0.4071        0.995
  8.05      7       1    0.545  0.1501       0.3180        0.936
  8.08      6       1    0.455  0.1501       0.2379        0.868
  9.36      5       1    0.364  0.1450       0.1664        0.795
  9.92      4       1    0.273  0.1343       0.1039        0.716
 11.60      3       1    0.182  0.1163       0.0519        0.637

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.17      2       1      0.5   0.354        0.125            1
 10.41      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
     time n.risk n.event survival std.err lower 95% CI upper 95% CI

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 1.25      3       1    0.667   0.272          0.3            1
 3.22      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.38     15       1    0.933  0.0644        0.815        1.000
  4.80     14       1    0.867  0.0878        0.711        1.000
  7.26     13       1    0.800  0.1033        0.621        1.000
  7.62     12       1    0.733  0.1142        0.540        0.995
 11.99     11       1    0.667  0.1217        0.466        0.953
 67.84      9       1    0.593  0.1288        0.387        0.907

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
       4.632        3.000        1.000        0.667        0.272 
lower 95% CI upper 95% CI 
       0.300        1.000 

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.35      9       1    0.889   0.105        0.706        1.000
  5.65      8       1    0.778   0.139        0.549        1.000
  6.77      7       1    0.667   0.157        0.420        1.000
  6.96      6       1    0.556   0.166        0.310        0.997
  7.20      5       1    0.444   0.166        0.214        0.923
 41.36      4       1    0.333   0.157        0.132        0.840

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  6.31      6       1    0.833   0.152        0.583            1
  8.15      5       1    0.667   0.192        0.379            1
 13.54      3       1    0.444   0.222        0.167            1

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
       8.476        4.000        1.000        0.750        0.217 
lower 95% CI upper 95% CI 
       0.426        1.000 

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  9.49      3       1    0.667   0.272          0.3            1
 13.44      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
   time n.risk n.event survival std.err lower 95% CI upper 95% CI
   3.98      6       1    0.833   0.152        0.583            1
   4.40      5       1    0.667   0.192        0.379            1
  14.88      4       1    0.500   0.204        0.225            1
  27.07      3       1    0.333   0.192        0.108            1
 102.47      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  4.37      9       1    0.889   0.105       0.7056        1.000
  7.03      8       1    0.778   0.139       0.5485        1.000
 10.64      7       1    0.667   0.157       0.4200        1.000
 17.15      6       1    0.556   0.166       0.3097        0.997
 19.15      5       1    0.444   0.166       0.2141        0.923
 30.88      4       1    0.333   0.157       0.1323        0.840
 87.06      2       1    0.167   0.142       0.0315        0.882

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  8.15     17       1    0.941  0.0571        0.836        1.000
  9.33     16       1    0.882  0.0781        0.742        1.000
 42.78     15       1    0.824  0.0925        0.661        1.000
 57.86     13       1    0.760  0.1048        0.580        0.996
 68.07     11       1    0.691  0.1159        0.498        0.960

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  5.09      5       1      0.8   0.179        0.516            1
  7.39      4       1      0.6   0.219        0.293            1
 53.09      3       1      0.4   0.219        0.137            1
 89.10      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 22.0     10       1    0.900  0.0949        0.732            1
 39.9      8       1    0.787  0.1340        0.564            1
 69.1      7       1    0.675  0.1551        0.430            1

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  5.82      3       1    0.667   0.272       0.2995            1
  9.79      2       1    0.333   0.272       0.0673            1
 13.70      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
 0.394      2       1      0.5   0.354        0.125            1
 8.378      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
        47.2          1.0          1.0          0.0          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
        time       n.risk      n.event     survival      std.err 
      10.645        2.000        1.000        0.500        0.354 
lower 95% CI upper 95% CI 
       0.125        1.000 

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU<1 
        time       n.risk      n.event     survival      std.err 
      30.127        3.000        1.000        0.667        0.272 
lower 95% CI upper 95% CI 
       0.300        1.000 

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
      15.606        2.000        1.000        0.500        0.354 
lower 95% CI upper 95% CI 
       0.125        1.000 

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  5.06      2       1      0.5   0.354        0.125            1
 33.91      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=0, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 10.5      2       1      0.5   0.354        0.125            1
 31.9      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
    time n.risk n.event survival std.err lower 95% CI upper 95% CI
   0.953     16       1   0.9375  0.0605       0.8261        1.000
   1.906     15       1   0.8750  0.0827       0.7271        1.000
   2.891     14       1   0.8125  0.0976       0.6421        1.000
   4.402     13       1   0.7500  0.1083       0.5652        0.995
   5.060     12       1   0.6875  0.1159       0.4941        0.957
   5.947     11       1   0.6250  0.1210       0.4276        0.914
   6.045     10       1   0.5625  0.1240       0.3651        0.867
   7.228      9       1   0.5000  0.1250       0.3063        0.816
   9.101      8       1   0.4375  0.1240       0.2510        0.763
   9.429      7       1   0.3750  0.1210       0.1992        0.706
  12.386      6       1   0.3125  0.1159       0.1511        0.646
  12.780      5       1   0.2500  0.1083       0.1070        0.584
  60.649      3       1   0.1667  0.0992       0.0519        0.535
 100.008      2       1   0.0833  0.0770       0.0136        0.510

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  5.29      9       1    0.889   0.105        0.706            1
 11.70      8       1    0.778   0.139        0.549            1

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  1.91     12       1   0.9167  0.0798       0.7729        1.000
  2.63     11       1   0.8333  0.1076       0.6470        1.000
  2.76     10       1   0.7500  0.1250       0.5410        1.000
  3.75      9       1   0.6667  0.1361       0.4468        0.995
  3.84      8       1   0.5833  0.1423       0.3616        0.941
  4.34      7       1   0.5000  0.1443       0.2840        0.880
  5.78      6       1   0.4167  0.1423       0.2133        0.814
  7.16      5       1   0.3333  0.1361       0.1498        0.742
  8.21      4       1   0.2500  0.1250       0.0938        0.666
  9.92      3       1   0.1667  0.1076       0.0470        0.591
 10.09      2       1   0.0833  0.0798       0.0128        0.544
 32.76      1       1   0.0000     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  1.22     17       1    0.941  0.0571        0.836        1.000
  3.94     16       1    0.882  0.0781        0.742        1.000
  4.17     15       1    0.824  0.0925        0.661        1.000
  5.82     14       1    0.765  0.1029        0.587        0.995
  8.38     13       1    0.706  0.1105        0.519        0.959
  8.57     12       1    0.647  0.1159        0.455        0.919
 12.88     11       1    0.588  0.1194        0.395        0.876
 13.86     10       1    0.529  0.1211        0.338        0.829
 26.74      9       1    0.471  0.1211        0.284        0.779
 38.11      8       1    0.412  0.1194        0.233        0.727

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
       6.965        4.000        1.000        0.750        0.217 
lower 95% CI upper 95% CI 
       0.426        1.000 

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.35     14       1    0.929  0.0688        0.803        1.000
  4.47     13       1    0.857  0.0935        0.692        1.000
  5.78     12       1    0.786  0.1097        0.598        1.000
  6.64     11       1    0.714  0.1207        0.513        0.995
  7.69     10       1    0.643  0.1281        0.435        0.950
  8.05      9       1    0.571  0.1323        0.363        0.899
  8.90      8       1    0.500  0.1336        0.296        0.844
 24.08      7       1    0.429  0.1323        0.234        0.785

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.06     23       1    0.957  0.0425        0.877        1.000
  3.52     22       1    0.913  0.0588        0.805        1.000
  5.95     21       1    0.870  0.0702        0.742        1.000
  6.50     20       1    0.826  0.0790        0.685        0.996
  6.54     19       1    0.783  0.0860        0.631        0.971
  7.13     18       1    0.739  0.0916        0.580        0.942
  7.46     17       1    0.696  0.0959        0.531        0.912
  7.52     16       1    0.652  0.0993        0.484        0.879
  7.92     15       1    0.609  0.1018        0.439        0.845
  9.27     14       2    0.522  0.1042        0.353        0.772
 10.71     12       1    0.478  0.1042        0.312        0.733
 11.70     11       1    0.435  0.1034        0.273        0.693
 57.89      8       1    0.380  0.1038        0.223        0.649
 58.22      7       1    0.326  0.1022        0.176        0.603

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
   time n.risk n.event survival std.err lower 95% CI upper 95% CI
  0.526      6       1    0.833   0.152       0.5827        1.000
  9.199      5       1    0.667   0.192       0.3786        1.000
 10.678      4       1    0.500   0.204       0.2246        1.000
 53.290      3       1    0.333   0.192       0.1075        1.000
 66.924      2       1    0.167   0.152       0.0278        0.997
 98.234      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  1.81     16       1   0.9375  0.0605      0.82609        1.000
  2.14     15       1   0.8750  0.0827      0.72707        1.000
  5.22     14       1   0.8125  0.0976      0.64209        1.000
  5.55     13       1   0.7500  0.1083      0.56520        0.995
  5.62     12       1   0.6875  0.1159      0.49409        0.957
  6.18     11       1   0.6250  0.1210      0.42761        0.914
  6.80     10       1   0.5625  0.1240      0.36513        0.867
  8.05      9       1   0.5000  0.1250      0.30632        0.816
  8.08      8       1   0.4375  0.1240      0.25101        0.763
  8.28      7       1   0.3750  0.1210      0.19921        0.706
  8.31      6       2   0.2500  0.1083      0.10699        0.584
  9.79      4       1   0.1875  0.0976      0.06761        0.520
 14.59      3       1   0.1250  0.0827      0.03419        0.457
 20.63      2       1   0.0625  0.0605      0.00937        0.417

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
   time n.risk n.event survival std.err lower 95% CI upper 95% CI
  0.953     10       1      0.9  0.0949       0.7320        1.000
  3.483      9       1      0.8  0.1265       0.5868        1.000
  4.435      8       1      0.7  0.1449       0.4665        1.000
  4.731      7       1      0.6  0.1549       0.3617        0.995
  5.421      6       1      0.5  0.1581       0.2690        0.929
  5.552      5       1      0.4  0.1549       0.1872        0.855
  9.462      4       1      0.3  0.1449       0.1164        0.773
 10.645      3       1      0.2  0.1265       0.0579        0.691
 11.828      2       1      0.1  0.0949       0.0156        0.642

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.63      7       1    0.857   0.132       0.6334            1
  6.64      6       1    0.714   0.171       0.4471            1
 27.20      4       1    0.536   0.201       0.2570            1
 32.16      3       1    0.357   0.198       0.1205            1
 76.25      2       1    0.179   0.160       0.0307            1

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.27     20       1     0.95  0.0487       0.8591        1.000
  2.53     19       1     0.90  0.0671       0.7777        1.000
  2.60     18       1     0.85  0.0798       0.7071        1.000
  2.63     17       1     0.80  0.0894       0.6426        0.996
  2.83     16       1     0.75  0.0968       0.5823        0.966
  2.89     15       1     0.70  0.1025       0.5254        0.933
  4.14     14       1     0.65  0.1067       0.4712        0.897
  4.66     13       1     0.60  0.1095       0.4195        0.858
  5.52     12       1     0.55  0.1112       0.3700        0.818
  5.65     11       1     0.50  0.1118       0.3226        0.775
  6.31     10       1     0.45  0.1112       0.2772        0.731
  6.47      9       1     0.40  0.1095       0.2339        0.684
  6.90      8       1     0.35  0.1067       0.1926        0.636
  8.02      7       1     0.30  0.1025       0.1536        0.586
  8.08      6       1     0.25  0.0968       0.1170        0.534
  9.13      5       1     0.20  0.0894       0.0832        0.481
  9.36      4       1     0.15  0.0798       0.0528        0.426
 12.32      3       1     0.10  0.0671       0.0269        0.372

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.07     11       1    0.909  0.0867        0.754        1.000
  4.14     10       1    0.818  0.1163        0.619        1.000
  7.69      9       1    0.727  0.1343        0.506        1.000
  7.82      8       1    0.636  0.1450        0.407        0.995
  9.49      7       1    0.545  0.1501        0.318        0.936
 11.27      6       1    0.455  0.1501        0.238        0.868
 23.06      5       1    0.364  0.1450        0.166        0.795
 63.11      4       1    0.273  0.1343        0.104        0.716

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU>1 
     time n.risk n.event survival std.err lower 95% CI upper 95% CI

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  1.84     15       1    0.933  0.0644        0.815        1.000
  3.15     14       1    0.867  0.0878        0.711        1.000
  3.19     13       1    0.800  0.1033        0.621        1.000
  5.88     12       1    0.733  0.1142        0.540        0.995
  5.91     11       1    0.667  0.1217        0.466        0.953
  6.37      9       1    0.593  0.1288        0.387        0.907
  9.33      8       1    0.519  0.1323        0.314        0.855
 77.60      5       1    0.415  0.1407        0.213        0.807

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.20     11       1   0.9091  0.0867       0.7541        1.000
  3.42     10       1   0.8182  0.1163       0.6192        1.000
  4.40      9       1   0.7273  0.1343       0.5064        1.000
  5.88      8       1   0.6364  0.1450       0.4071        0.995
  6.34      7       1   0.5455  0.1501       0.3180        0.936
  8.31      6       1   0.4545  0.1501       0.2379        0.868
  8.97      5       1   0.3636  0.1450       0.1664        0.795
 11.14      4       1   0.2727  0.1343       0.1039        0.716
 26.09      3       1   0.1818  0.1163       0.0519        0.637
 76.09      2       1   0.0909  0.0867       0.0140        0.589
 93.37      1       1   0.0000     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  1.84      7       1    0.857   0.132       0.6334        1.000
  5.95      6       1    0.714   0.171       0.4471        1.000
 16.76      5       1    0.571   0.187       0.3008        1.000
 39.33      4       1    0.429   0.187       0.1822        1.000
 55.79      3       1    0.286   0.171       0.0886        0.922

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
   time n.risk n.event survival std.err lower 95% CI upper 95% CI
  0.986     11       1   0.9091  0.0867       0.7541        1.000
  2.694     10       1   0.8182  0.1163       0.6192        1.000
  3.055      9       1   0.7273  0.1343       0.5064        1.000
  3.483      8       1   0.6364  0.1450       0.4071        0.995
  3.713      7       1   0.5455  0.1501       0.3180        0.936
  3.975      6       1   0.4545  0.1501       0.2379        0.868
  4.764      5       1   0.3636  0.1450       0.1664        0.795
  5.585      4       1   0.2727  0.1343       0.1039        0.716
  5.881      3       1   0.1818  0.1163       0.0519        0.637
  6.177      2       1   0.0909  0.0867       0.0140        0.589
 80.066      1       1   0.0000     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.23     10       1      0.9  0.0949       0.7320        1.000
  3.48      9       1      0.8  0.1265       0.5868        1.000
  4.76      8       1      0.7  0.1449       0.4665        1.000
  6.21      7       1      0.6  0.1549       0.3617        0.995
  6.60      6       1      0.5  0.1581       0.2690        0.929
 10.88      5       1      0.4  0.1549       0.1872        0.855
 13.70      4       1      0.3  0.1449       0.1164        0.773
 15.34      3       1      0.2  0.1265       0.0579        0.691
 15.44      2       1      0.1  0.0949       0.0156        0.642
 21.16      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.06      3       1    0.667   0.272       0.2995            1
 20.50      2       1    0.333   0.272       0.0673            1
 62.62      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
        time       n.risk      n.event     survival      std.err 
       0.789        1.000        1.000        0.000          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.30      6       1    0.833   0.152       0.5827        1.000
  7.03      5       1    0.667   0.192       0.3786        1.000
 15.38      4       1    0.500   0.204       0.2246        1.000
 15.51      3       1    0.333   0.192       0.1075        1.000
 22.64      2       1    0.167   0.152       0.0278        0.997

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU>1 
     time n.risk n.event survival std.err lower 95% CI upper 95% CI

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=SDPD 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 5.55      5       1      0.8   0.179       0.5161            1
 6.47      4       1      0.6   0.219       0.2933            1
 6.83      3       1      0.4   0.219       0.1367            1
 7.10      2       1      0.2   0.179       0.0346            1

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  5.98      5       1      0.8   0.179        0.516            1
  9.63      4       1      0.6   0.219        0.293            1
 15.90      3       1      0.4   0.219        0.137            1

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
     time n.risk n.event survival std.err lower 95% CI upper 95% CI

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 4.60      2       1      0.5   0.354        0.125            1
 9.33      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 2.10      3       1    0.667   0.272       0.2995            1
 8.87      2       1    0.333   0.272       0.0673            1
 9.63      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.35      4       1     0.75   0.217       0.4259            1
  4.07      3       1     0.50   0.250       0.1877            1
 14.19      2       1     0.25   0.217       0.0458            1

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.33      3       1    0.667   0.272       0.2995            1
  3.94      2       1    0.333   0.272       0.0673            1
 17.51      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  5.95      4       1     0.75   0.217       0.4259            1
  7.69      3       1     0.50   0.250       0.1877            1
 20.96      2       1     0.25   0.217       0.0458            1
 25.33      1       1     0.00     NaN           NA           NA

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
        51.8          1.0          1.0          0.0          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=0, 1, as.factor(pr_resp)=SDPD 
        time       n.risk      n.event     survival      std.err 
        7.62         1.00         1.00         0.00          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  3.19      8       1    0.875   0.117        0.673        1.000
 13.50      7       1    0.750   0.153        0.503        1.000
 14.03      6       1    0.625   0.171        0.365        1.000
 25.20      5       1    0.500   0.177        0.250        1.000
 37.98      4       1    0.375   0.171        0.153        0.917
 70.97      2       1    0.188   0.158        0.036        0.976

                as.factor(PERF_STA)=1, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
        time       n.risk      n.event     survival      std.err 
        4.21         1.00         1.00         0.00          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 4.11      5       1      0.8   0.179       0.5161            1
 5.03      4       1      0.6   0.219       0.2933            1
 5.88      3       1      0.4   0.219       0.1367            1
 7.56      2       1      0.2   0.179       0.0346            1

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  5.88      3       1    0.667   0.272       0.2995            1
 20.34      2       1    0.333   0.272       0.0673            1

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  1.22      9       1    0.889   0.105       0.7056        1.000
  2.69      8       1    0.778   0.139       0.5485        1.000
  4.40      7       1    0.667   0.157       0.4200        1.000
  7.39      6       1    0.556   0.166       0.3097        0.997
  8.84      5       1    0.444   0.166       0.2141        0.923
  9.76      4       1    0.333   0.157       0.1323        0.840
 10.38      3       1    0.222   0.139       0.0655        0.754

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=0, 1, as.factor(pr_resp)=SDPD 
     time n.risk n.event survival std.err lower 95% CI upper 95% CI

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
        time       n.risk      n.event     survival      std.err 
        13.3          1.0          1.0          0.0          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 3.68      2       1      0.5   0.354        0.125            1
 8.31      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
 0.099      9       1    0.889   0.105       0.7056        1.000
 1.051      8       1    0.778   0.139       0.5485        1.000
 2.103      7       1    0.667   0.157       0.4200        1.000
 2.628      6       1    0.556   0.166       0.3097        0.997
 4.074      5       1    0.444   0.166       0.2141        0.923
 5.684      4       1    0.333   0.157       0.1323        0.840
 5.749      3       1    0.222   0.139       0.0655        0.754

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
      14.949        2.000        1.000        0.500        0.354 
lower 95% CI upper 95% CI 
       0.125        1.000 

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
   time n.risk n.event survival std.err lower 95% CI upper 95% CI
  0.657     11       1   0.9091  0.0867       0.7541        1.000
  3.023     10       1   0.8182  0.1163       0.6192        1.000
  3.220      9       1   0.7273  0.1343       0.5064        1.000
  3.515      8       1   0.6364  0.1450       0.4071        0.995
  3.548      7       1   0.5455  0.1501       0.3180        0.936
  4.402      6       1   0.4545  0.1501       0.2379        0.868
  5.060      5       1   0.3636  0.1450       0.1664        0.795
  5.125      4       1   0.2727  0.1343       0.1039        0.716
  6.407      3       1   0.1818  0.1163       0.0519        0.637
 11.302      2       1   0.0909  0.0867       0.0140        0.589

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
     time n.risk n.event survival std.err lower 95% CI upper 95% CI

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
        time       n.risk      n.event     survival      std.err 
        1.51         1.00         1.00         0.00          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  0.46      5       1    0.800   0.179       0.5161            1
  6.21      3       1    0.533   0.248       0.2142            1
 28.62      2       1    0.267   0.226       0.0507            1

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.37      4       1     0.75   0.217       0.4259            1
  3.81      3       1     0.50   0.250       0.1877            1
  5.49      2       1     0.25   0.217       0.0458            1
 20.89      1       1     0.00     NaN           NA           NA

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU>1 
     time n.risk n.event survival std.err lower 95% CI upper 95% CI

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 1.41      4       1     0.75   0.217       0.4259            1
 3.02      3       1     0.50   0.250       0.1877            1
 4.83      2       1     0.25   0.217       0.0458            1
 5.32      1       1     0.00     NaN           NA           NA

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  5.09      2       1      0.5   0.354        0.125            1
 34.07      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
   time n.risk n.event survival std.err lower 95% CI upper 95% CI
  0.329      2       1      0.5   0.354        0.125            1
 81.084      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=2, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
        time       n.risk      n.event     survival      std.err 
        1.77         1.00         1.00         0.00          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 1.25      4       1     0.75   0.217       0.4259            1
 2.43      3       1     0.50   0.250       0.1877            1
 7.03      2       1     0.25   0.217       0.0458            1

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
     time n.risk n.event survival std.err lower 95% CI upper 95% CI

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=N, as.factor(B_SYM)=N, as.factor(r_score)=2   , as.factor(pr_resp)=DU<1 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 1.71      2       1      0.5   0.354        0.125            1
 4.50      1       1      0.0     NaN           NA           NA

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU<1 
  time n.risk n.event survival std.err lower 95% CI upper 95% CI
  2.76      3       1    0.667   0.272       0.2995            1
  3.29      2       1    0.333   0.272       0.0673            1
 12.58      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
       0.723        2.000        1.000        0.500        0.354 
lower 95% CI upper 95% CI 
       0.125        1.000 

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
 time n.risk n.event survival std.err lower 95% CI upper 95% CI
 1.74      3       1    0.667   0.272       0.2995            1
 2.17      2       1    0.333   0.272       0.0673            1
 4.07      1       1    0.000     NaN           NA           NA

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=N, as.factor(B_SYM)=Y, as.factor(r_score)=2   , as.factor(pr_resp)=SDPD 
        time       n.risk      n.event     survival      std.err 
        5.16         1.00         1.00         0.00          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
        14.5          1.0          1.0          0.0          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=Y, as.factor(B_SYM)=N, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
        time       n.risk      n.event     survival      std.err 
        3.09         1.00         1.00         0.00          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=DU>1 
        time       n.risk      n.event     survival      std.err 
        4.89         1.00         1.00         0.00          NaN 
lower 95% CI upper 95% CI 
          NA           NA 

                as.factor(PERF_STA)=3, as.factor(PR_RAD)=Y, as.factor(B_SYM)=Y, as.factor(r_score)=>=3 , as.factor(pr_resp)=SDPD 
        time       n.risk      n.event     survival      std.err 
        28.9          1.0          1.0          0.0          NaN 
lower 95% CI upper 95% CI 
          NA           NA 
fit.lognm0<-survreg(Surv(os_time,os_event)~as.factor(PERF_STA)+AGE+as.factor(STAGE)+as.factor(SEX)+as.factor(PR_RAD)+as.factor(B_SYM)+as.factor(r_score)+as.factor(pr_resp)+as.factor(pr_drug)+as.factor(trt),data = dat,dist="lognormal")
> summary(fit.lognm0)

Call:
survreg(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA) + 
    AGE + as.factor(STAGE) + as.factor(SEX) + as.factor(PR_RAD) + 
    as.factor(B_SYM) + as.factor(r_score) + as.factor(pr_resp) + 
    as.factor(pr_drug) + as.factor(trt), data = dat, dist = "lognormal")
                           Value Std. Error     z       p
(Intercept)              3.57873    0.58495  6.12 9.5e-10
as.factor(PERF_STA)1    -0.59024    0.16287 -3.62 0.00029
as.factor(PERF_STA)2    -0.54899    0.27493 -2.00 0.04585
as.factor(PERF_STA)3    -1.04034    0.40651 -2.56 0.01049
AGE                     -0.00665    0.00705 -0.94 0.34524
as.factor(STAGE)II      -0.34465    0.29722 -1.16 0.24622
as.factor(STAGE)III      0.38865    0.33107  1.17 0.24043
as.factor(STAGE)IV       0.07644    0.33015  0.23 0.81691
as.factor(SEX)M         -0.06814    0.14494 -0.47 0.63827
as.factor(PR_RAD)Y      -0.40800    0.16830 -2.42 0.01534
as.factor(B_SYM)Y       -0.48875    0.14866 -3.29 0.00101
as.factor(r_score)0, 1   1.42048    0.26555  5.35 8.8e-08
as.factor(r_score)2      0.32459    0.19602  1.66 0.09773
as.factor(pr_resp)DU>1   1.44228    0.19302  7.47 7.9e-14
as.factor(pr_resp)SDPD  -0.30296    0.16376 -1.85 0.06430
as.factor(pr_drug)Y     -0.30808    0.15793 -1.95 0.05109
as.factor(trt)treatment  0.04862    0.13974  0.35 0.72788
Log(scale)               0.48305    0.03748 12.89 < 2e-16

Scale= 1.62 

Log Normal distribution
Loglik(model)= -1815.7   Loglik(intercept only)= -1927.8
	Chisq= 224.03 on 16 degrees of freedom, p= 1.1e-38 
Number of Newton-Raphson Iterations: 4 
n= 619 
> fit.lognm7<-survreg(Surv(os_time,os_event)~as.factor(PERF_STA)+as.factor(PR_RAD)+as.factor(B_SYM)+as.factor(r_score)+as.factor(pr_resp)+as.factor(pr_drug),data = dat,dist="lognormal")
> summary(fit.lognm7)

Call:
survreg(formula = Surv(os_time, os_event) ~ as.factor(PERF_STA) + 
    as.factor(PR_RAD) + as.factor(B_SYM) + as.factor(r_score) + 
    as.factor(pr_resp) + as.factor(pr_drug), data = dat, dist = "lognormal")
                         Value Std. Error     z       p
(Intercept)             3.3992     0.2479 13.71 < 2e-16
as.factor(PERF_STA)1   -0.6040     0.1635 -3.69 0.00022
as.factor(PERF_STA)2   -0.6074     0.2743 -2.21 0.02681
as.factor(PERF_STA)3   -1.0961     0.4083 -2.68 0.00726
as.factor(PR_RAD)Y     -0.4284     0.1680 -2.55 0.01078
as.factor(B_SYM)Y      -0.4766     0.1492 -3.19 0.00140
as.factor(r_score)0, 1  1.1797     0.1921  6.14 8.2e-10
as.factor(r_score)2     0.3297     0.1866  1.77 0.07728
as.factor(pr_resp)DU>1  1.4217     0.1930  7.37 1.7e-13
as.factor(pr_resp)SDPD -0.3136     0.1637 -1.92 0.05538
as.factor(pr_drug)Y    -0.3502     0.1581 -2.22 0.02676
Log(scale)              0.4917     0.0375 13.11 < 2e-16

Scale= 1.64 

Log Normal distribution
Loglik(model)= -1821.1   Loglik(intercept only)= -1927.8
	Chisq= 213.25 on 10 degrees of freedom, p= 2.8e-40 
Number of Newton-Raphson Iterations: 4 
n= 619 

> 1-pchisq(2*((-1815.7)-(-1821.1)),16-10)
[1] 0.09475787
> fit.resids7<-resid(fit.lognm7, type="deviance")
> par(mfrow=c(1,2))
> plot(predict(fit.lognm7),fit.resids7,ylab="Deviance Residuals",xlab="Risk Score")
> qqnorm(fit.resids7,ylab="Deviance Residuals",xlab="N(0,1) Quantiles")
> abline(0,1)


```
