Mental well-being and emergency savings
================
Kieran Yuen

# Outline of Paper

## Introduction

  - save this for last

## Literature Review

Economists have been studying how people make decisions since the
beginning days of the social science.

  - Here are some papers I am referencing as to why having an emergency
    fund is important to have and talking about it’s benefits

## Methods/Data

### Hypothesis

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

### Dataset used

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

#### Dependent Variable

The dependent variable will be question \#J5: *Have you set aside
emergency or rainy day funds that would cover your expenses for 3
months, in case of sickness, job loss, economic downturn, or other
emergencies?* The available answers were: “Yes,” “No,” “Don’t know,” and
“Prefer not to say.” A binary variable was created where “1” corresponds
to “Yes” and “0” means “No” this individual did not have an emergency
fund. Responses where the answers were “Don’t know” or “Prefer not to
say” were not included in the analysis.

#### Independent Variables

*The four key independent variables had (INSERT ANSWER HERE)
correlations with one anohter, indicating that the four varialbes were
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

### Means (simple graphs, correlations, differences of means)

### Simple Regressions

Do logistic regression on

### Complicated Regressions

## Results

  - Here is a scatterplot of my dep. variable and one of the ind.
    variables (lets do one for each ind. var. so that we can see what
    each one looks like)
  - Determine if squared or cubic or logarithmic terms would be useful
    by looking at the scatterplot of my regression
  - Determine if I want to look at certain subgroups within my data -
    maybe looking specifically on an income group might tell me
    something intersting about my data
  - Here is where I present some of my regression models (logit, probit)
    in easy-to-read tables (look at papers you have read as an example)
    -Here is where I present my main conclusion from what the regression
    has told me and where i try to do some “robustness checks” of the
    data (for example, I could look at the results by education level
    here and see )

## Discussion

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

## Limitations

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

## Conclusion

  - save this for last

# Overall goal

To find possible reasons why someone might not have an emergency fund
and propose ideas on how to address those issues to encourage/incentive
people to have an emergency fund.

# Variables

## Dependent variable

(J5) Emergency fund (Yes/No) *Have you set aside emergency or rainy day
funds that would cover your expenses for 3 months, in case of sickness,
job loss, economic downturn, or other emergencies?* Code this as 0/1,
exclude don’t know and prefer not to answer

## Independent variables (rate 1-10)

(J1) Personal Financial Condition *Overall, thinking of your assets,
debts and savings, how satisfied are you with your current personal
financial condition?* 10 = Extremely Satisfied 1 = Not at all Satisfied

8-10 = High\_Finances 4-7 = Moderate\_Finances 1-3 = Low\_Finances

(J33\_40) Anxiety about my personal finances (rate 1-7) *How strongly do
you agree or disagree with the following statements? - Thinking about my
personal finances can make me feel anxious* 7 = Strongly agree 1 =
Strongly disagree

6-7 = High\_Anxiety 3-5 = Moderate\_Anxiety 1-2 = Low\_Anxiety

(J33\_41) Personal finances make me feel stressed (rate 1-7) *How
strongly do you agree or disagree with the following statements? -
Discussing my finances can make my heart race or make me feel stressed*
7 = Strongly agree 1 = Strongly disagree

6-7 = High\_Stress 3-5 = Moderate\_Stress 1-2 = Low\_Stress

(G23) Too much debt right now in my life (rate 1-7) *How strongly do you
agree or disagree with the following statement? - I have too much debt
right now* 7 = Strongly agree 1 = Strongly disagree

6-7 = High\_Debt 3-5 = Moderate\_Debt 1-2 = Low\_Debt

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

# Steps for data

1)  Decide how to parse out the independent variables (answers range
    from 1-7 and 1-10). So I can do 1-2 = Low 3-5 = Moderate 6-7 = High

8-10 = High 4-7 = Moderate 1-3 = Low

2)  Find out what regressions I can do with my one (1) independent
    variable and four (4) dependent variables

3)  Prep data to be regressed

4)  Make sure Interactions can be regresses as well

5)  If interactions can be done, then prepare data to be able to be
    regressed

6)  
# Things to consider

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

# Coding

## Loading in Data

``` r
library(haven)
NFCS_2018_State_Data <- read_sav("NFCS 2018 State Data.sav")
View(NFCS_2018_State_Data)
```

## Recoding Variables

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
NFCS_2018_State_Data$EmergencyFund <- as.numeric(NFCS_2018_State_Data$J5) #Creating a new column for our dep. var.
NFCS_2018_State_Data$EmergencyFund <- recode(NFCS_2018_State_Data$EmergencyFund, '1' = 1, '2' = 0) #so that a '0' = no emergency fund and '1' = yes emergency fund

#NFCS_2018_State_Data$FinancialCondition <- as.factor(NFCS_2018_State_Data$J1) #Creating a new column 

#samplemodel <- lm(J5 ~ J1 + J33_40 + J33_41 + G23, data = NFCS_2018_State_Data)
#summary(samplemodel)
#car::vif(samplemodel)
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
detach()
```
