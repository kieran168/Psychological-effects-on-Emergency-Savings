Mental well-being and emergency savings
================
Kieran Yuen

### Loading in Data

## Means (simple graphs, correlations, differences of means)

### Preliminary Multicollinearity Check

    ## [1] 0.224398

    ## [1] 0.2320714

    ## [1] 0.2251923

    ## [1] 0.2378071

    ## [1] 0.268183

    ## [1] 0.2598679

    ## [1] 0.2284568

    ## [1] 0.6698352

    ## [1] 0.380633

    ## [1] 0.3905643

## Preliminary data preparation

### Create new columns of data

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

### Subsetting data

### Recoding Ind. Variables in Subsetted Database

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

## Simple Regressions

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ ConfidenceObj + AgeGroup + Gender + 
    ##     Race + MaritalStatus + DepChildren + EducationLevel + Income + 
    ##     Employement + FinancesObj + AnxietyObj + DebtObj, family = binomial, 
    ##     data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.8047  -0.7375  -0.2991   0.7433   2.6525  
    ## 
    ## Coefficients:
    ##                                Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)                     0.63473    0.09024   7.034 2.01e-12 ***
    ## ConfidenceObjModConfidence      0.38282    0.04460   8.583  < 2e-16 ***
    ## ConfidenceObjLowConfidence      0.68198    0.06443  10.584  < 2e-16 ***
    ## AgeGroup25-34                  -0.14810    0.06509  -2.275 0.022895 *  
    ## AgeGroup35-44                   0.06771    0.06697   1.011 0.311969    
    ## AgeGroup45-54                   0.14309    0.06618   2.162 0.030614 *  
    ## AgeGroup55-64                  -0.15597    0.06594  -2.365 0.018019 *  
    ## AgeGroup65+                    -0.46988    0.06946  -6.765 1.34e-11 ***
    ## GenderFemale                    0.08665    0.03331   2.602 0.009275 ** 
    ## RaceNon-White                  -0.03512    0.03785  -0.928 0.353469    
    ## MaritalStatusNot Married        0.06984    0.03772   1.852 0.064063 .  
    ## DepChildrenNo                  -0.20377    0.03879  -5.254 1.49e-07 ***
    ## EducationLevelSome College     -0.21170    0.04138  -5.116 3.12e-07 ***
    ## EducationLevelCollege Graduate -0.56776    0.04844 -11.720  < 2e-16 ***
    ## EducationLevelAdvancedDeg      -0.58735    0.05935  -9.896  < 2e-16 ***
    ## Income$25,000-$50,000          -0.54758    0.05057 -10.829  < 2e-16 ***
    ## Income$50,000-$100,000         -0.95619    0.05220 -18.319  < 2e-16 ***
    ## Income$100,000+                -1.27283    0.06417 -19.834  < 2e-16 ***
    ## EmployementUnemployed           0.10879    0.03949   2.755 0.005865 ** 
    ## FinancesObjModFinCond           1.06255    0.04036  26.326  < 2e-16 ***
    ## FinancesObjLowFinCond           2.18829    0.05328  41.068  < 2e-16 ***
    ## AnxietyObjModAnxiety           -0.15928    0.04466  -3.567 0.000362 ***
    ## AnxietyObjLowAnxiety           -0.40755    0.04278  -9.528  < 2e-16 ***
    ## DebtObjModDebt                 -0.46534    0.04830  -9.634  < 2e-16 ***
    ## DebtObjLowDebt                 -1.20082    0.03884 -30.915  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 34355  on 24828  degrees of freedom
    ## Residual deviance: 23527  on 24804  degrees of freedom
    ##   (1029 observations deleted due to missingness)
    ## AIC: 23577
    ## 
    ## Number of Fisher Scoring iterations: 5

    ##                    GVIF Df GVIF^(1/(2*Df))
    ## ConfidenceObj  1.116856  2        1.028015
    ## AgeGroup       1.852139  5        1.063573
    ## Gender         1.051232  1        1.025296
    ## Race           1.076630  1        1.037608
    ## MaritalStatus  1.359691  1        1.166058
    ## DepChildren    1.355707  1        1.164348
    ## EducationLevel 1.186241  3        1.028874
    ## Income         1.550071  3        1.075784
    ## Employement    1.424598  1        1.193565
    ## FinancesObj    1.198781  2        1.046369
    ## AnxietyObj     1.233070  2        1.053773
    ## DebtObj        1.243654  2        1.056027

    ##                    (Intercept)     ConfidenceObjModConfidence 
    ##                      1.8865202                      1.4664139 
    ##     ConfidenceObjLowConfidence                  AgeGroup25-34 
    ##                      1.9777837                      0.8623471 
    ##                  AgeGroup35-44                  AgeGroup45-54 
    ##                      1.0700565                      1.1538289 
    ##                  AgeGroup55-64                    AgeGroup65+ 
    ##                      0.8555853                      0.6250790 
    ##                   GenderFemale                  RaceNon-White 
    ##                      1.0905168                      0.9654920 
    ##       MaritalStatusNot Married                  DepChildrenNo 
    ##                      1.0723382                      0.8156486 
    ##     EducationLevelSome College EducationLevelCollege Graduate 
    ##                      0.8092072                      0.5667949 
    ##      EducationLevelAdvancedDeg          Income$25,000-$50,000 
    ##                      0.5558006                      0.5783460 
    ##         Income$50,000-$100,000                Income$100,000+ 
    ##                      0.3843558                      0.2800381 
    ##          EmployementUnemployed          FinancesObjModFinCond 
    ##                      1.1149334                      2.8937295 
    ##          FinancesObjLowFinCond           AnxietyObjModAnxiety 
    ##                      8.9199528                      0.8527571 
    ##           AnxietyObjLowAnxiety                 DebtObjModDebt 
    ##                      0.6652786                      0.6279247 
    ##                 DebtObjLowDebt 
    ##                      0.3009483

## Complicated Regressions

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ ConfidenceObj + AgeGroup + Gender + 
    ##     Race + MaritalStatus + DepChildren + EducationLevel + Income + 
    ##     Employement + FinancesObj + AnxietyObj + DebtObj + ConfidenceObj:FinancesObj, 
    ##     family = binomial, data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.7374  -0.7377  -0.2934   0.7330   2.6667  
    ## 
    ## Coefficients:
    ##                                                  Estimate Std. Error z value
    ## (Intercept)                                       0.58208    0.09112   6.388
    ## ConfidenceObjModConfidence                        0.66910    0.11634   5.751
    ## ConfidenceObjLowConfidence                        1.24930    0.17499   7.139
    ## AgeGroup25-34                                    -0.13961    0.06501  -2.148
    ## AgeGroup35-44                                     0.07210    0.06691   1.077
    ## AgeGroup45-54                                     0.14692    0.06613   2.222
    ## AgeGroup55-64                                    -0.14979    0.06591  -2.273
    ## AgeGroup65+                                      -0.46323    0.06944  -6.671
    ## GenderFemale                                      0.08275    0.03335   2.481
    ## RaceNon-White                                    -0.03626    0.03786  -0.958
    ## MaritalStatusNot Married                          0.07037    0.03775   1.864
    ## DepChildrenNo                                    -0.20437    0.03881  -5.265
    ## EducationLevelSome College                       -0.20909    0.04139  -5.052
    ## EducationLevelCollege Graduate                   -0.56880    0.04849 -11.731
    ## EducationLevelAdvancedDeg                        -0.58757    0.05943  -9.886
    ## Income$25,000-$50,000                            -0.54448    0.05056 -10.770
    ## Income$50,000-$100,000                           -0.95188    0.05221 -18.233
    ## Income$100,000+                                  -1.26893    0.06420 -19.765
    ## EmployementUnemployed                             0.10824    0.03949   2.741
    ## FinancesObjModFinCond                             1.10906    0.04387  25.279
    ## FinancesObjLowFinCond                             2.31674    0.06240  37.130
    ## AnxietyObjModAnxiety                             -0.16130    0.04470  -3.609
    ## AnxietyObjLowAnxiety                             -0.40259    0.04284  -9.398
    ## DebtObjModDebt                                   -0.46697    0.04833  -9.663
    ## DebtObjLowDebt                                   -1.20098    0.03887 -30.899
    ## ConfidenceObjModConfidence:FinancesObjModFinCond -0.30485    0.12833  -2.375
    ## ConfidenceObjLowConfidence:FinancesObjModFinCond -0.51263    0.19751  -2.595
    ## ConfidenceObjModConfidence:FinancesObjLowFinCond -0.43585    0.14820  -2.941
    ## ConfidenceObjLowConfidence:FinancesObjLowFinCond -0.83354    0.19999  -4.168
    ##                                                  Pr(>|z|)    
    ## (Intercept)                                      1.68e-10 ***
    ## ConfidenceObjModConfidence                       8.86e-09 ***
    ## ConfidenceObjLowConfidence                       9.37e-13 ***
    ## AgeGroup25-34                                    0.031739 *  
    ## AgeGroup35-44                                    0.281258    
    ## AgeGroup45-54                                    0.026311 *  
    ## AgeGroup55-64                                    0.023045 *  
    ## AgeGroup65+                                      2.54e-11 ***
    ## GenderFemale                                     0.013085 *  
    ## RaceNon-White                                    0.338166    
    ## MaritalStatusNot Married                         0.062340 .  
    ## DepChildrenNo                                    1.40e-07 ***
    ## EducationLevelSome College                       4.37e-07 ***
    ## EducationLevelCollege Graduate                    < 2e-16 ***
    ## EducationLevelAdvancedDeg                         < 2e-16 ***
    ## Income$25,000-$50,000                             < 2e-16 ***
    ## Income$50,000-$100,000                            < 2e-16 ***
    ## Income$100,000+                                   < 2e-16 ***
    ## EmployementUnemployed                            0.006131 ** 
    ## FinancesObjModFinCond                             < 2e-16 ***
    ## FinancesObjLowFinCond                             < 2e-16 ***
    ## AnxietyObjModAnxiety                             0.000308 ***
    ## AnxietyObjLowAnxiety                              < 2e-16 ***
    ## DebtObjModDebt                                    < 2e-16 ***
    ## DebtObjLowDebt                                    < 2e-16 ***
    ## ConfidenceObjModConfidence:FinancesObjModFinCond 0.017529 *  
    ## ConfidenceObjLowConfidence:FinancesObjModFinCond 0.009446 ** 
    ## ConfidenceObjModConfidence:FinancesObjLowFinCond 0.003272 ** 
    ## ConfidenceObjLowConfidence:FinancesObjLowFinCond 3.07e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 34355  on 24828  degrees of freedom
    ## Residual deviance: 23503  on 24800  degrees of freedom
    ##   (1029 observations deleted due to missingness)
    ## AIC: 23561
    ## 
    ## Number of Fisher Scoring iterations: 5

    ##                                      (Intercept) 
    ##                                        1.7897532 
    ##                       ConfidenceObjModConfidence 
    ##                                        1.9524788 
    ##                       ConfidenceObjLowConfidence 
    ##                                        3.4878856 
    ##                                    AgeGroup25-34 
    ##                                        0.8696955 
    ##                                    AgeGroup35-44 
    ##                                        1.0747604 
    ##                                    AgeGroup45-54 
    ##                                        1.1582577 
    ##                                    AgeGroup55-64 
    ##                                        0.8608861 
    ##                                      AgeGroup65+ 
    ##                                        0.6292477 
    ##                                     GenderFemale 
    ##                                        1.0862732 
    ##                                    RaceNon-White 
    ##                                        0.9643900 
    ##                         MaritalStatusNot Married 
    ##                                        1.0729041 
    ##                                    DepChildrenNo 
    ##                                        0.8151645 
    ##                       EducationLevelSome College 
    ##                                        0.8113226 
    ##                   EducationLevelCollege Graduate 
    ##                                        0.5662061 
    ##                        EducationLevelAdvancedDeg 
    ##                                        0.5556740 
    ##                            Income$25,000-$50,000 
    ##                                        0.5801440 
    ##                           Income$50,000-$100,000 
    ##                                        0.3860158 
    ##                                  Income$100,000+ 
    ##                                        0.2811316 
    ##                            EmployementUnemployed 
    ##                                        1.1143136 
    ##                            FinancesObjModFinCond 
    ##                                        3.0315002 
    ##                            FinancesObjLowFinCond 
    ##                                       10.1425844 
    ##                             AnxietyObjModAnxiety 
    ##                                        0.8510350 
    ##                             AnxietyObjLowAnxiety 
    ##                                        0.6685874 
    ##                                   DebtObjModDebt 
    ##                                        0.6268976 
    ##                                   DebtObjLowDebt 
    ##                                        0.3009003 
    ## ConfidenceObjModConfidence:FinancesObjModFinCond 
    ##                                        0.7372345 
    ## ConfidenceObjLowConfidence:FinancesObjModFinCond 
    ##                                        0.5989189 
    ## ConfidenceObjModConfidence:FinancesObjLowFinCond 
    ##                                        0.6467154 
    ## ConfidenceObjLowConfidence:FinancesObjLowFinCond 
    ##                                        0.4345096

# Tables for Paper

    ## EmergencyFund
    ##         1         0 
    ## 0.5192204 0.4807796

    ## FinancesObj
    ## HighFinCond  ModFinCond  LowFinCond 
    ##   0.3250176   0.4175217   0.2574606

    ## AnxietyObj
    ## HighAnxiety  ModAnxiety  LowAnxiety 
    ##   0.5387045   0.1734196   0.2878758

    ## StressObj
    ## HighStress  ModStress  LowStress 
    ##  0.4431734  0.1932612  0.3635654

    ## DebtObj
    ##  HighDebt   ModDebt   LowDebt 
    ## 0.3839094 0.1470806 0.4690100

    ## ConfidenceObj
    ## HighConfidence  ModConfidence  LowConfidence 
    ##      0.7381356      0.1616321      0.1002324

    ## EducationLevel
    ## Less than College      Some College  College Graduate       AdvancedDeg 
    ##         0.2709026         0.3755898         0.2200480         0.1334597

    ## Gender
    ##      Male    Female 
    ## 0.4419909 0.5580091

    ## Race
    ##     White Non-White 
    ## 0.7439477 0.2560523

    ## MaritalStatus
    ##     Married Not Married 
    ##   0.5355403   0.4644597

    ## DepChildren
    ##       Yes        No 
    ## 0.3548225 0.6451775

    ## Employement
    ##   Employed Unemployed 
    ##    0.56381    0.43619

    ## Income
    ## Less than $25,000   $25,000-$50,000  $50,000-$100,000         $100,000+ 
    ##         0.2112306         0.2518370         0.3392374         0.1976951

    ## AgeGroup
    ##      18-24      25-34      35-44      45-54      55-64        65+ 
    ## 0.09954366 0.17170702 0.16683425 0.17263516 0.18373424 0.20554567
