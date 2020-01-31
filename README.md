

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Intern example 
```{r}
setwd("S:/Indiana Research & Evaluation/FHHC Homelessness/Data and QPR/YearlyReports")
SPARS_data = read.csv("FHHC.csv", header = TRUE, na.strings = c(-99, -98, -97, -1, -4, -5, -7, -9, -2, -6, -8, " "))
```
Check out the variables
Data is in long format, so reassessments are stacked.
```{r}
head(SPARS_data)

SPARS_data_base = subset(SPARS_data, InterviewType_07 == 1)

```
Select variables
```{r}
SPARS_data_base_example = data.frame(race = SPARS_data_base$RaceWhite, gender = SPARS_data_base$Gender, age = SPARS_data_base$Agegroup,hospital_nights =  SPARS_data_base$NightsHospitalMHC)
```
Review all variables
```{r}
library(psych)
SPARS_data_base_example[,1:2]= apply(SPARS_data_base_example[,1:2], 2, as.factor)
describe(SPARS_data_base_example)
```
Check out the missing data if any
```{r}
library(naniar)

miss_var_summary(SPARS_data_base_example)
miss_var_summary(SPARS_data)
```
Check outcome variable (nights in hospital)
```{r}
hist(SPARS_data_base_example$hospital_nights)
```
Clearly not normal so try a non-parametric test
```{r}
wilcox.test(SPARS_data_base_example$hospital_nights ~ SPARS_data_base_example$gender)
```

