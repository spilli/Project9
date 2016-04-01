---
title       : Miles Per Gallon Predictor
subtitle    : A shiny app that predicts the mpg of your car
author      : Sridhar Pilli
job         : Aspiring Data Scientist
framework   : html5slides        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

- MPG predictor is a shiny application that predicts the miles per gallon of a car given its
    - Engine displacement in cu.in.
    - Transmission type - Automatic or Manual
    - The number of carburetors used.

- The actual prediction is carried out using a linear regression model fitted on the **mtcars** dataset from the datasets package in R


```r
head(mtcars,4)
```

```
##                 mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4      21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag  21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710     22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive 21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
```

--- .class #id 

## Fitted model and its summary


```r
fit <- lm(mpg ~ disp + am + carb ,mtcars)
summary(fit)
```

```
## 
## Call:
## lm(formula = mpg ~ disp + am + carb, data = mtcars)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -5.1034 -1.6113 -0.4638  1.6840  5.0685 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 28.17607    1.50009  18.783  < 2e-16 ***
## disp        -0.02515    0.00558  -4.508 0.000106 ***
## am           3.80481    1.27529   2.983 0.005851 ** 
## carb        -1.36103    0.34587  -3.935 0.000500 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.628 on 28 degrees of freedom
## Multiple R-squared:  0.8283,	Adjusted R-squared:  0.8099 
## F-statistic: 45.02 on 3 and 28 DF,  p-value: 7.691e-11
```

---

## Fitted model and its summary
- The R-squared is 80.99% indicating about 80% of the variance is captured by this model. 
- All the variables considered has statistically significant beta values in the model. Hence this is a reasonably good model.
- Note that there is a negative association between engine displacement and mpg. As one increases, the other decreases.
- Likewise there is a negative association between number of carburetors and mpg.
- Overall manual cars have higher mpg than automatic transmission type cars.


---

## App usage

- Select the Engine displacement on the slider bar
- Select the Transmission type from the drop down menu
- Enter or select the Number of carburetors.

- The main panel on the righ displays the values entered, plots them and gives out the predicted mpg and its confidence interval.
- Confidence interval is calculated using the 95% confidence assuimng a t-distribution for the predicted mpg.

---

## Conclusion

- Overall the model seems to do a good job with a residual standard error of 2.628 on 28 degrees of freedom
- The model predicts appropriate mpg as per the associations with various variables - displacement, transmission type and number of carburetors. For eg., By selecting a higher engine displacement a lower predicted mpg is generated. 

---

## Code

- ui.R can be found [here](https://github.com/spilli/MPG_predictor/blob/master/ui.R)
- server.R can be found [here](https://github.com/spilli/MPG_predictor/blob/master/server.R)



