Psychological effects on likelihood of having an emergency fund
================
Kieran Yuen

# Loading in Data

``` r
library(haven)
NFCS_2018_State_Data <- read_sav("NFCS 2018 State Data.sav")
View(NFCS_2018_State_Data)
detach()
```

# Preliminary Multicollinearity Check

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

# Preliminary data preparation

## Create new columns of data

``` r
attach(NFCS_2018_State_Data)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
#Dep. Var: Emergency Fund
NFCS_2018_State_Data$EmergencyFund <- as.factor(NFCS_2018_State_Data$J5) 
levels(NFCS_2018_State_Data$EmergencyFund) <- c("1","0",NA, NA)

#Ind. Var: Financial Condition
NFCS_2018_State_Data$FinancialCondition <- as.factor(NFCS_2018_State_Data$J1) 
levels(NFCS_2018_State_Data$FinancialCondition) <- c("1","2","3","4","5","6","7","8","9","10",NA, NA)

#Ind. Var: Anxiety
NFCS_2018_State_Data$Anxiety <- as.factor(NFCS_2018_State_Data$J33_40)
levels(NFCS_2018_State_Data$Anxiety) <- c("1","2","3","4","5","6","7",NA, NA)

#Ind. Var: Stress
NFCS_2018_State_Data$Stress <- as.factor(NFCS_2018_State_Data$J33_41)
levels(NFCS_2018_State_Data$Stress) <- c("1","2","3","4","5","6","7",NA, NA)

#Ind. Var: Amount of Debt
NFCS_2018_State_Data$Debt <- as.factor(NFCS_2018_State_Data$G23)
levels(NFCS_2018_State_Data$Debt) <- c("1","2","3","4","5","6","7",NA, NA)

#Ind. Var: Subjective Financial Knowledge (Confidence)
NFCS_2018_State_Data$Confidence <- as.factor(NFCS_2018_State_Data$M4)
levels(NFCS_2018_State_Data$Confidence) <- c("1","2","3","4","5","6","7",NA, NA)

#Demographic variable: Age Group
NFCS_2018_State_Data$AgeGroup <- as.factor(NFCS_2018_State_Data$A3Ar_w)
levels(NFCS_2018_State_Data$AgeGroup) <- c("18-24","25-34","35-44","45-54","55-64","65+")

#Demographic variable: Gender
NFCS_2018_State_Data$Gender <- as.factor(NFCS_2018_State_Data$A3)
levels(NFCS_2018_State_Data$Gender) <- c("Male","Female")

#Demographic variable: Education Level
NFCS_2018_State_Data$EducationLevel <- as.factor(NFCS_2018_State_Data$A5_2015)
levels(NFCS_2018_State_Data$EducationLevel) <- c("Less than College","Less than College", "Less than College", "Some College", "Some College", "College Graduate", "AdvancedDeg")

#Demographic variable: Race (Survey only included White or Non-White)
NFCS_2018_State_Data$Race <- as.factor(NFCS_2018_State_Data$A4A_new_w)
levels(NFCS_2018_State_Data$Race) <- c("White","Non-White")

#Demographic variable: Marital Status
NFCS_2018_State_Data$MaritalStatus <- as.factor(NFCS_2018_State_Data$A6)
levels(NFCS_2018_State_Data$MaritalStatus) <- c("Married","Not Married","Not Married","Not Married","Not Married")

#Demographic variable: Yes/No for Dependent Children
NFCS_2018_State_Data$DepChildren <- as.factor(NFCS_2018_State_Data$A11)
levels(NFCS_2018_State_Data$DepChildren) <- c("Yes","Yes","Yes","Yes","No", "No")

#Demographic variable: Income Groupings
NFCS_2018_State_Data$Income <- as.factor(NFCS_2018_State_Data$A8)
levels(NFCS_2018_State_Data$Income) <- c("Less than $25,000","Less than $25,000","$25,000-$50,000","$25,000-$50,000","$50,000-$100,000","$50,000-$100,000","$100,000+","$100,000+")

#Demographic variable: Employment Status
NFCS_2018_State_Data$Employement <- as.factor(NFCS_2018_State_Data$A9)
levels(NFCS_2018_State_Data$Employement) <- c("Employed","Employed","Employed","Unemployed","Unemployed","Unemployed","Unemployed","Unemployed")

detach()
detach()
```

## Subsetting data

``` r
attach(NFCS_2018_State_Data)
use_varb <- ((EmergencyFund == 1) | (EmergencyFund == 0))
data_use <- subset(NFCS_2018_State_Data, use_varb)
detach()
```

## Recoding Ind. Variables in Subsetted Database

``` r
attach(data_use)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
#Ind. Var: Financial Condition
data_use$FinancialCondition <- as.numeric(data_use$FinancialCondition) 
High_Finances <- ((data_use$FinancialCondition>= 8) & (data_use$FinancialCondition <= 10))
Moderate_Finances <- ((data_use$FinancialCondition>= 4) & (data_use$FinancialCondition <= 7))
Low_Finances <- ((data_use$FinancialCondition>= 1) & (data_use$FinancialCondition <= 3))
FinancesObj <- factor((1*High_Finances + 2*Moderate_Finances + 3*Low_Finances), levels = c(1, 2, 3), labels = c( "HighFinCond", "ModFinCond", "LowFinCond"))

#Ind. Var: Anxiety
data_use$Anxiety <- as.numeric(data_use$Anxiety)
High_Anxiety <- ((data_use$Anxiety>= 5) & (data_use$Anxiety <= 7))
Moderate_Anxiety <- ((data_use$Anxiety > 3) & (data_use$Anxiety < 5))
Low_Anxiety <- ((data_use$Anxiety>= 1) & (data_use$Anxiety <= 3))
AnxietyObj <- factor((1*Low_Anxiety + 2*Moderate_Anxiety + 3*High_Anxiety), levels = c(1, 2, 3), labels = c( "LowAnxiety", "ModAnxiety", "HighAnxiety"))

#Ind. Var: Stress
data_use$Stress <- as.numeric(data_use$Stress)
High_Stress <- ((data_use$Stress>= 5) & (data_use$Stress <= 7))
Moderate_Stress <- ((data_use$Stress > 3) & (data_use$Stress < 5))
Low_Stress <- ((data_use$Stress>= 1) & (data_use$Stress <= 3))
StressObj <- factor((1*Low_Stress + 2*Moderate_Stress + 3*High_Stress), levels = c(1, 2, 3), labels = c( "LowStress", "ModStress", "HighStress"))

#Ind. Var: Amount of Debt
data_use$Debt <- as.numeric(data_use$Debt)
High_Debt <- ((data_use$Debt>= 5) & (data_use$Debt <= 7))
Moderate_Debt <- ((data_use$Debt > 3) & (data_use$Debt < 5))
Low_Debt <- ((data_use$Debt>= 1) & (data_use$Debt <= 3))
DebtObj<- factor((1*Low_Debt + 2*Moderate_Debt + 3*High_Debt), levels = c(1, 2, 3), labels = c( "LowDebt", "ModDebt", "HighDebt"))

#Ind. Var: Subjective Financial Knowledge (Confidence)
data_use$Confidence <- as.numeric(data_use$Confidence)
High_Confidence <- ((data_use$Confidence>= 5) & (data_use$Confidence <= 7))
Moderate_Confidence <- ((data_use$Confidence > 3) & (data_use$Confidence < 5))
Low_Confidence <- ((data_use$Confidence>= 1) & (data_use$Confidence <= 3))
ConfidenceObj<- factor((1*High_Confidence + 2*Moderate_Confidence + 3*Low_Confidence), levels = c(1, 2, 3), labels = c( "HighConfidence", "ModConfidence", "LowConfidence"))


detach()
detach()
```

## TABLE 2. Descriptive Statistics

    ## EmergencyFund
    ##         1         0 
    ## 0.5192204 0.4807796

    ## FinancesObj
    ## HighFinCond  ModFinCond  LowFinCond 
    ##   0.3250176   0.4175217   0.2574606

    ## AnxietyObj
    ##  LowAnxiety  ModAnxiety HighAnxiety 
    ##   0.2878758   0.1734196   0.5387045

    ## StressObj
    ##  LowStress  ModStress HighStress 
    ##  0.3635654  0.1932612  0.4431734

    ## DebtObj
    ##   LowDebt   ModDebt  HighDebt 
    ## 0.4690100 0.1470806 0.3839094

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

# Regressions

## TABLE 3. Logistic Regression with Emergency Fund as Dependent Variable

``` r
logitmodel <- glm(EmergencyFund ~ FinancesObj + AnxietyObj + DebtObj + ConfidenceObj + AgeGroup + Gender + Race + MaritalStatus + DepChildren + EducationLevel + Income + Employement, family = binomial, data = data_use)
summary(logitmodel)
```

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ FinancesObj + AnxietyObj + DebtObj + 
    ##     ConfidenceObj + AgeGroup + Gender + Race + MaritalStatus + 
    ##     DepChildren + EducationLevel + Income + Employement, family = binomial, 
    ##     data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.8047  -0.7375  -0.2991   0.7433   2.6525  
    ## 
    ## Coefficients:
    ##                                Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)                    -0.97363    0.09080 -10.723  < 2e-16 ***
    ## FinancesObjModFinCond           1.06255    0.04036  26.326  < 2e-16 ***
    ## FinancesObjLowFinCond           2.18829    0.05328  41.068  < 2e-16 ***
    ## AnxietyObjModAnxiety            0.24827    0.05094   4.874 1.09e-06 ***
    ## AnxietyObjHighAnxiety           0.40755    0.04278   9.528  < 2e-16 ***
    ## DebtObjModDebt                  0.73548    0.04690  15.681  < 2e-16 ***
    ## DebtObjHighDebt                 1.20082    0.03884  30.915  < 2e-16 ***
    ## ConfidenceObjModConfidence      0.38282    0.04460   8.583  < 2e-16 ***
    ## ConfidenceObjLowConfidence      0.68198    0.06443  10.584  < 2e-16 ***
    ## AgeGroup25-34                  -0.14810    0.06509  -2.275  0.02289 *  
    ## AgeGroup35-44                   0.06771    0.06697   1.011  0.31197    
    ## AgeGroup45-54                   0.14309    0.06618   2.162  0.03061 *  
    ## AgeGroup55-64                  -0.15597    0.06594  -2.365  0.01802 *  
    ## AgeGroup65+                    -0.46988    0.06946  -6.765 1.34e-11 ***
    ## GenderFemale                    0.08665    0.03331   2.602  0.00928 ** 
    ## RaceNon-White                  -0.03512    0.03785  -0.928  0.35347    
    ## MaritalStatusNot Married        0.06984    0.03772   1.852  0.06406 .  
    ## DepChildrenNo                  -0.20377    0.03879  -5.254 1.49e-07 ***
    ## EducationLevelSome College     -0.21170    0.04138  -5.116 3.12e-07 ***
    ## EducationLevelCollege Graduate -0.56776    0.04844 -11.720  < 2e-16 ***
    ## EducationLevelAdvancedDeg      -0.58735    0.05935  -9.896  < 2e-16 ***
    ## Income$25,000-$50,000          -0.54758    0.05057 -10.829  < 2e-16 ***
    ## Income$50,000-$100,000         -0.95619    0.05220 -18.319  < 2e-16 ***
    ## Income$100,000+                -1.27283    0.06417 -19.834  < 2e-16 ***
    ## EmployementUnemployed           0.10879    0.03949   2.755  0.00586 ** 
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

``` r
car::vif(logitmodel)
```

    ##                    GVIF Df GVIF^(1/(2*Df))
    ## FinancesObj    1.198781  2        1.046369
    ## AnxietyObj     1.233070  2        1.053773
    ## DebtObj        1.243654  2        1.056027
    ## ConfidenceObj  1.116856  2        1.028015
    ## AgeGroup       1.852139  5        1.063573
    ## Gender         1.051232  1        1.025296
    ## Race           1.076630  1        1.037608
    ## MaritalStatus  1.359691  1        1.166058
    ## DepChildren    1.355707  1        1.164348
    ## EducationLevel 1.186241  3        1.028874
    ## Income         1.550071  3        1.075784
    ## Employement    1.424598  1        1.193565

``` r
exp(coefficients(logitmodel))
```

    ##                    (Intercept)          FinancesObjModFinCond 
    ##                      0.3777086                      2.8937295 
    ##          FinancesObjLowFinCond           AnxietyObjModAnxiety 
    ##                      8.9199528                      1.2818045 
    ##          AnxietyObjHighAnxiety                 DebtObjModDebt 
    ##                      1.5031297                      2.0864867 
    ##                DebtObjHighDebt     ConfidenceObjModConfidence 
    ##                      3.3228297                      1.4664139 
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
    ##          EmployementUnemployed 
    ##                      1.1149334

## TABLE 4. Logistic Regression with Emergency Fund as Dependent Variable, Demo Variables removed

``` r
logitmodel2 <- glm(EmergencyFund ~ FinancesObj + AnxietyObj + DebtObj + ConfidenceObj, family = binomial, data = data_use)
summary(logitmodel2)
```

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ FinancesObj + AnxietyObj + DebtObj + 
    ##     ConfidenceObj, family = binomial, data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.4103  -0.8477  -0.4265   0.7951   2.2101  
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)                -2.35134    0.04032 -58.314  < 2e-16 ***
    ## FinancesObjModFinCond       1.18041    0.03863  30.556  < 2e-16 ***
    ## FinancesObjLowFinCond       2.53637    0.05083  49.902  < 2e-16 ***
    ## AnxietyObjModAnxiety        0.34319    0.04887   7.023 2.18e-12 ***
    ## AnxietyObjHighAnxiety       0.52042    0.04070  12.785  < 2e-16 ***
    ## DebtObjModDebt              0.80437    0.04491  17.910  < 2e-16 ***
    ## DebtObjHighDebt             1.16965    0.03650  32.044  < 2e-16 ***
    ## ConfidenceObjModConfidence  0.52570    0.04299  12.228  < 2e-16 ***
    ## ConfidenceObjLowConfidence  0.97334    0.06219  15.650  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 34355  on 24828  degrees of freedom
    ## Residual deviance: 24854  on 24820  degrees of freedom
    ##   (1029 observations deleted due to missingness)
    ## AIC: 24872
    ## 
    ## Number of Fisher Scoring iterations: 4

``` r
car::vif(logitmodel2)
```

    ##                   GVIF Df GVIF^(1/(2*Df))
    ## FinancesObj   1.141337  2        1.033602
    ## AnxietyObj    1.190405  2        1.044537
    ## DebtObj       1.158741  2        1.037520
    ## ConfidenceObj 1.067964  2        1.016574

``` r
exp(coefficients(logitmodel2))
```

    ##                (Intercept)      FinancesObjModFinCond 
    ##                 0.09524106                 3.25569482 
    ##      FinancesObjLowFinCond       AnxietyObjModAnxiety 
    ##                12.63372582                 1.40944346 
    ##      AnxietyObjHighAnxiety             DebtObjModDebt 
    ##                 1.68272738                 2.23528525 
    ##            DebtObjHighDebt ConfidenceObjModConfidence 
    ##                 3.22087202                 1.69165022 
    ## ConfidenceObjLowConfidence 
    ##                 2.64676023

## TABLE 5. Logistic Regression with Emergency Fund as Dependent Variable

``` r
logitmodel3 <- glm(EmergencyFund ~ Income, family = binomial, data = data_use)
summary(logitmodel3)
```

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ Income, family = binomial, data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.6818  -0.9901  -0.7406   1.0702   1.6899  
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)             1.13557    0.03154   36.00   <2e-16 ***
    ## Income$25,000-$50,000  -0.87801    0.04024  -21.82   <2e-16 ***
    ## Income$50,000-$100,000 -1.59348    0.03841  -41.49   <2e-16 ***
    ## Income$100,000+        -2.28919    0.04547  -50.34   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 35809  on 25857  degrees of freedom
    ## Residual deviance: 32324  on 25854  degrees of freedom
    ## AIC: 32332
    ## 
    ## Number of Fisher Scoring iterations: 4

``` r
exp(coefficients(logitmodel3))
```

    ##            (Intercept)  Income$25,000-$50,000 Income$50,000-$100,000 
    ##              3.1129518              0.4156073              0.2032179 
    ##        Income$100,000+ 
    ##              0.1013480

## TABLE 6. Logistic Model with Interaction between Anxiety and Confidence

``` r
interactionmodel1 <- glm(EmergencyFund ~ AnxietyObj:ConfidenceObj + FinancesObj + DebtObj + AgeGroup + Gender + Race + MaritalStatus + DepChildren + EducationLevel + Income + Employement, family = binomial, data = data_use)
summary(interactionmodel1)
```

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ AnxietyObj:ConfidenceObj + FinancesObj + 
    ##     DebtObj + AgeGroup + Gender + Race + MaritalStatus + DepChildren + 
    ##     EducationLevel + Income + Employement, family = binomial, 
    ##     data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.7990  -0.7370  -0.2968   0.7432   2.6601  
    ## 
    ## Coefficients: (1 not defined because of singularities)
    ##                                                   Estimate Std. Error z value
    ## (Intercept)                                        0.09784    0.11290   0.867
    ## FinancesObjModFinCond                              1.06061    0.04038  26.263
    ## FinancesObjLowFinCond                              2.18658    0.05333  41.003
    ## DebtObjModDebt                                     0.73495    0.04691  15.667
    ## DebtObjHighDebt                                    1.19985    0.03885  30.885
    ## AgeGroup25-34                                     -0.14687    0.06508  -2.257
    ## AgeGroup35-44                                      0.06934    0.06696   1.036
    ## AgeGroup45-54                                      0.14483    0.06618   2.188
    ## AgeGroup55-64                                     -0.15441    0.06594  -2.342
    ## AgeGroup65+                                       -0.46898    0.06945  -6.753
    ## GenderFemale                                       0.08746    0.03331   2.625
    ## RaceNon-White                                     -0.03607    0.03785  -0.953
    ## MaritalStatusNot Married                           0.07022    0.03773   1.861
    ## DepChildrenNo                                     -0.20332    0.03881  -5.239
    ## EducationLevelSome College                        -0.21147    0.04138  -5.110
    ## EducationLevelCollege Graduate                    -0.56667    0.04846 -11.693
    ## EducationLevelAdvancedDeg                         -0.58451    0.05939  -9.842
    ## Income$25,000-$50,000                             -0.54705    0.05056 -10.819
    ## Income$50,000-$100,000                            -0.95516    0.05219 -18.300
    ## Income$100,000+                                   -1.27104    0.06418 -19.804
    ## EmployementUnemployed                              0.11016    0.03950   2.789
    ## AnxietyObjLowAnxiety:ConfidenceObjHighConfidence  -1.09644    0.08488 -12.917
    ## AnxietyObjModAnxiety:ConfidenceObjHighConfidence  -0.80992    0.08664  -9.348
    ## AnxietyObjHighAnxiety:ConfidenceObjHighConfidence -0.66092    0.07784  -8.491
    ## AnxietyObjLowAnxiety:ConfidenceObjModConfidence   -0.54990    0.12297  -4.472
    ## AnxietyObjModAnxiety:ConfidenceObjModConfidence   -0.51436    0.11330  -4.540
    ## AnxietyObjHighAnxiety:ConfidenceObjModConfidence  -0.29432    0.08781  -3.352
    ## AnxietyObjLowAnxiety:ConfidenceObjLowConfidence   -0.35504    0.15892  -2.234
    ## AnxietyObjModAnxiety:ConfidenceObjLowConfidence   -0.11006    0.17217  -0.639
    ## AnxietyObjHighAnxiety:ConfidenceObjLowConfidence        NA         NA      NA
    ##                                                   Pr(>|z|)    
    ## (Intercept)                                       0.386138    
    ## FinancesObjModFinCond                              < 2e-16 ***
    ## FinancesObjLowFinCond                              < 2e-16 ***
    ## DebtObjModDebt                                     < 2e-16 ***
    ## DebtObjHighDebt                                    < 2e-16 ***
    ## AgeGroup25-34                                     0.024019 *  
    ## AgeGroup35-44                                     0.300361    
    ## AgeGroup45-54                                     0.028640 *  
    ## AgeGroup55-64                                     0.019203 *  
    ## AgeGroup65+                                       1.45e-11 ***
    ## GenderFemale                                      0.008658 ** 
    ## RaceNon-White                                     0.340634    
    ## MaritalStatusNot Married                          0.062682 .  
    ## DepChildrenNo                                     1.61e-07 ***
    ## EducationLevelSome College                        3.22e-07 ***
    ## EducationLevelCollege Graduate                     < 2e-16 ***
    ## EducationLevelAdvancedDeg                          < 2e-16 ***
    ## Income$25,000-$50,000                              < 2e-16 ***
    ## Income$50,000-$100,000                             < 2e-16 ***
    ## Income$100,000+                                    < 2e-16 ***
    ## EmployementUnemployed                             0.005291 ** 
    ## AnxietyObjLowAnxiety:ConfidenceObjHighConfidence   < 2e-16 ***
    ## AnxietyObjModAnxiety:ConfidenceObjHighConfidence   < 2e-16 ***
    ## AnxietyObjHighAnxiety:ConfidenceObjHighConfidence  < 2e-16 ***
    ## AnxietyObjLowAnxiety:ConfidenceObjModConfidence   7.76e-06 ***
    ## AnxietyObjModAnxiety:ConfidenceObjModConfidence   5.63e-06 ***
    ## AnxietyObjHighAnxiety:ConfidenceObjModConfidence  0.000803 ***
    ## AnxietyObjLowAnxiety:ConfidenceObjLowConfidence   0.025477 *  
    ## AnxietyObjModAnxiety:ConfidenceObjLowConfidence   0.522677    
    ## AnxietyObjHighAnxiety:ConfidenceObjLowConfidence        NA    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 34355  on 24828  degrees of freedom
    ## Residual deviance: 23524  on 24800  degrees of freedom
    ##   (1029 observations deleted due to missingness)
    ## AIC: 23582
    ## 
    ## Number of Fisher Scoring iterations: 5

``` r
exp(coefficients(interactionmodel1))
```

    ##                                       (Intercept) 
    ##                                         1.1027865 
    ##                             FinancesObjModFinCond 
    ##                                         2.8881188 
    ##                             FinancesObjLowFinCond 
    ##                                         8.9047294 
    ##                                    DebtObjModDebt 
    ##                                         2.0853796 
    ##                                   DebtObjHighDebt 
    ##                                         3.3196200 
    ##                                     AgeGroup25-34 
    ##                                         0.8634095 
    ##                                     AgeGroup35-44 
    ##                                         1.0718034 
    ##                                     AgeGroup45-54 
    ##                                         1.1558451 
    ##                                     AgeGroup55-64 
    ##                                         0.8569210 
    ##                                       AgeGroup65+ 
    ##                                         0.6256425 
    ##                                      GenderFemale 
    ##                                         1.0913936 
    ##                                     RaceNon-White 
    ##                                         0.9645752 
    ##                          MaritalStatusNot Married 
    ##                                         1.0727491 
    ##                                     DepChildrenNo 
    ##                                         0.8160157 
    ##                        EducationLevelSome College 
    ##                                         0.8093941 
    ##                    EducationLevelCollege Graduate 
    ##                                         0.5674093 
    ##                         EducationLevelAdvancedDeg 
    ##                                         0.5573771 
    ##                             Income$25,000-$50,000 
    ##                                         0.5786543 
    ##                            Income$50,000-$100,000 
    ##                                         0.3847504 
    ##                                   Income$100,000+ 
    ##                                         0.2805387 
    ##                             EmployementUnemployed 
    ##                                         1.1164594 
    ##  AnxietyObjLowAnxiety:ConfidenceObjHighConfidence 
    ##                                         0.3340586 
    ##  AnxietyObjModAnxiety:ConfidenceObjHighConfidence 
    ##                                         0.4448915 
    ## AnxietyObjHighAnxiety:ConfidenceObjHighConfidence 
    ##                                         0.5163762 
    ##   AnxietyObjLowAnxiety:ConfidenceObjModConfidence 
    ##                                         0.5770061 
    ##   AnxietyObjModAnxiety:ConfidenceObjModConfidence 
    ##                                         0.5978815 
    ##  AnxietyObjHighAnxiety:ConfidenceObjModConfidence 
    ##                                         0.7450349 
    ##   AnxietyObjLowAnxiety:ConfidenceObjLowConfidence 
    ##                                         0.7011453 
    ##   AnxietyObjModAnxiety:ConfidenceObjLowConfidence 
    ##                                         0.8957827 
    ##  AnxietyObjHighAnxiety:ConfidenceObjLowConfidence 
    ##                                                NA
