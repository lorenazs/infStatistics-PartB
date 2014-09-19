Statistical Inference Project Part B
========================================================

This is the second part of the Statistical Inference´s course project.  
In this project the data set about the effect of vitamin C on tooth growth in 10
Guinea Pigs, at each of three dose levels (0.5mg, 1mg, 2mg) with each of two
delivery methods (OJ,VC)

### Loading the ToothGrowth data

```r

data(ToothGrowth)
library(ggplot2)
```

### Exploratory data analysis

Basically the data set contains 3 variables and 60 observations about the tooth growth in guinea pigs.
The variables are  len(the tooth length), supp  (the type of supplement VC or OJ) and dose (the dose in milligrams)


```r

head(ToothGrowth)
```

```
##    len supp dose
## 1  4.2   VC  0.5
## 2 11.5   VC  0.5
## 3  7.3   VC  0.5
## 4  5.8   VC  0.5
## 5  6.4   VC  0.5
## 6 10.0   VC  0.5
```

```r
summary(ToothGrowth)
```

```
##       len       supp         dose     
##  Min.   : 4.2   OJ:30   Min.   :0.50  
##  1st Qu.:13.1   VC:30   1st Qu.:0.50  
##  Median :19.2           Median :1.00  
##  Mean   :18.8           Mean   :1.17  
##  3rd Qu.:25.3           3rd Qu.:2.00  
##  Max.   :33.9           Max.   :2.00
```

When observing the len vs the dose variables, it can be observed three well defined groups: 
those which received 0.5 mg dose, 1mg dose or 2mg dose

```r
qplot(dose, len, data = ToothGrowth, color = supp)
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 


### Confidence Intervals and hypothesis tests to compare tooth growth by supp and dose

```r
t.test(ToothGrowth$len ~ ToothGrowth$supp, paired = FALSE, var.equal = TRUE, 
    data = ToothGrowth, conf.level = 0.95)
```

```
## 
## 	Two Sample t-test
## 
## data:  ToothGrowth$len by ToothGrowth$supp 
## t = 1.915, df = 58, p-value = 0.06039
## alternative hypothesis: true difference in means is not equal to 0 
## 95 percent confidence interval:
##  -0.167  7.567 
## sample estimates:
## mean in group OJ mean in group VC 
##            20.66            16.96
```

```r

dose05 <- ToothGrowth[ToothGrowth$dose == 0.5, ]

t.test(dose05$len ~ dose05$supp, paired = FALSE, var.equal = TRUE, data = ToothGrowth)
```

```
## 
## 	Two Sample t-test
## 
## data:  dose05$len by dose05$supp 
## t = 3.17, df = 18, p-value = 0.005304
## alternative hypothesis: true difference in means is not equal to 0 
## 95 percent confidence interval:
##  1.77 8.73 
## sample estimates:
## mean in group OJ mean in group VC 
##            13.23             7.98
```

```r

dose1mg <- ToothGrowth[ToothGrowth$dose == 1, ]

t.test(dose1mg$len ~ dose1mg$supp, paired = FALSE, var.equal = TRUE, data = ToothGrowth)
```

```
## 
## 	Two Sample t-test
## 
## data:  dose1mg$len by dose1mg$supp 
## t = 4.033, df = 18, p-value = 0.0007807
## alternative hypothesis: true difference in means is not equal to 0 
## 95 percent confidence interval:
##  2.841 9.019 
## sample estimates:
## mean in group OJ mean in group VC 
##            22.70            16.77
```

```r

dose2mg <- ToothGrowth[ToothGrowth$dose == 2, ]

t.test(dose2mg$len ~ dose2mg$supp, paired = FALSE, var.equal = TRUE, data = ToothGrowth)
```

```
## 
## 	Two Sample t-test
## 
## data:  dose2mg$len by dose2mg$supp 
## t = -0.0461, df = 18, p-value = 0.9637
## alternative hypothesis: true difference in means is not equal to 0 
## 95 percent confidence interval:
##  -3.723  3.563 
## sample estimates:
## mean in group OJ mean in group VC 
##            26.06            26.14
```

 

 
### Conclusions and assumptions needed for your conclusions
 
 In this case the assumptions are:
  
  - Given that all the pigs came from the same population I assume a constant variance
  - From the description of the data, I assume that the doses were applied to a different
    set of guinea pigs, therefore the samples are not paired.
