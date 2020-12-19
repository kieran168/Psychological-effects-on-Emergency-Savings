---
title: "Psychological effects on likelihood of having an emergency fund"
font-family: 'Corbel'
author: Kieran Yuen
output: github_document
---

# Loading in Data
```{r Loading NFCS database}
library(haven)
NFCS_2018_State_Data <- read_sav("NFCS 2018 State Data.sav")
View(NFCS_2018_State_Data)
detach()
```


# Preliminary Multicollinearity Check
```{r Preliminary Multicollinearity Check, echo=FALSE}
attach(NFCS_2018_State_Data)
cor(J1,J5)
cor(J33_40,J5)
cor(J33_41,J5)
cor(G23,J5)
cor(J1,J33_40)
cor(J1,J33_41)
cor(J1,G23)
cor(J33_40,J33_41)
cor(J33_40,G23)
cor(G23,J33_41)
detach()
```


# Preliminary data preparation

## Create new columns of data
```{r Create new columns of data}
attach(NFCS_2018_State_Data)
library(dplyr)

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
```{r Subsetting data}
attach(NFCS_2018_State_Data)
use_varb <- ((EmergencyFund == 1) | (EmergencyFund == 0))
data_use <- subset(NFCS_2018_State_Data, use_varb)
detach()
```



## Recoding Ind. Variables in Subsetted Database
```{r Recoding Ind. Variables in Subsetted Database}
attach(data_use)
library(dplyr)

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
```{r TABLE 2. Descriptive Statistics, echo=FALSE}
attach(data_use)
prop.table(table(EmergencyFund))
prop.table(table(FinancesObj))
prop.table(table(AnxietyObj))
prop.table(table(StressObj))
prop.table(table(DebtObj))
prop.table(table(ConfidenceObj))

prop.table(table(EducationLevel))
prop.table(table(Gender))
prop.table(table(Race))
prop.table(table(MaritalStatus))
prop.table(table(DepChildren))
prop.table(table(Employement))
prop.table(table(Income))
prop.table(table(AgeGroup))
detach()
```


# Regressions

## TABLE 3. Logistic Regression with Emergency Fund as Dependent Variable
```{r TABLE 3. Logistic Regression with Emergency Fund as Dependent Variable}
logitmodel <- glm(EmergencyFund ~ FinancesObj + AnxietyObj + DebtObj + ConfidenceObj + AgeGroup + Gender + Race + MaritalStatus + DepChildren + EducationLevel + Income + Employement, family = binomial, data = data_use)
summary(logitmodel)
car::vif(logitmodel)

exp(coefficients(logitmodel))
```

## TABLE 4. Logistic Regression with Emergency Fund as Dependent Variable, Demo Variables removed
```{r TABLE 4. Logistic Regression with Emergency Fund as Dependent Variable, Demo Variables removed}
logitmodel2 <- glm(EmergencyFund ~ FinancesObj + AnxietyObj + DebtObj + ConfidenceObj, family = binomial, data = data_use)
summary(logitmodel2)
car::vif(logitmodel2)

exp(coefficients(logitmodel2))
```



## TABLE 5. Logistic Regression with Emergency Fund as Dependent Variable
```{r TABLE 5. Logistic Regression with Emergency Fund as Dependent Variable}
logitmodel3 <- glm(EmergencyFund ~ Income, family = binomial, data = data_use)
summary(logitmodel3)

exp(coefficients(logitmodel3))
```

## TABLE 6. Logistic Model with Interaction between Anxiety and Confidence
```{r TABLE 6. Logistic Model with Interaction between Anxiety and Confidence}
interactionmodel1 <- glm(EmergencyFund ~ AnxietyObj:ConfidenceObj + FinancesObj + DebtObj + AgeGroup + Gender + Race + MaritalStatus + DepChildren + EducationLevel + Income + Employement, family = binomial, data = data_use)
summary(interactionmodel1)

exp(coefficients(interactionmodel1))
```


