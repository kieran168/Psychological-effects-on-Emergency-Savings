Financial Literacy’s Impact on Financial Choices
================
Kieran Yuen

# Possible Hypotheses

What is the impact of consumerism on a person/household’s personal
finances?

What is the impact of consumerism on debt?

How does a course in personal finance in high school impact a person’s
finances in the long-term? short-term?

How much more income is earned by someone who has taken a personal
finance course in high school? In college? after graduating from
college?

How much more money is spent by people who use credit cards more often
on a daily basis versus people who use paper cash more often on a daily
basis?

Someone with great financial knowledge should have the understanding and
foresight to save for the future/emergency fund. *Make emergency fund
the dependent variable and use the objective questions as independent
variables. I would expect to see that those with correct answers in the
objective questions should have an emergency fund*

# Introduction

# Literature Review

## Article \#1

Jaclyn J. Beierlein, Margot Neverett, (2013). “Who takes personal
finance?”,
<http://ccny-proxy1.libr.ccny.cuny.edu/login?url=https://search.ebscohost.com/login.aspx?direct=true&db=bth&AN=94644713&site=ehost-live>

This article has certainly peaked my interests because I always believed
that if people took a course in personal finance that they would make
much smarter decisions with their money.

### Data

Institutional data from admission applications and transcripts of 17,499
students at East Carolina University. I believe this type of data should
be accessible by asking for it from a college or university if they can
provide it to me anonymized.

### Econometric Techniques

They made dummy variables (0/1) of all the variables they have and ran a
t-test to determine the difference between the group who took the
personal finance course and those who did not. They also performed a
logistic regression to account for spurious relationships amongst the
variables. Used ordinal regression to analyze students’ grades.

### What question is addressed?

This articles primary question is: What are the characteristics of
traditional undergraduate students that take the university personal
finance class?

### Findings

Assuming that enrollment in a personal finance course is considered
showing as a measure of interest, women demonstrate less interest in
personal finance than do men. Those with highest interest in a pesonal
finance course are: men, business, human ecology an social science
majors. Those students who are less likely to take a personal finance
course are: women, students with higher verbal SAT scores and GPAs, and
arts and education majors.

## Article \#2

Hancock, Adam M.; Jorgensen, Bryce L.; Swanson, Melvin S., (2013).
“College Students and Credit Card Use: The Role of Parents, Work
Experience, Financial Knowledge, and Credit Card Attitudes”,
<http://ccny-proxy1.libr.ccny.cuny.edu/login?url=https://search.ebscohost.com/login.aspx?direct=true&db=ecn&AN=1412539&site=ehost-live>

### Data

The data they used were from the College Student Financial Literacy
Surveys (CSFLS), which measures the financial knowledge, attitudes,
behavior, influences, and personal demographics that may affect the
fianncial literacy of college students.

### Econometric Techniques

Logistical regression to predict likelihood of having two or more credit
cards. Logistical regression predicting likelihood of having more than
$500 in credit card debt

### What question is addressed?

This study is trying to examine how students’ credit card behaviors
(i.e. number of credit cards and amount of debt) is influenced by:
parental interactions, years of work experience, financial knowledge,
credit card attitudes, and personal characteristics.

## Article \#3

Henager, R., Cude, B.J. Financial Literacy of High School Graduates:
Long- and Short-Term Financial Behavior by Age Group. J Fam Econ Iss 40,
564–575 (2019). <https://doi.org/10.1007/s10834-019-09626-2>

### Data

2015 National Financial Capability Study (NFCS) State-by-State Survey
Instrument sponsored by the Financial Industry Regulation Authority
(FINRA)

### Econometric Techniques

Ordered logistic regressions were run to analyze the key dependent
variables (when the dependent variable was an index of behaviors; either
0-3 or 0-4).

Logistic Regression was used for when the dependent variable was the
short-term variable budgeting.

### What question is addressed?

Examine the influence of financial literacy and financial education on
the long- and short-term financial behaviors, by age group for those
without a college degree.

### Findings

The study found that confidence in both financial knowledge and
financial ability are importanct influences on positive financial
behaviors for those without a college degree.

## Article \#4

Henager, R., Cude, B.J. Financial Literacy of High School Graduates:
Long- and Short-Term Financial Behavior by Age Group. J Fam Econ Iss 40,
564–575 (2019). <https://doi.org/10.1007/s10834-019-09626-2>

### Data

2015 National Financial Capability Study (NFCS) State-by-State Survey
Instrument sponsored by the Financial Industry Regulation Authority
(FINRA)

### Econometric Techniques

Ordered logistic regressions were run to analyze the key dependent
variables (when the dependent variable was an index of behaviors; either
0-3 or 0-4).

Logistic Regression was used for when the dependent variable was the
short-term variable budgeting.

### What question is addressed?

Examine the influence of financial literacy and financial education on
the long- and short-term financial behaviors, by age group for those
without a college degree.

### Findings

The study found that confidence in both financial knowledge and
financial ability are importanct influences on positive financial
behaviors for those without a college degree.

# Means (simple graphs, correlations, differences of means)

# Simple Regressions

# Complicated Regressions

# Conclusion (Explain Results)

``` r
library(haven)
NFCS_2018_State_Data <- read_sav("NFCS 2018 State Data.sav")
View(NFCS_2018_State_Data)
```
