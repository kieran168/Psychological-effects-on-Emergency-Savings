Mental well-being and emergency savings
================
Kieran Yuen

# Introduction

  - save this for last

# Literature Review

Economists have been studying how people make decisions since the
beginning days of the social science. One of these decisions includes
financial decisions. The field of economics studies

  - Here are some papers I am referencing as to why having an emergency
    fund is important to have and talking about it’s benefits

# Methods/Data

## Overall goal

To find possible reasons why someone might not have an emergency fund
and propose ideas on how to address those issues to encourage/incentive
people to have an emergency fund.

## Other variables to interact with ind. var.

### Interaction \#1

Objective financial knowledge:anxiety/stressed about personal finances

Someone who objectively understands finances (but not necessarily
confident) but is stressed or gets anixety from thinking about.

How likely are they to have an emergency fund?

### Interaction \#2

Subjective financial knowledge:anxiety/stressed about personal finances

Someone who is confident in their knowledge about personal finance (but
not necessarily objectively knowledgeable about it) but is stressed/not
stressed or gets anixety from thinking about.

How likely are they to have an emergency fund?

## Hypothesis

Someone with great financial knowledge should have the understanding and
foresight to save for the future/emergency fund. *Make emergency fund
the dependent variable and use the objective questions as independent
variables.*

*In addition, maybe we can find correlations between our independent
variables and some of the objective questions. These correlations might
tell us something. For example, seeing if there is a correlation between
someone who feels a lot of stress just thinking about finances but
answered the objective questions correctly. I would expect to see that
those with correct answers in the objective questions should have an
emergency fund*

What type of people will have an emergency fund?

What kind of effect does mental well-being have in determining if
someone has an emergency fund?

## Dataset used

### Loading in Data

``` r
library(haven)
NFCS_2018_State_Data <- read_sav("NFCS 2018 State Data.sav")
View(NFCS_2018_State_Data)
```

The dataset I used is the National Financial Capability Study (NFCS)
which was funded by the FINRA Investor Education Foundation and
conducted by ARC Research. The data can be downloaded here:
<https://www.usfinancialcapability.org/downloads.php>. This study has
been conducted in 2009, 2012, 2015, and 2018. I will be using the 2018
dataset. The overall goal of this study is to assess financial
capability on certain key metrics and evaluate how these vary with
underlying demographic, behavioral, attitudinal and financial literacy
characteristics. I chose this dataset as it focuses on financial
decisions being made in a household, which is the local-level data I was
looking for to address my hypothesis.

This research will be focusing on one financial decision made by
households, and that is the decision to save an emergency fund or not.

### Dependent Variable

The dependent variable will be question \#J5: *Have you set aside
emergency or rainy day funds that would cover your expenses for 3
months, in case of sickness, job loss, economic downturn, or other
emergencies?* The available answers were: “Yes,” “No,” “Don’t know,” and
“Prefer not to say.” A binary variable was created where “1” corresponds
to “Yes” and “0” means “No” this individual did not have an emergency
fund. Responses where the answers were “Don’t know” or “Prefer not to
say” were not included in the analysis.

### Independent Variables

*The four key independent variables had (INSERT ANSWER HERE)
correlations with one another, indicating that the four variables were
not likely measuring the same thing. The correlation coefficient was
X.XX. This means that they both had low correlation but both affected
the likelihood of someone having an emergnecy fund or not - ALSO
CONSIDER RUNNING THE VARIANCE INFLATION FACTOR (VIF) TEST TO CHECK FOR
MULTICOLLINEARITY BETWEEN THE IND. VARIABLES*

How does how you feel about your finances affect whether you have an
emergency fund or not? - Here is my hypothesis and why I chose this
hypothesis - Here is the data I am going to look at to answer the
question about that hypothesis - Here is how I am going to
restrict/SUBSET the data to test my hypothesis - explain why we are
excluding the Don’t Know/Prefer not to answer - Here is how I am going
to test the data to test my hypothesis - Here is how i prepared the data
- Here are some summary statistics of my SUBSETTED data broken out by
Age, Education Level, Labor Force Participation, income level, race,
marital status, dependent children - Here is a table of all my important
variables in my regression with mean, standard deviation, min/max,
median, average rating - Here is how I verified that all the important
variables I will be using in my research makes sense (just talk about
how the average rating you saw for one of the questions should be low
because people who have a lot of debt would feel anxious about their
finances - this is a correlation)

## Means (simple graphs, correlations, differences of means)

### Preliminary Multicollinearity Check

``` r
attach(NFCS_2018_State_Data)
cor(J1,J5)
```

    ## [1] 0.224398

``` r
cor(J33_40,J5)
```

    ## [1] 0.2320714

``` r
cor(J33_41,J5)
```

    ## [1] 0.2251923

``` r
cor(G23,J5)
```

    ## [1] 0.2378071

``` r
cor(J1,J33_40)
```

    ## [1] 0.268183

``` r
cor(J1,J33_41)
```

    ## [1] 0.2598679

``` r
cor(J1,G23)
```

    ## [1] 0.2284568

``` r
cor(J33_40,J33_41)
```

    ## [1] 0.6698352

``` r
cor(J33_40,G23)
```

    ## [1] 0.380633

``` r
cor(G23,J33_41)
```

    ## [1] 0.3905643

``` r
detach()
```

## Preliminary data preparation

### Create new columns of data

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
#Dep. Var: Financial Condition
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

#Ind. Var: Objective Financial Knowledge (6 finance questions)
NFCS_2018_State_Data$Question1 <- as.factor(NFCS_2018_State_Data$M6)
levels(NFCS_2018_State_Data$Question1) <- c("1","0","0","0","0")

NFCS_2018_State_Data$Question2 <- as.factor(NFCS_2018_State_Data$M7)
levels(NFCS_2018_State_Data$Question2) <- c("0","0","1","0","0")

NFCS_2018_State_Data$Question3 <- as.factor(NFCS_2018_State_Data$M8)
levels(NFCS_2018_State_Data$Question3) <- c("0","1","0","0","0","0")

NFCS_2018_State_Data$Question4 <- as.factor(NFCS_2018_State_Data$M31)
levels(NFCS_2018_State_Data$Question4) <- c("0","1","0","0","0","0")

NFCS_2018_State_Data$Question5 <- as.factor(NFCS_2018_State_Data$M9)
levels(NFCS_2018_State_Data$Question5) <- c("1","0","0","0")

NFCS_2018_State_Data$Question6 <- as.factor(NFCS_2018_State_Data$M10)
levels(NFCS_2018_State_Data$Question6) <- c("0","1","0","0")

NFCS_2018_State_Data$AgeGroup <- as.factor(NFCS_2018_State_Data$A3Ar_w)
levels(NFCS_2018_State_Data$AgeGroup) <- c("18-24","25-34","35-44","45-54","55-64","65+")

NFCS_2018_State_Data$Gender <- as.factor(NFCS_2018_State_Data$A3)
levels(NFCS_2018_State_Data$Gender) <- c("Male","Female")

NFCS_2018_State_Data$EducationLevel <- as.factor(NFCS_2018_State_Data$A5_2015)
levels(NFCS_2018_State_Data$EducationLevel) <- c("Less than College","Less than College", "Less than College", "Some College", "Some College", "College Graduate", "AdvancedDeg")

NFCS_2018_State_Data$Race <- as.factor(NFCS_2018_State_Data$A4A_new_w)
levels(NFCS_2018_State_Data$Race) <- c("White","Non-White")

NFCS_2018_State_Data$MaritalStatus <- as.factor(NFCS_2018_State_Data$A6)
levels(NFCS_2018_State_Data$MaritalStatus) <- c("Married","Not Married","Not Married","Not Married","Not Married")

NFCS_2018_State_Data$DepChildren <- as.factor(NFCS_2018_State_Data$A11)
levels(NFCS_2018_State_Data$DepChildren) <- c("Yes","Yes","Yes","Yes","No", "No")

NFCS_2018_State_Data$Income <- as.factor(NFCS_2018_State_Data$A8)
levels(NFCS_2018_State_Data$Income) <- c("Less than $25,000","$Less than $25,000","$25,000-$50,000","$25,000-$50,000","$50,000-$100,000","$50,000-$100,000","$100,000+","$100,000+")

NFCS_2018_State_Data$Employement <- as.factor(NFCS_2018_State_Data$A9)
levels(NFCS_2018_State_Data$Employement) <- c("Employed","Employed","Employed","Unemployed","Unemployed","Unemployed","Unemployed","Unemployed")

detach()
detach()
```

### Subsetting data

``` r
attach(NFCS_2018_State_Data)
use_varb <- ((EmergencyFund == 1) | (EmergencyFund == 0))
data_use <- subset(NFCS_2018_State_Data, use_varb)
detach()
```

### Recoding Ind. Variables in Subsetted Database

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
#data_use$Anxiety <- as.factor(data_use$J33_40)
#levels(data_use$Anxiety) <- c("1","2","3","4","5","6","7",NA, NA)
data_use$Anxiety <- as.numeric(data_use$Anxiety)
High_Anxiety <- ((data_use$Anxiety>= 5) & (data_use$Anxiety <= 7))
Moderate_Anxiety <- ((data_use$Anxiety > 3) & (data_use$Anxiety < 5))
Low_Anxiety <- ((data_use$Anxiety>= 1) & (data_use$Anxiety <= 3))
AnxietyObj <- factor((1*High_Anxiety + 2*Moderate_Anxiety + 3*Low_Anxiety), levels = c(1, 2, 3), labels = c( "HighAnxiety", "ModAnxiety", "LowAnxiety"))

#Ind. Var: Stress
#data_use$Stress <- as.factor(data_use$J33_41)
#levels(data_use$Stress) <- c("1","2","3","4","5","6","7",NA, NA)
data_use$Stress <- as.numeric(data_use$Stress)
High_Stress <- ((data_use$Stress>= 5) & (data_use$Stress <= 7))
Moderate_Stress <- ((data_use$Stress > 3) & (data_use$Stress < 5))
Low_Stress <- ((data_use$Stress>= 1) & (data_use$Stress <= 3))
StressObj <- factor((1*High_Stress + 2*Moderate_Stress + 3*Low_Stress), levels = c(1, 2, 3), labels = c( "HighStress", "ModStress", "LowStress"))

#Ind. Var: Amount of Debt
#data_use$Debt <- as.factor(data_use$G23)
#levels(data_use$Debt) <- c("1","2","3","4","5","6","7",NA, NA)
data_use$Debt <- as.numeric(data_use$Debt)
High_Debt <- ((data_use$Debt>= 5) & (data_use$Debt <= 7))
Moderate_Debt <- ((data_use$Debt > 3) & (data_use$Debt < 5))
Low_Debt <- ((data_use$Debt>= 1) & (data_use$Debt <= 3))
DebtObj<- factor((1*High_Debt + 2*Moderate_Debt + 3*Low_Debt), levels = c(1, 2, 3), labels = c( "HighDebt", "ModDebt", "LowDebt"))

#Ind. Var: Subjective Financial Knowledge (Confidence)
#data_use$Confidence <- as.factor(data_use$M4)
#levels(data_use$Confidence) <- c("1","2","3","4","5","6","7",NA, NA)
data_use$Confidence <- as.numeric(data_use$Confidence)
High_Confidence <- ((data_use$Confidence>= 5) & (data_use$Confidence <= 7))
Moderate_Confidence <- ((data_use$Confidence > 3) & (data_use$Confidence < 5))
Low_Confidence <- ((data_use$Confidence>= 1) & (data_use$Confidence <= 3))
ConfidenceObj<- factor((1*High_Confidence + 2*Moderate_Confidence + 3*Low_Confidence), levels = c(1, 2, 3), labels = c( "HighConfidence", "ModConfidence", "LowConfidence"))


detach()
detach()
```

## Simple Regressions

``` r
logitmodel <- glm(EmergencyFund ~ ConfidenceObj + AgeGroup + Gender + Race + MaritalStatus + DepChildren + EducationLevel + Income + Employement + FinancesObj + AnxietyObj + StressObj + DebtObj, family = binomial, data = data_use)
summary(logitmodel)
```

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

``` r
car::vif(logitmodel)
```

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

``` r
exp(coefficients(logitmodel))
```

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

``` r
interactionmodel1 <- glm(EmergencyFund ~ FinancesObj + AnxietyObj + StressObj + DebtObj + ConfidenceObj + StressObj:ConfidenceObj, family = binomial, data = data_use)
summary(interactionmodel1)
```

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

``` r
car::vif(interactionmodel1)
```

    ##                             GVIF Df GVIF^(1/(2*Df))
    ## FinancesObj             1.152573  2        1.036137
    ## AnxietyObj              2.498931  2        1.257299
    ## StressObj               3.649645  2        1.382174
    ## DebtObj                 1.186866  2        1.043759
    ## ConfidenceObj           3.747015  2        1.391302
    ## StressObj:ConfidenceObj 5.245624  4        1.230197

``` r
exp(coefficients(interactionmodel1))
```

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

# Results

  - Here is a scatterplot of my dep. variable and one of the ind.
    variables (lets do one for each ind. var. so that we can see what
    each one looks like)
  - Determine if squared or cubic or logarithmic terms would be useful
    by looking at the scatterplot of my regression
  - Determine if I want to look at certain subgroups within my data -
    maybe looking specifically on an income group might tell me
    something interesting about my data
  - Here is where I present some of my regression models (logit, probit)
    in easy-to-read tables (look at papers you have read as an example)
    -Here is where I present my main conclusion from what the regression
    has told me and where i try to do some “robustness checks” of the
    data (for example, I could look at the results by education level
    here and see )

# Discussion

  - What are the real world policy implications of my results?
  - Is there existing policies that already are doing what my research
    shows they should be doing?
  - DO NOT SAY “DO THIS” “DON’T DO THIS”
  - Instead, rely on economic facts and analysis
  - Present the facts and allow the reader to make the policy decison
    for themselves
  - I can say “if we can educate people more on personal financial
    issues this would increase the liklihood of them having a savings
    account by XX%” *Add a statement about how this fits into the larger
    picture of financial literacy*

# Limitations

  - We do not know where people are holding their 3 months of emergency
    funds. Whether that is in their savings account or invested in the
    stock market.
  - It is understood that measuring a person’s financial well-being is
    not like measuring their finances to determine if they can afford a
    mortgage, there is subjectivity on both the researcher side and the
    survey-taker side.
  - The simplicity of the functional form of the research limits it’s
    purview *How this study can continue to be studied/what I can
    further study* *Understand that we cannot know everything, there are
    limitations to what we can know and what we can even find out*

# Conclusion

  - save this for last

# Other

Is “feeling confident” the same as “not feeling anxious” or “feeling
great about my personal finance situation?”

Per Kevin, when I run the objective and subjective financial knowledge
questions I should be able to see the same results as what I saw in
previous studies.

Logit can give misleading results when we have “factors.”

Per Kevin, Income would be endogenous to what we would spend it on

The reason macro data is problematic is because the data is wider than
it is longer. That is because macro data is collected on a quarterly
level so even if we go back all the way to 1955. there would not be
enough data.

What should I do with the “weights” in my data?

Look for an academic paper that finds out if people know the difference
between anixety and stress
