---
title       : Predicting fuel consumption with linear regression
subtitle    : Using a wrapper method to select features
author      : Gonçalo Nogueira
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## The problem

We want to predict the fuel consumption of a car using linear regression
with possibly 10 different features.

The data is from the `mtcars` dataset available in R. It consists of 32
observations and 11 variables, one of which is `mpg` (miles per gallon) - our
target variable.

--- .class #id 

## The problem - Part 2

The problem when building a linear regression model for this purpose is:

### Which features should be included in the model?

---

## The solution

The app uses a wrapper method to select the best features to include in the
model. The user selects the number of features to be included and the app
selects and builds a model using the best combination of features.

The process of feature selection goes like this:

1. Build 10 simple linear regression models (one for each predictor) and
select the one that produces the highest $R^2$ score.

2. If the number of predictors to be included is greater than 1, build
9 multiple regression models with the predictor selected in the first
step as the first predictor and one of the other predictors as second
regressor. Select the model that produces the highest $R^2$ score.

3. Keep repeating step 2 until the number of predictors in the model
is equal to the number requested by the user.

---

## The results

Using this approach the variables can be ranked by their explanatory power.



The function `select.best.model` is the heart of the app and takes the
number of predictors to be used and selects the best ones to include in the model.

So if we call it with 10 predictors we will be able to get a ranking of the variables.


```r
model <- select.best.model(10)
attr(model$terms, "term.labels")
```

```
##  [1] "wt"   "cyl"  "hp"   "am"   "vs"   "carb" "disp" "gear" "drat" "qsec"
```





