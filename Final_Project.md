Mental well-being and emergency savings
================
Kieran Yuen

# Introduction

  - save this for last

# Literature Review

Economists have been studying how people make decisions since the
beginning days of the social science.

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
maritical status, dependent children - Here is a table of all my
important variables in my regression with mean, standard deviation,
min/max, median, average rating - Here is how I verified that all the
important variables I will be using in my research makes sense (just
talk about how the average rating you saw for one of the questions
should be low because people who have a lot of debt would feel anxious
about their finances - this is a correlation)

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
data_use$Anxiety <- as.factor(data_use$J33_40)
levels(data_use$Anxiety) <- c("1","2","3","4","5","6","7",NA, NA)
data_use$Anxiety <- as.numeric(data_use$Anxiety)
High_Anxiety <- ((data_use$Anxiety>= 5) & (data_use$Anxiety <= 7))
Moderate_Anxiety <- ((data_use$Anxiety > 3) & (data_use$Anxiety < 5))
Low_Anxiety <- ((data_use$Anxiety>= 1) & (data_use$Anxiety <= 3))
AnxietyObj <- factor((1*High_Anxiety + 2*Moderate_Anxiety + 3*Low_Anxiety), levels = c(1, 2, 3), labels = c( "HighAnxiety", "ModAnxiety", "LowAnxiety"))

#Ind. Var: Stress
data_use$Stress <- as.factor(data_use$J33_41)
levels(data_use$Stress) <- c("1","2","3","4","5","6","7",NA, NA)
data_use$Stress <- as.numeric(data_use$Stress)
High_Stress <- ((data_use$Stress>= 5) & (data_use$Stress <= 7))
Moderate_Stress <- ((data_use$Stress > 3) & (data_use$Stress < 5))
Low_Stress <- ((data_use$Stress>= 1) & (data_use$Stress <= 3))
StressObj <- factor((1*High_Stress + 2*Moderate_Stress + 3*Low_Stress), levels = c(1, 2, 3), labels = c( "HighStress", "ModStress", "LowStress"))

#Ind. Var: Amount of Debt
data_use$Debt <- as.factor(data_use$G23)
levels(data_use$Debt) <- c("1","2","3","4","5","6","7",NA, NA)
data_use$Debt <- as.numeric(data_use$Debt)
High_Debt <- ((data_use$Debt>= 5) & (data_use$Debt <= 7))
Moderate_Debt <- ((data_use$Debt > 3) & (data_use$Debt < 5))
Low_Debt <- ((data_use$Debt>= 1) & (data_use$Debt <= 3))
DebtObj<- factor((1*High_Debt + 2*Moderate_Debt + 3*Low_Debt), levels = c(1, 2, 3), labels = c( "HighDebt", "ModDebt", "LowDebt"))

#Ind. Var: Subjective Financial Knowledge (Confidence)
data_use$Confidence <- as.factor(data_use$M4)
levels(data_use$Confidence) <- c("1","2","3","4","5","6","7",NA, NA)
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
logitmodel <- glm(EmergencyFund ~ FinancesObj + AnxietyObj + StressObj + DebtObj, family = binomial, data = data_use)
summary(logitmodel)
```

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ FinancesObj + AnxietyObj + StressObj + 
    ##     DebtObj, family = binomial, data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.1628  -0.8041  -0.4294   0.8821   2.2044  
    ## 
    ## Coefficients:
    ##                       Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)           -0.52510    0.04103 -12.799  < 2e-16 ***
    ## FinancesObjModFinCond  1.26848    0.03807  33.321  < 2e-16 ***
    ## FinancesObjLowFinCond  2.76246    0.04914  56.211  < 2e-16 ***
    ## AnxietyObjModAnxiety  -0.02821    0.04865  -0.580    0.562    
    ## AnxietyObjLowAnxiety  -0.24956    0.05284  -4.723 2.33e-06 ***
    ## StressObjModStress    -0.18855    0.04733  -3.983 6.79e-05 ***
    ## StressObjLowStress    -0.46846    0.04955  -9.454  < 2e-16 ***
    ## DebtObjModDebt        -0.30137    0.04587  -6.570 5.02e-11 ***
    ## DebtObjLowDebt        -1.09440    0.03633 -30.120  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 34684  on 25060  degrees of freedom
    ## Residual deviance: 25340  on 25052  degrees of freedom
    ##   (797 observations deleted due to missingness)
    ## AIC: 25358
    ## 
    ## Number of Fisher Scoring iterations: 4

``` r
car::vif(logitmodel)
```

    ##                 GVIF Df GVIF^(1/(2*Df))
    ## FinancesObj 1.087506  2        1.021193
    ## AnxietyObj  2.502737  2        1.257777
    ## StressObj   2.435859  2        1.249289
    ## DebtObj     1.178690  2        1.041957

``` r
exp(coefficients(logitmodel))
```

    ##           (Intercept) FinancesObjModFinCond FinancesObjLowFinCond 
    ##             0.5914949             3.5554290            15.8387430 
    ##  AnxietyObjModAnxiety  AnxietyObjLowAnxiety    StressObjModStress 
    ##             0.9721854             0.7791446             0.8281583 
    ##    StressObjLowStress        DebtObjModDebt        DebtObjLowDebt 
    ##             0.6259684             0.7398070             0.3347391

``` r
subjectivemodel <- glm(EmergencyFund ~ ConfidenceObj, family = binomial, data = data_use)
summary(subjectivemodel)
```

    ## 
    ## Call:
    ## glm(formula = EmergencyFund ~ ConfidenceObj, family = binomial, 
    ##     data = data_use)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.8085  -0.9979  -0.9979   1.3682   1.3682  
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)                -0.43799    0.01496  -29.28   <2e-16 ***
    ## ConfidenceObjModConfidence  1.11364    0.03625   30.72   <2e-16 ***
    ## ConfidenceObjLowConfidence  1.85652    0.05223   35.55   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 35147  on 25390  degrees of freedom
    ## Residual deviance: 32861  on 25388  degrees of freedom
    ##   (467 observations deleted due to missingness)
    ## AIC: 32867
    ## 
    ## Number of Fisher Scoring iterations: 4

``` r
exp(coefficients(subjectivemodel))
```

    ##                (Intercept) ConfidenceObjModConfidence 
    ##                   0.645334                   3.045427 
    ## ConfidenceObjLowConfidence 
    ##                   6.401411

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
