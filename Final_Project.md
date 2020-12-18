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
    ##     Employement + FinancesObj + AnxietyObj + StressObj + DebtObj, 
    ##     family = binomial, data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.7851  -0.7348  -0.2979   0.7387   2.6510  
    ## 
    ## Coefficients:
    ##                                Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)                     0.84941    0.09994   8.499  < 2e-16 ***
    ## ConfidenceObjModConfidence      0.37086    0.04479   8.280  < 2e-16 ***
    ## ConfidenceObjLowConfidence      0.65404    0.06485  10.086  < 2e-16 ***
    ## AgeGroup25-34                  -0.14345    0.06558  -2.187  0.02872 *  
    ## AgeGroup35-44                   0.07275    0.06749   1.078  0.28110    
    ## AgeGroup45-54                   0.15969    0.06673   2.393  0.01671 *  
    ## AgeGroup55-64                  -0.12878    0.06659  -1.934  0.05312 .  
    ## AgeGroup65+                    -0.42696    0.07035  -6.069 1.29e-09 ***
    ## GenderFemale                    0.08277    0.03347   2.473  0.01339 *  
    ## RaceNon-White                  -0.04437    0.03803  -1.167  0.24331    
    ## MaritalStatusNot Married        0.06546    0.03784   1.730  0.08366 .  
    ## DepChildrenNo                  -0.20134    0.03901  -5.161 2.45e-07 ***
    ## EducationLevelSome College     -0.20199    0.04158  -4.858 1.19e-06 ***
    ## EducationLevelCollege Graduate -0.54938    0.04864 -11.294  < 2e-16 ***
    ## EducationLevelAdvancedDeg      -0.57448    0.05955  -9.647  < 2e-16 ***
    ## Income$Less than $25,000       -0.35833    0.07711  -4.647 3.37e-06 ***
    ## Income$25,000-$50,000          -0.73878    0.06678 -11.063  < 2e-16 ***
    ## Income$50,000-$100,000         -1.14455    0.06849 -16.711  < 2e-16 ***
    ## Income$100,000+                -1.46655    0.07837 -18.713  < 2e-16 ***
    ## EmployementUnemployed           0.09394    0.03978   2.361  0.01821 *  
    ## FinancesObjModFinCond           1.07667    0.04068  26.466  < 2e-16 ***
    ## FinancesObjLowFinCond           2.18744    0.05357  40.833  < 2e-16 ***
    ## AnxietyObjModAnxiety           -0.05880    0.05125  -1.147  0.25125    
    ## AnxietyObjLowAnxiety           -0.19713    0.05579  -3.533  0.00041 ***
    ## StressObjModStress             -0.11708    0.04954  -2.364  0.01810 *  
    ## StressObjLowStress             -0.30853    0.05218  -5.913 3.37e-09 ***
    ## DebtObjModDebt                 -0.45610    0.04863  -9.379  < 2e-16 ***
    ## DebtObjLowDebt                 -1.18310    0.03924 -30.154  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 34215  on 24730  degrees of freedom
    ## Residual deviance: 23355  on 24703  degrees of freedom
    ##   (1127 observations deleted due to missingness)
    ## AIC: 23411
    ## 
    ## Number of Fisher Scoring iterations: 5

    ##                    GVIF Df GVIF^(1/(2*Df))
    ## ConfidenceObj  1.119544  2        1.028633
    ## AgeGroup       1.888786  5        1.065659
    ## Gender         1.053324  1        1.026316
    ## Race           1.078638  1        1.038575
    ## MaritalStatus  1.357668  1        1.165190
    ## DepChildren    1.361550  1        1.166855
    ## EducationLevel 1.186660  3        1.028935
    ## Income         1.583414  4        1.059130
    ## Employement    1.432344  1        1.196806
    ## FinancesObj    1.207564  2        1.048281
    ## AnxietyObj     2.503748  2        1.257905
    ## StressObj      2.442942  2        1.250197
    ## DebtObj        1.267364  2        1.061024

    ##                    (Intercept)     ConfidenceObjModConfidence 
    ##                      2.3382693                      1.4489795 
    ##     ConfidenceObjLowConfidence                  AgeGroup25-34 
    ##                      1.9233047                      0.8663678 
    ##                  AgeGroup35-44                  AgeGroup45-54 
    ##                      1.0754597                      1.1731445 
    ##                  AgeGroup55-64                    AgeGroup65+ 
    ##                      0.8791711                      0.6524869 
    ##                   GenderFemale                  RaceNon-White 
    ##                      1.0862914                      0.9565965 
    ##       MaritalStatusNot Married                  DepChildrenNo 
    ##                      1.0676521                      0.8176338 
    ##     EducationLevelSome College EducationLevelCollege Graduate 
    ##                      0.8170993                      0.5773081 
    ##      EducationLevelAdvancedDeg       Income$Less than $25,000 
    ##                      0.5630003                      0.6988443 
    ##          Income$25,000-$50,000         Income$50,000-$100,000 
    ##                      0.4776948                      0.3183685 
    ##                Income$100,000+          EmployementUnemployed 
    ##                      0.2307212                      1.0984933 
    ##          FinancesObjModFinCond          FinancesObjLowFinCond 
    ##                      2.9349040                      8.9123809 
    ##           AnxietyObjModAnxiety           AnxietyObjLowAnxiety 
    ##                      0.9428958                      0.8210852 
    ##             StressObjModStress             StressObjLowStress 
    ##                      0.8895110                      0.7345266 
    ##                 DebtObjModDebt                 DebtObjLowDebt 
    ##                      0.6337497                      0.3063273

## Complicated Regressions

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ FinancesObj + AnxietyObj + StressObj + 
    ##     DebtObj + ConfidenceObj + StressObj:ConfidenceObj, family = binomial, 
    ##     data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.3904  -0.7883  -0.4166   0.8195   2.2305  
    ## 
    ## Coefficients:
    ##                                               Estimate Std. Error z value
    ## (Intercept)                                   -0.59002    0.04271 -13.814
    ## FinancesObjModFinCond                          1.19020    0.03896  30.553
    ## FinancesObjLowFinCond                          2.52906    0.05118  49.420
    ## AnxietyObjModAnxiety                          -0.02815    0.04936  -0.570
    ## AnxietyObjLowAnxiety                          -0.22918    0.05383  -4.257
    ## StressObjModStress                            -0.20472    0.05393  -3.796
    ## StressObjLowStress                            -0.44990    0.05459  -8.242
    ## DebtObjModDebt                                -0.35034    0.04666  -7.509
    ## DebtObjLowDebt                                -1.13167    0.03697 -30.611
    ## ConfidenceObjModConfidence                     0.47462    0.06116   7.761
    ## ConfidenceObjLowConfidence                     0.85893    0.08233  10.432
    ## StressObjModStress:ConfidenceObjModConfidence  0.04856    0.10563   0.460
    ## StressObjLowStress:ConfidenceObjModConfidence  0.09191    0.10278   0.894
    ## StressObjModStress:ConfidenceObjLowConfidence  0.14380    0.16044   0.896
    ## StressObjLowStress:ConfidenceObjLowConfidence  0.19007    0.14995   1.268
    ##                                               Pr(>|z|)    
    ## (Intercept)                                    < 2e-16 ***
    ## FinancesObjModFinCond                          < 2e-16 ***
    ## FinancesObjLowFinCond                          < 2e-16 ***
    ## AnxietyObjModAnxiety                          0.568491    
    ## AnxietyObjLowAnxiety                          2.07e-05 ***
    ## StressObjModStress                            0.000147 ***
    ## StressObjLowStress                             < 2e-16 ***
    ## DebtObjModDebt                                5.97e-14 ***
    ## DebtObjLowDebt                                 < 2e-16 ***
    ## ConfidenceObjModConfidence                    8.44e-15 ***
    ## ConfidenceObjLowConfidence                     < 2e-16 ***
    ## StressObjModStress:ConfidenceObjModConfidence 0.645709    
    ## StressObjLowStress:ConfidenceObjModConfidence 0.371202    
    ## StressObjModStress:ConfidenceObjLowConfidence 0.370093    
    ## StressObjLowStress:ConfidenceObjLowConfidence 0.204971    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 34215  on 24730  degrees of freedom
    ## Residual deviance: 24648  on 24716  degrees of freedom
    ##   (1127 observations deleted due to missingness)
    ## AIC: 24678
    ## 
    ## Number of Fisher Scoring iterations: 4

    ##                             GVIF Df GVIF^(1/(2*Df))
    ## FinancesObj             1.152573  2        1.036137
    ## AnxietyObj              2.498931  2        1.257299
    ## StressObj               3.649645  2        1.382174
    ## DebtObj                 1.186866  2        1.043759
    ## ConfidenceObj           3.747015  2        1.391302
    ## StressObj:ConfidenceObj 5.245624  4        1.230197

    ##                                   (Intercept) 
    ##                                     0.5543182 
    ##                         FinancesObjModFinCond 
    ##                                     3.2877490 
    ##                         FinancesObjLowFinCond 
    ##                                    12.5416767 
    ##                          AnxietyObjModAnxiety 
    ##                                     0.9722454 
    ##                          AnxietyObjLowAnxiety 
    ##                                     0.7951860 
    ##                            StressObjModStress 
    ##                                     0.8148771 
    ##                            StressObjLowStress 
    ##                                     0.6376949 
    ##                                DebtObjModDebt 
    ##                                     0.7044510 
    ##                                DebtObjLowDebt 
    ##                                     0.3224931 
    ##                    ConfidenceObjModConfidence 
    ##                                     1.6074078 
    ##                    ConfidenceObjLowConfidence 
    ##                                     2.3606259 
    ## StressObjModStress:ConfidenceObjModConfidence 
    ##                                     1.0497605 
    ## StressObjLowStress:ConfidenceObjModConfidence 
    ##                                     1.0962678 
    ## StressObjModStress:ConfidenceObjLowConfidence 
    ##                                     1.1546512 
    ## StressObjLowStress:ConfidenceObjLowConfidence 
    ##                                     1.2093283
