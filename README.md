Models I have Developed:
1. Since the task is to classify different accents, a logistic regression model has been selected as the classification algorithm. The first step in this approach is to develop separate logistic regression models for each accent category, including ES, FR, GE, IT, UK, and US.
> setwd("C:\\Users\\mpalthya\\Downloads")
> data<-read.csv("accent-mfcc-data-1.csv",sep=",")
>dim(data)
[1] 329  13
#Language=ES
> ES<- as.factor(data$language=="ES")
> M_logis1 <- glm(ES~X1+X2+X3+X4+X5+X6+X7+X8+X9+X10+X11+X12, family =binomial, data = data)
> summary(M_logis1)

Call:
glm(formula = ES ~ X1 + X2 + X3 + X4 + X5 + X6 + X7 + X8 + X9 + 
    X10 + X11 + X12, family = binomial, data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-2.23754  -0.06066  -0.01367  -0.00126   2.86195  

Coefficients:
             Estimate Std. Error z value Pr(>|z|)    
(Intercept) -55.91683   14.91070  -3.750 0.000177 ***
X1            0.01197    0.25534   0.047 0.962620    
X2           -0.14503    0.25400  -0.571 0.568026    
X3           -0.31836    0.31333  -1.016 0.309608    
X4            1.11702    0.37416   2.985 0.002832 ** 
X5           -1.04941    0.42202  -2.487 0.012896 *  
X6            1.28702    0.42134   3.055 0.002254 ** 
X7           -1.55859    0.46801  -3.330 0.000868 ***
X8            1.03036    0.37916   2.717 0.006578 ** 
X9           -0.98593    0.41767  -2.361 0.018249 *  
X10          -0.69467    0.27955  -2.485 0.012958 *  
X11          -0.46760    0.33035  -1.415 0.156934    
X12           0.73523    0.27998   2.626 0.008640 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 196.233  on 328  degrees of freedom
Residual deviance:  43.374  on 316  degrees of freedom
AIC: 69.374

Number of Fisher Scoring iterations: 11

> P_logis <- predict(M_logis1, newdata = data, type = "response")
> C_logis <- rep(0, length(ES))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, ES)
> C
       ES
C_logis FALSE TRUE
      0   298    5
      1     2   24
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9787234

#REDUCED MODEL FOR LANGAUGE ES
> M_logis1R<- glm(ES~X4+X5+X6+X7+X8+X9+X10+X12, family =binomial, data = data)
> summary(M_logis1R)

Call:
glm(formula = ES ~ X4 + X5 + X6 + X7 + X8 + X9 + X10 + X12, family = binomial, 
    data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-2.60210  -0.07506  -0.01838  -0.00191   2.63839  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept) -48.3068    10.2787  -4.700 2.61e-06 ***
X4            0.9045     0.2546   3.552 0.000382 ***
X5           -0.9297     0.2283  -4.073 4.64e-05 ***
X6            1.0236     0.2713   3.773 0.000161 ***
X7           -1.2658     0.3255  -3.889 0.000101 ***
X8            0.6462     0.2422   2.669 0.007617 ** 
X9           -0.6050     0.2648  -2.284 0.022343 *  
X10          -0.8333     0.2415  -3.451 0.000559 ***
X12           0.5546     0.1901   2.917 0.003532 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 196.233  on 328  degrees of freedom
Residual deviance:  46.001  on 320  degrees of freedom
AIC: 64.001

Number of Fisher Scoring iterations: 10

> P_logis <- predict(M_logis1R, newdata = data, type = "response")
> C_logis <- rep(0, length(ES))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, ES)
> C
       ES
C_logis FALSE TRUE
      0   297    6
      1     3   23
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9726444
> AIC(M_logis1,M_logis1R)
          df      AIC
M_logis1  13 69.37381
M_logis1R  9 64.00139
> BIC(M_logis1,M_logis1R)
          df       BIC
M_logis1  13 118.72256
M_logis1R  9  98.16591


Model-ES	AIC	BIC	ACCURACY(%)
Original(12)	69.37381	118.72256	97.872
Reduced()	64.00139	98.16591	97.26

Upon examining the accuracy of language ES, it was observed that the accuracy is approximately 97%, indicating that detecting this language is not very challenging. As a result, the developed model is able to accurately detect the language with an accuracy of 97%.

LANGUAGE=FR
> M_logis2<- glm(FR~X1+X2+X3+X4+X5+X7+X8+X9+X10+X11+X12, family =binomial, data = data)
> summary(M_logis2)

Call:
glm(formula = FR ~ X1 + X2 + X3 + X4 + X5 + X7 + X8 + X9 + X10 + 
    X11 + X12, family = binomial, data = data)

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-1.8428  -0.2790  -0.1491  -0.0447   2.9520  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept) -5.83054    3.05129  -1.911 0.056024 .  
X1          -0.36535    0.10159  -3.596 0.000323 ***
X2          -0.31109    0.10559  -2.946 0.003217 ** 
X3           0.05515    0.13649   0.404 0.686189    
X4           0.05595    0.12492   0.448 0.654223    
X5          -0.57811    0.14412  -4.011 6.04e-05 ***
X7           0.63764    0.18875   3.378 0.000729 ***
X8           0.58391    0.16845   3.466 0.000527 ***
X9           0.30866    0.14983   2.060 0.039384 *  
X10          0.18896    0.13525   1.397 0.162353    
X11          0.32235    0.15769   2.044 0.040928 *  
X12         -0.35397    0.12048  -2.938 0.003303 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 200.87  on 328  degrees of freedom
Residual deviance: 118.44  on 317  degrees of freedom
AIC: 142.44

Number of Fisher Scoring iterations: 8

> P_logis <- predict(M_logis2, newdata = data, type = "response")
> C_logis <- rep(0, length(FR))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, FR)
> C
       FR
C_logis FALSE TRUE
      0   295   21
      1     4    9
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9240122
REDUCED MODEL FR
> M_logis2R<- glm(FR~X1+X2+X5+X7+X8+X9+X11+X12, family =binomial, data = data)
> summary(M_logis2R)

Call:
glm(formula = FR ~ X1 + X2 + X5 + X7 + X8 + X9 + X11 + X12, family = binomial, 
    data = data)

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-1.9824  -0.2901  -0.1495  -0.0445   2.8965  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept) -4.63607    2.04235  -2.270 0.023210 *  
X1          -0.40084    0.09955  -4.026 5.66e-05 ***
X2          -0.33335    0.08536  -3.905 9.41e-05 ***
X5          -0.52373    0.12946  -4.045 5.22e-05 ***
X7           0.69719    0.16600   4.200 2.67e-05 ***
X8           0.53588    0.14757   3.631 0.000282 ***
X9           0.32336    0.15009   2.154 0.031207 *  
X11          0.29454    0.16013   1.839 0.065858 .  
X12         -0.39317    0.12202  -3.222 0.001272 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 200.87  on 328  degrees of freedom
Residual deviance: 120.52  on 320  degrees of freedom
AIC: 138.52

Number of Fisher Scoring iterations: 8

> P_logis <- predict(M_logis2R, newdata = data, type = "response")
> C_logis <- rep(0, length(FR))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, FR)
> C
       FR
C_logis FALSE TRUE
      0   295   21
      1     4    9
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9240122
> AIC(M_logis2,M_logis2R)
          df      AIC
M_logis2  12 142.4397
M_logis2R  9 138.5204
> BIC(M_logis2,M_logis2R)
          df      BIC
M_logis2  12 187.9924
M_logis2R  9 172.6849

Model FR	AIC	BIC	ACCURACY(%)
ORGINAL(12)	142.4397	187.9924	92.401
REDUCED(8)	138.5204	172.6849	92.40122

It was observed that the accuracy of detecting language FR is approximately 92%, indicating that it is not very challenging to detect this language. Therefore, the developed model can accurately detect the language with an accuracy of 92%.

LANGUAGE=GE
> GE<- as.factor(data$language=="GE")
> M_logis3 <- glm(GE~X1+X2+X3+X4+X5+X6+X7+X8+X9+X10+X11+X12, family =binomial, data = data)
> summary(M_logis3)

Call:
glm(formula = GE ~ X1 + X2 + X3 + X4 + X5 + X6 + X7 + X8 + X9 + 
    X10 + X11 + X12, family = binomial, data = data)

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-1.6216  -0.2258  -0.0830  -0.0273   3.3983  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept) -5.55095    4.64915  -1.194 0.232489    
X1           0.13495    0.10350   1.304 0.192273    
X2           0.51768    0.16165   3.203 0.001362 ** 
X3          -0.07126    0.17258  -0.413 0.679699    
X4          -0.63789    0.17330  -3.681 0.000233 ***
X5           0.10257    0.15573   0.659 0.510117    
X6           0.16402    0.18696   0.877 0.380322    
X7          -0.62298    0.27170  -2.293 0.021856 *  
X8          -0.11773    0.19267  -0.611 0.541169    
X9           0.30357    0.24063   1.262 0.207110    
X10          0.08059    0.18528   0.435 0.663581    
X11          0.38933    0.20690   1.882 0.059864 .  
X12         -0.06252    0.16928  -0.369 0.711873    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 200.869  on 328  degrees of freedom
Residual deviance:  92.577  on 316  degrees of freedom
AIC: 118.58

Number of Fisher Scoring iterations: 8

> P_logis <- predict(M_logis3, newdata = data, type = "response")
> C_logis <- rep(0, length(GE))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, GE)
> C
       GE
C_logis FALSE TRUE
      0   296   12
      1     3   18
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9544073
# REDUCED MODEL FOR GE
> M_logis3R<- glm(GE~X2+X4+X7+X11, family =binomial, data = data)
> summary(M_logis3R)

Call:
glm(formula = GE ~ X2 + X4 + X7 + X11, family = binomial, data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-1.70180  -0.27506  -0.13580  -0.03645   3.01677  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept) -7.42570    1.60920  -4.615 3.94e-06 ***
X2           0.39532    0.09367   4.220 2.44e-05 ***
X4          -0.41225    0.09895  -4.166 3.10e-05 ***
X7          -0.71388    0.16192  -4.409 1.04e-05 ***
X11          0.41564    0.15122   2.749  0.00599 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 200.87  on 328  degrees of freedom
Residual deviance: 107.88  on 324  degrees of freedom
AIC: 117.88

Number of Fisher Scoring iterations: 7

> P_logis <- predict(M_logis3R, newdata = data, type = "response")
> C_logis <- rep(0, length(GE))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, GE)
> C
       GE
C_logis FALSE TRUE
      0   295   14
      1     4   16
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9452888
> AIC(M_logis3,M_logis3R)
          df      AIC
M_logis3  13 118.5769
M_logis3R  5 117.8806
> BIC(M_logis3,M_logis3R)
          df      BIC
M_logis3  13 167.9257
M_logis3R  5 136.8609
MODEL-GE	AIC	BIC	ACCURACY(%)
ORGINAL(12)	118.5769	167.9257	94.44073

REDUCED(4)	117.8806	136.8609	94.52888

Upon examining the accuracy of language GE, it was found to be around 94%, suggesting that detecting this language is not too difficult. The developed model is capable of detecting the language with a high degree of accuracy, achieving a 94% accuracy rate. It is worth noting that the accuracy of detecting language GE is 2% higher compared to language FR.
Language=-IT
> IT<- as.factor(data$language=="IT")
> M_logis4 <- glm(IT~X1+X2+X3+X4+X5+X6+X7+X8+X9+X10+X11+X12, family =binomial, data = data)
> summary(M_logis4)

Call:
glm(formula = IT ~ X1 + X2 + X3 + X4 + X5 + X6 + X7 + X8 + X9 + 
    X10 + X11 + X12, family = binomial, data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-2.13908  -0.25061  -0.07095  -0.00893   2.69389  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept) -25.5978     6.1998  -4.129 3.65e-05 ***
X1           -0.5676     0.1446  -3.926 8.63e-05 ***
X2            0.1627     0.1442   1.128 0.259199    
X3           -0.3543     0.1751  -2.024 0.042986 *  
X4            0.6744     0.1830   3.685 0.000228 ***
X5           -0.8372     0.2137  -3.917 8.96e-05 ***
X6            1.0130     0.2323   4.361 1.30e-05 ***
X7           -0.8341     0.2727  -3.058 0.002226 ** 
X8           -0.1894     0.2086  -0.908 0.363967    
X9           -1.0737     0.2784  -3.857 0.000115 ***
X10           0.3597     0.1714   2.099 0.035796 *  
X11          -0.3485     0.1977  -1.763 0.077939 .  
X12           0.3637     0.1679   2.166 0.030275 *  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 200.87  on 328  degrees of freedom
Residual deviance: 101.88  on 316  degrees of freedom
AIC: 127.88

Number of Fisher Scoring iterations: 9

> P_logis <- predict(M_logis4, newdata = data, type = "response")
> C_logis <- rep(0, length(IT))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, IT)
> C
       IT
C_logis FALSE TRUE
      0   290   16
      1     9   14
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9240122
REDUCED MODEL IT
> M_logis4R<- glm(IT~X1+X3+X4+X5+X6+X7+X9+X10+X11+X12, family =binomial, data = data)
> summary(M_logis4R)

Call:
glm(formula = IT ~ X1 + X3 + X4 + X5 + X6 + X7 + X9 + X10 + X11 + 
    X12, family = binomial, data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-2.08534  -0.24168  -0.07712  -0.01147   2.68470  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept) -27.9231     5.5521  -5.029 4.92e-07 ***
X1           -0.5989     0.1284  -4.663 3.11e-06 ***
X3           -0.4868     0.1409  -3.455 0.000550 ***
X4            0.7282     0.1780   4.091 4.29e-05 ***
X5           -0.8969     0.2056  -4.362 1.29e-05 ***
X6            1.0748     0.2245   4.788 1.68e-06 ***
X7           -0.8535     0.2535  -3.367 0.000759 ***
X9           -1.0905     0.2761  -3.950 7.82e-05 ***
X10           0.3677     0.1672   2.199 0.027844 *  
X11          -0.4533     0.1682  -2.695 0.007033 ** 
X12           0.3761     0.1578   2.383 0.017180 *  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 200.87  on 328  degrees of freedom
Residual deviance: 103.49  on 318  degrees of freedom
AIC: 125.49

Number of Fisher Scoring iterations: 9

> P_logis <- predict(M_logis4R, newdata = data, type = "response")
> C_logis <- rep(0, length(IT))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, IT)
> C
       IT
C_logis FALSE TRUE
      0   291   16
      1     8   14
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9270517
> AIC(M_logis4,M_logis4R)
          df      AIC
M_logis4  13 127.8822
M_logis4R 11 125.4917
> BIC(M_logis4,M_logis4R)
          df      BIC
M_logis4  13 177.2309
M_logis4R 11 167.2483
MODEL IT	AIC	BIC	ACCURACY(%)
ORGINAL MODEL(12)	127.8822	177.2309	92.40122
REDUCED(10)	125.4917	167.2483	92.70517

Upon analyzing the accuracy of language IT, it was found to be around 92%, suggesting that detecting this language is not particularly challenging. The model that was developed is able to accurately detect the language with a 92% accuracy rate.


LANGAUGE=UK
> UK<- as.factor(data$language=="UK")
> M_logis5<- glm(UK~X1+X2+X3+X4+X5+X6+X7+X8+X9+X10+X11+X12, family =binomial, data = data)
> summary(M_logis5)

Call:
glm(formula = UK ~ X1 + X2 + X3 + X4 + X5 + X6 + X7 + X8 + X9 + 
    X10 + X11 + X12, family = binomial, data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-2.49149  -0.19348  -0.04856  -0.00286   2.32706  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept) 16.68554    7.66405   2.177 0.029472 *  
X1          -1.07690    0.25168  -4.279 1.88e-05 ***
X2          -0.44489    0.14821  -3.002 0.002685 ** 
X3          -0.20789    0.17635  -1.179 0.238458    
X4          -0.23330    0.19960  -1.169 0.242463    
X5           0.42768    0.26415   1.619 0.105438    
X6          -0.47605    0.23403  -2.034 0.041937 *  
X7           1.16639    0.33074   3.527 0.000421 ***
X8          -0.81726    0.25290  -3.232 0.001231 ** 
X9           0.91452    0.33274   2.748 0.005987 ** 
X10         -1.34112    0.27875  -4.811 1.50e-06 ***
X11         -0.09107    0.23511  -0.387 0.698493    
X12         -1.03599    0.23524  -4.404 1.06e-05 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 262.589  on 328  degrees of freedom
Residual deviance:  91.378  on 316  degrees of freedom
AIC: 117.38

Number of Fisher Scoring iterations: 11

> P_logis <- predict(M_logis5, newdata = data, type = "response")
> C_logis <- rep(0, length(UK))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, UK)
> C
       UK
C_logis FALSE TRUE
      0   277   17
      1     7   28
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9270517
REDUCED MODEL FOR UK
> M_logis5R <- glm(UK~X1+X2+X3+X7+X8+X9+X10+X12, family =binomial, data = data)
> summary(M_logis5R)

Call:
glm(formula = UK ~ X1 + X2 + X3 + X7 + X8 + X9 + X10 + X12, family = binomial, 
    data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-2.36995  -0.19161  -0.05178  -0.00005   2.22450  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept)   2.9780     2.4085   1.236 0.216297    
X1           -1.2778     0.2136  -5.983 2.19e-09 ***
X2           -0.5319     0.1402  -3.792 0.000149 ***
X3           -0.3994     0.1444  -2.766 0.005670 ** 
X7            0.8569     0.2391   3.584 0.000339 ***
X8           -0.6002     0.1631  -3.679 0.000234 ***
X9            0.8491     0.2542   3.341 0.000835 ***
X10          -1.3568     0.2281  -5.948 2.72e-09 ***
X12          -1.0951     0.2067  -5.297 1.18e-07 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 262.59  on 328  degrees of freedom
Residual deviance:  95.75  on 320  degrees of freedom
AIC: 113.75

Number of Fisher Scoring iterations: 9

> P_logis <- predict(M_logis5R, newdata = data, type = "response")
> C_logis <- rep(0, length(UK))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, UK)
> C
       UK
C_logis FALSE TRUE
      0   277   15
      1     7   30
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.9331307
> AIC(M_logis5,M_logis5R)
          df      AIC
M_logis5  13 117.3777
M_logis5R  9 113.7499
> BIC(M_logis5,M_logis5R)
          df      BIC
M_logis5  13 166.7265
M_logis5R  9 147.9144
Model-UK	AIC	BIC	ACCURACY(%)
ORGINAL MODEL(12)	117.3777	166.7625	92.70517
REDUCED(8)	113.7499	147.9144	93.31307

Upon analyzing the accuracy of language UK, it was found to be around 92%, indicating that detecting this language is not overly difficult. The developed model is capable of accurately detecting the language with an accuracy rate of 92%.
LANGUAGE=US
> US<- as.factor(data$language=="US")
> M_logis6<- glm(US~X1+X2+X3+X4+X5+X6+X7+X8+X9+X10+X11+X12, family =binomial, data = data)
> summary(M_logis6)

Call:
glm(formula = US ~ X1 + X2 + X3 + X4 + X5 + X6 + X7 + X8 + X9 + 
    X10 + X11 + X12, family = binomial, data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-2.25560  -0.71014   0.00005   0.59842   2.48821  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept)  8.11248    2.91239   2.786  0.00534 ** 
X1           0.38462    0.06658   5.777 7.62e-09 ***
X2           0.09803    0.07070   1.386  0.16562    
X3           0.26997    0.09222   2.928  0.00342 ** 
X4          -0.12142    0.08613  -1.410  0.15864    
X5           0.25908    0.10471   2.474  0.01335 *  
X6          -0.30651    0.10858  -2.823  0.00476 ** 
X7           0.10542    0.10548   0.999  0.31758    
X8          -0.30671    0.11167  -2.747  0.00602 ** 
X9           0.15983    0.11009   1.452  0.14654    
X10          0.46724    0.09106   5.131 2.88e-07 ***
X11          0.13640    0.09666   1.411  0.15819    
X12          0.19570    0.07299   2.681  0.00734 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 456.09  on 328  degrees of freedom
Residual deviance: 279.87  on 316  degrees of freedom
AIC: 305.87

Number of Fisher Scoring iterations: 8

> P_logis <- predict(M_logis6, newdata = data, type = "response")
> C_logis <- rep(0, length(US))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, US)
> C
       US
C_logis FALSE TRUE
      0   136   42
      1    28  123
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.787234
REDUCED MODEL US
> US<- as.factor(data$language=="US")
> M_logis6R<- glm(US~X1+X3+X5+X6+X8+X10+X12, family =binomial, data = data)
> summary(M_logis6R)

Call:
glm(formula = US ~ X1 + X3 + X5 + X6 + X8 + X10 + X12, family = binomial, 
    data = data)

Deviance Residuals: 
     Min        1Q    Median        3Q       Max  
-1.90303  -0.73478   0.00006   0.59270   2.38649  

Coefficients:
            Estimate Std. Error z value Pr(>|z|)    
(Intercept)  4.14047    1.39876   2.960 0.003075 ** 
X1           0.35973    0.05241   6.864 6.69e-12 ***
X3           0.14081    0.05627   2.502 0.012336 *  
X5           0.15065    0.07792   1.933 0.053204 .  
X6          -0.18694    0.08661  -2.159 0.030888 *  
X8          -0.16578    0.07921  -2.093 0.036365 *  
X10          0.52207    0.08345   6.256 3.94e-10 ***
X12          0.23085    0.06741   3.425 0.000615 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 456.09  on 328  degrees of freedom
Residual deviance: 284.09  on 321  degrees of freedom
AIC: 300.09

Number of Fisher Scoring iterations: 7

> P_logis <- predict(M_logis6R, newdata = data, type = "response")
> C_logis <- rep(0, length(US))
> C_logis[P_logis>0.5] <- 1
> C=table(C_logis, US)
> C
       US
C_logis FALSE TRUE
      0   135   44
      1    29  121
> accuracy <- sum(diag(C)) / sum(C)
> accuracy
[1] 0.7781155
> AIC(M_logis6,M_logis6R)
          df      AIC
M_logis6  13 305.8747
M_logis6R  8 300.0943
> BIC(M_logis6,M_logis6R)
          df      BIC
M_logis6  13 355.2234
M_logis6R  8 330.4628

Model-US	AIC	BIC	ACCURACY(%)
Original(12)	305.8747	355.2234	77.81155
Reduced(7)	300.0943	330.4628	77.81155

Upon analyzing the accuracy of language US, it was found to be around 77%, suggesting that detecting this language is more challenging compared to the other language models.


> AIC(M_logis1,M_logis2,M_logis3,M_logis4,M_logis5,M_logis6)
         df       AIC
M_logis1 13  69.37381
M_logis2 13 141.55428
M_logis3 13 118.57692
M_logis4 13 127.88219
M_logis5 13 117.37775
M_logis6 13 305.87467
> BIC(M_logis1,M_logis2,M_logis3,M_logis4,M_logis5,M_logis6)
         df      BIC
M_logis1 13 118.7226
M_logis2 13 190.9030
M_logis3 13 167.9257
M_logis4 13 177.2309
M_logis5 13 166.7265
M_logis6 13 355.2234
