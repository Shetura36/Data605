---
title: "Data 605 FINAL - Problem 2"
author: "S. Tinapunan"
date: "December 16, 2018"
output: 
  html_document: 
    keep_md: yes
---






---

## <span style="color:blue"> Part 4: Modeling </span>

Build some type of multiple regression  model and submit your model to the competition board.  Provide your complete model summary and results with analysis. Report your Kaggle.com  user name and score.

<br /> 

### Training Data

Source: https://www.kaggle.com/c/house-prices-advanced-regression-techniques

- No. of observations: 1460
- No. of attributes: 81


```r
house_data <- read.csv(file="train.csv", header=TRUE, sep=",")
```



---

### Introduction 

<br /> 

The aim of this project is to create a multiple regression model that predicts the Sale Price of houses in the given data set. This data set has 79 explanatory variables. 

This model uses 17 explanatory variables. Some of these variables are used to generate calculated variables. Below is a list of these. 

<br /> 

-  *Neighborhood*: used to create a new variable *NeighborhoodGroup*. 

-  *YearRemodAdd, YrSold*: used to create a new variable *SinceRemod*. This is the number of years since remodeled at time of sale. The remodeled value is equal to construction year if property was never remodeled. 

- *TotalBsmtSF, X1stFlrSF, X2ndFlrSF, GarageArea, PoolArea*: used to generate a new variable called *OverallArea*. 

- *SaleCondition*: used to create a new variable *IsAbnormalSale*. This is set to 1 when the sale is abnormal (e.g., foreclosures)

- *Functional*: used to create a new variable *IsReduced* when the functional level of the property is not normal. 

- *KitchenQual*: used to create a new variable *KitchenQualGroup* that groups the kitchen into high, medium, and low quality levels. 

- *FireplaceQu*: used to create a new variable *ExcellentFireplace* that flags properties with excellent fireplaces. 

- *GarageQual*: used to create a new variable *ExcellentGarage* that flags properties with excellent garages. 

- *PoolQC*: used to create a new variable *ExcellentPool* that flags properties with excellent pools. 

- *OverallQual*: used to create a new variable *OverallQualityHigh* that flags properties with high overall conditions. 

- *MasVnrArea*

- *CentralAir* 


<br /> 

---

### Neighborhood 

We all know that location is one important factor that determines the price of any real estate. So I went ahead and did a linear regression on *Sale Price* by *Neighborhood*. 

<br /> 


```r
m <- lm(SalePrice ~ Neighborhood, data=house_data)
```

<br /> 

As you can see in the summary below, there are a lot of neighborhoods. In total, there are 25 different neighborhoods. In addition, some of the estimators for the neighborhoods are not really significant; however, a good number of the estimators are significant. The adjusted-R-squared is 0.538, which means that the variable *neighborhood* explains about 50% of the variability in sale price in this single variable regression. 

<br /> 



```
## 
## Call:
## lm(formula = SalePrice ~ Neighborhood, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -162271  -27552   -5324   19685  419705 
## 
## Coefficients:
##                     Estimate Std. Error t value Pr(>|t|)    
## (Intercept)           194871      13097  14.879  < 2e-16 ***
## NeighborhoodBlueste   -57371      40367  -1.421 0.155463    
## NeighborhoodBrDale    -90377      18809  -4.805 1.71e-06 ***
## NeighborhoodBrkSide   -70037      14893  -4.703 2.81e-06 ***
## NeighborhoodClearCr    17695      16603   1.066 0.286721    
## NeighborhoodCollgCr     3095      13819   0.224 0.822820    
## NeighborhoodCrawfor    15754      15123   1.042 0.297712    
## NeighborhoodEdwards   -66651      14166  -4.705 2.78e-06 ***
## NeighborhoodGilbert    -2016      14437  -0.140 0.888944    
## NeighborhoodIDOTRR    -94747      15822  -5.988 2.67e-09 ***
## NeighborhoodMeadowV   -96294      18522  -5.199 2.29e-07 ***
## NeighborhoodMitchel   -38601      15200  -2.540 0.011204 *  
## NeighborhoodNAmes     -49024      13582  -3.609 0.000318 ***
## NeighborhoodNoRidge   140424      15577   9.015  < 2e-16 ***
## NeighborhoodNPkVill   -52176      22260  -2.344 0.019217 *  
## NeighborhoodNridgHt   121400      14470   8.390  < 2e-16 ***
## NeighborhoodNWAmes     -5821      14542  -0.400 0.689011    
## NeighborhoodOldTown   -66646      14047  -4.744 2.30e-06 ***
## NeighborhoodSawyer    -58078      14523  -3.999 6.69e-05 ***
## NeighborhoodSawyerW    -8315      14864  -0.559 0.575974    
## NeighborhoodSomerst    30509      14333   2.129 0.033456 *  
## NeighborhoodStoneBr   115628      16975   6.812 1.42e-11 ***
## NeighborhoodSWISU     -52280      16975  -3.080 0.002111 ** 
## NeighborhoodTimber     47377      15756   3.007 0.002686 ** 
## NeighborhoodVeenker    43902      20895   2.101 0.035810 *  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 54000 on 1435 degrees of freedom
## Multiple R-squared:  0.5456,	Adjusted R-squared:  0.538 
## F-statistic: 71.78 on 24 and 1435 DF,  p-value: < 2.2e-16
```

<br /> 

Based on common knowledge, I know that certain areas are more affordable and others are more expensive. Since I do not have any additional information on which neighborhood would tend to have more affordable and which ones are more expensive, I used the output of the linear regression above to rank the neighborhood based on the values of the estimators. The base group in the estimate is *Blmngtn*.



Neighborhood   Estimate   Group   
-------------  ---------  --------
NoRidge        140424     Group C 
NridgHt        121400     Group C 
StoneBr        115628     Group C 
Timber         47377      Group C 
Veenker        43902      Group C 
Somerst        30509      Group C 
ClearCr        17695      Group B 
Crawfor        15754      Group B 
CollgCr        3095       Group B 
Blmngtn        base       Group B 
Gilbert        -2016      Group B 
NWAmes         -5821      Group B 
SawyerW        -8315      Group B 
Mitchel        -38601     Group A 
NAmes          -49024     Group A 
NPkVill        -52176     Group A 
SWISU          -52280     Group A 
Blueste        -57371     Group A 
Sawyer         -58078     Group A 
OldTown        -66646     Group A 
Edwards        -66651     Group A 
BrkSide        -70037     Group A 
BrDale         -90377     Group A 
IDOTRR         -94747     Group A 
MeadowV        -96294     Group A 

I divided the 25 neighborhoods into 3 groups - A, B, and C. 




```r
#Neighborhood: NeighborhoodGroup 

house_data$NeighborhoodGroup[house_data$Neighborhood %in% 
    c('NoRidge',	'NridgHt',	'StoneBr',	'Timber',	'Veenker',	'Somerst')] <- "GroupC"

house_data$NeighborhoodGroup[house_data$Neighborhood %in% 
    c('ClearCr',	'Crawfor',	'CollgCr',	'Blmngtn',	'Gilbert',	'NWAmes',	'SawyerW')] <- "GroupB"

house_data$NeighborhoodGroup[house_data$Neighborhood %in%
    c('Mitchel',	'NAmes',	'NPkVill',	'SWISU',	'Blueste',	'Sawyer',	'OldTown',	'Edwards',	
      'BrkSide',	'BrDale',	'IDOTRR',	'MeadowV')] <- "GroupA"
```


<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-9-1.png)<!-- -->


<br /> 


Running the linear model on *NeighborhoodGroup*, this is the result: 


```r
summary(lm(SalePrice ~ NeighborhoodGroup, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -139755  -29240   -5240   23157  477745 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)               134240       2162   62.08   <2e-16 ***
## NeighborhoodGroupGroupB    62138       3478   17.87   <2e-16 ***
## NeighborhoodGroupGroupC   143016       4107   34.82   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 58220 on 1457 degrees of freedom
## Multiple R-squared:  0.4636,	Adjusted R-squared:  0.4629 
## F-statistic: 629.7 on 2 and 1457 DF,  p-value: < 2.2e-16
```

All base group is *GroupA*, and the estimators for the groups are significant. The adjusted R-squared is 0.4629, which is lower than the previous value of 0.5380. 


<br /> 

---

### YearRemodAdd, YrSold

<br /> 

The *YearRemodAdd* is the remodel date, and it is same as construction date if no remodeling or additions. *YrSold* is the year when the property was sold. 

The calculated variable *SinceRemod* is the number of years since the property had remodeling or additions done when at the time it was sold.



```r
#YearRemodAdd, YrSold: SinceRemod
house_data$SinceRemod <- house_data$YrSold - house_data$YearRemodAdd
```

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

<br /> 

As you can, there is an inverse relationship between sale price and number of years since last remodeled (or if never remodeled this is number of years since house was built at time of sale). 

<br /> 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -137405  -29662   -5083   21787  482313 
## 
## Coefficients:
##                          Estimate Std. Error t value Pr(>|t|)    
## (Intercept)             161617.95    3597.22  44.929   <2e-16 ***
## NeighborhoodGroupGroupB  47342.02    3728.64  12.697   <2e-16 ***
## NeighborhoodGroupGroupC 120745.53    4643.48  26.003   <2e-16 ***
## SinceRemod                -806.39      86.01  -9.376   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 56560 on 1456 degrees of freedom
## Multiple R-squared:  0.4942,	Adjusted R-squared:  0.4931 
## F-statistic: 474.1 on 3 and 1456 DF,  p-value: < 2.2e-16
```

<br /> 

Running the model with *SinceRemod* increases the adjusted R-squared from 0.4629 to 0.4931. All the estimators are significant. 

<br /> 

---

### TotalBsmtSF, X1stFlrSF, X2ndFlrSF, GarageArea, PoolArea

<br /> 

The variables *TotalBsmtSF, X1stFlrSF, X2ndFlrSF, GarageArea, PoolArea* are quantitative variables that measure the area (in square feet) of the basement, first and second floor, garage area, and pool area respectively. A new variable is created called *OverallArea*, which sums the areas of all these spaces. 

<br /> 


```r
#OverallArea: TotalBsmtSF, X1stFlrSF, X2ndFlrSF, GarageArea, PoolArea
house_data$OverallArea <- house_data$TotalBsmtSF + house_data$X1stFlrSF + house_data$X2ndFlrSF + house_data$GarageArea + house_data$PoolArea
```

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

Running the model with *OverallArea* updates the model as follows. 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea, 
##     data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -539894  -18058     124   15946  297998 
## 
## Coefficients:
##                          Estimate Std. Error t value Pr(>|t|)    
## (Intercept)             21044.527   4344.702   4.844 1.41e-06 ***
## NeighborhoodGroupGroupB 23476.480   2658.836   8.830  < 2e-16 ***
## NeighborhoodGroupGroupC 64145.197   3528.119  18.181  < 2e-16 ***
## SinceRemod               -479.797     60.300  -7.957 3.52e-15 ***
## OverallArea                49.733      1.258  39.546  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 39280 on 1455 degrees of freedom
## Multiple R-squared:  0.7562,	Adjusted R-squared:  0.7555 
## F-statistic:  1128 on 4 and 1455 DF,  p-value: < 2.2e-16
```

<br /> 

Including *OverallArea* in the model increased the adjusted R-squared from 0.4931 to 0.7555. All the estimators are significant. 

<br /> 

---

### SaleCondition

<br /> 

The variable *SaleCondition* captures a category level *Abnorml*, which describes an abnormal sale such as trade, foreclosure, and short sale. A new variable *IsAbnormalSale* is created that flags this condition. 

<br /> 


```r
#IsAbnormalSale: SaleCondition when 'Abnorml'
house_data$IsAbnormalSale[house_data$SaleCondition == "Abnorml"] = 1
house_data$IsAbnormalSale[house_data$SaleCondition != "Abnorml"] = 0
```

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

<br /> 


```
## Warning: Continuous x aesthetic -- did you forget aes(group=...)?
```

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-19-1.png)<!-- -->

<br /> 

Running the model with *IsAbnormalSale* gives the following result. 

<br /> 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -540378  -18127     111   15793  297383 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              21681.537   4336.208   5.000 6.43e-07 ***
## NeighborhoodGroupGroupB  23154.949   2652.713   8.729  < 2e-16 ***
## NeighborhoodGroupGroupC  63991.474   3517.720  18.191  < 2e-16 ***
## SinceRemod                -461.732     60.390  -7.646 3.75e-14 ***
## OverallArea                 49.721      1.254  39.658  < 2e-16 ***
## IsAbnormalSale          -12832.356   4078.789  -3.146  0.00169 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 39160 on 1454 degrees of freedom
## Multiple R-squared:  0.7579,	Adjusted R-squared:  0.757 
## F-statistic: 910.1 on 5 and 1454 DF,  p-value: < 2.2e-16
```

<br /> 

Including *IsAbnormalSale* in the model increased the adjusted R-squared from 0.7555 to 0.7570. All the estimators are significant. 

<br /> 

---

### Functional 

The variable *Functional* describes the functional level of the property. The new variable *IsReduced* flags those properties whose sale price were reduced because of less than normal functional levels. 

<br /> 



```r
#IsReduced: Functional
house_data$IsReduced <- 0
house_data$IsReduced[house_data$Functional %in% c("Min1", "Min2", "Mod", "Maj1", "Maj2", "Sev", "Sal")] <- 1
```

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-22-1.png)<!-- -->

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-23-1.png)<!-- -->

<br /> 

Running the model with *IsReduced* gives the following result. 

<br /> 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale + IsReduced, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale + IsReduced, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -546997  -18132       3   15161  295505 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              22320.407   4314.599   5.173 2.62e-07 ***
## NeighborhoodGroupGroupB  21661.005   2661.970   8.137 8.60e-16 ***
## NeighborhoodGroupGroupC  61862.044   3534.942  17.500  < 2e-16 ***
## SinceRemod                -458.138     60.058  -7.628 4.28e-14 ***
## OverallArea                 50.159      1.251  40.091  < 2e-16 ***
## IsAbnormalSale          -12922.799   4055.970  -3.186  0.00147 ** 
## IsReduced               -17153.569   4106.567  -4.177 3.13e-05 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 38940 on 1453 degrees of freedom
## Multiple R-squared:  0.7607,	Adjusted R-squared:  0.7597 
## F-statistic: 769.9 on 6 and 1453 DF,  p-value: < 2.2e-16
```

<br /> 

Including *IsReduced* increased the adjusted R-squared from 0.7570 to 0.7597. All estimators are significant. 

<br /> 

---

### KitchenQual

<br /> 

The variable *KitchenQual* has 5 different category levels. Running the model without modifying this variable yielded some estimators that were not significant. The variable *KitchenQualGroup* collapses the 5 levels into 3 groups of high, medium, and low. 

<br /> 



```r
#KitchenQual - KitchenQualGroup
house_data$KitchenQualGroup[house_data$KitchenQual %in% c('Ex')] <- "High"
house_data$KitchenQualGroup[house_data$KitchenQual %in% c('Gd')] <- "Medium"
house_data$KitchenQualGroup[house_data$KitchenQual %in% c('Fa', 'TA', 'Po')] <- "Low"
house_data$KitchenQualGroup <- factor(house_data$KitchenQualGroup)
house_data$KitchenQualGroup <- relevel(house_data$KitchenQualGroup, ref="Low")
```


<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-26-1.png)<!-- -->

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-27-1.png)<!-- -->

<br /> 

Running the model with *KitchenQualGroup* gives the following result. 

<br /> 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale + IsReduced + KitchenQualGroup, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale + IsReduced + KitchenQualGroup, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -543188  -17467    -531   14830  272878 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              27633.508   4242.041   6.514 1.00e-10 ***
## NeighborhoodGroupGroupB  23157.806   2590.991   8.938  < 2e-16 ***
## NeighborhoodGroupGroupC  54424.616   3473.461  15.669  < 2e-16 ***
## SinceRemod                -297.760     64.070  -4.647 3.67e-06 ***
## OverallArea                 44.886      1.255  35.763  < 2e-16 ***
## IsAbnormalSale          -15207.386   3841.335  -3.959 7.89e-05 ***
## IsReduced               -14857.451   3894.247  -3.815 0.000142 ***
## KitchenQualGroupHigh     62865.836   4950.620  12.699  < 2e-16 ***
## KitchenQualGroupMedium    9208.140   2793.350   3.296 0.001003 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 36820 on 1451 degrees of freedom
## Multiple R-squared:  0.7863,	Adjusted R-squared:  0.7852 
## F-statistic: 667.6 on 8 and 1451 DF,  p-value: < 2.2e-16
```

<br /> 

Including *KitchenQualGroup* in the model increased the adjusted R-squared from 0.7597 to 0.7852. All estimators are significant. 

<br /> 

---

### FireplaceQu

<br /> 

The variable *FireplaceQu* describes the quality of the fireplace. In my previous trial and error with categorical variables that have different levels of quality, I find that some of the levels do not have estimators that are significant. I have decided to focus on properties that have excellent fireplaces, and reviewing the plots below properties with excellent fireplaces tend to have higher sale prices. 

The variable *ExcellentFireplace* flags those with excellent fireplaces. 

<br/> 


```r
#FireplaceQu
house_data$ExcellentFireplace<- 0
house_data$ExcellentFireplace[house_data$FireplaceQu %in% c('Ex')] <- 1
```

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-30-1.png)<!-- -->

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-31-1.png)<!-- -->

<br /> 

Running the model with *ExcellentFireplace* gives the following result. 

<br /> 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale + IsReduced + 
             KitchenQualGroup + ExcellentFireplace, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale + IsReduced + KitchenQualGroup + ExcellentFireplace, 
##     data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -534852  -18065    -477   14829  255238 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              28684.913   4231.666   6.779 1.76e-11 ***
## NeighborhoodGroupGroupB  23657.789   2582.472   9.161  < 2e-16 ***
## NeighborhoodGroupGroupC  54267.363   3457.779  15.694  < 2e-16 ***
## SinceRemod                -296.534     63.777  -4.650 3.63e-06 ***
## OverallArea                 44.430      1.255  35.399  < 2e-16 ***
## IsAbnormalSale          -15729.775   3826.195  -4.111 4.16e-05 ***
## IsReduced               -14474.575   3877.700  -3.733 0.000197 ***
## KitchenQualGroupHigh     59699.802   4998.039  11.945  < 2e-16 ***
## KitchenQualGroupMedium    8995.305   2781.104   3.234 0.001246 ** 
## ExcellentFireplace       29985.922   7901.663   3.795 0.000154 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 36650 on 1450 degrees of freedom
## Multiple R-squared:  0.7885,	Adjusted R-squared:  0.7871 
## F-statistic: 600.5 on 9 and 1450 DF,  p-value: < 2.2e-16
```

<br /> 

Including *ExcellentFireplace* increased the adjusted R-squared from 0.7852 to 0.7871. All estimators are significant. 

<br /> 

---

### GarageQual

<br /> 

The variable *GarageQual* describes the quality of the garage. The variable *ExcellentGarage* flags houses with excellent garages. 

<br /> 


```r
#GarageQual
house_data$ExcellentGarage <- 0
house_data$ExcellentGarage[house_data$GarageQual %in% c('Ex')] <- 1
```

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-34-1.png)<!-- -->

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-35-1.png)<!-- -->

<br /> 

Running the model with *ExcellentGarage* gives the following result. 

<br /> 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale + IsReduced + 
             KitchenQualGroup + ExcellentFireplace + ExcellentGarage, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale + IsReduced + KitchenQualGroup + ExcellentFireplace + 
##     ExcellentGarage, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -533238  -17954    -405   14884  255884 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              28739.913   4219.711   6.811 1.42e-11 ***
## NeighborhoodGroupGroupB  23958.073   2577.043   9.297  < 2e-16 ***
## NeighborhoodGroupGroupC  54738.012   3451.448  15.859  < 2e-16 ***
## SinceRemod                -301.849     63.620  -4.745 2.30e-06 ***
## OverallArea                 44.371      1.252  35.449  < 2e-16 ***
## IsAbnormalSale          -15493.043   3816.143  -4.060 5.17e-05 ***
## IsReduced               -14228.549   3867.555  -3.679 0.000243 ***
## KitchenQualGroupHigh     58836.975   4991.936  11.786  < 2e-16 ***
## KitchenQualGroupMedium    8869.918   2773.528   3.198 0.001413 ** 
## ExcellentFireplace       30403.653   7880.463   3.858 0.000119 ***
## ExcellentGarage          64507.044  21204.164   3.042 0.002391 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 36550 on 1449 degrees of freedom
## Multiple R-squared:  0.7898,	Adjusted R-squared:  0.7883 
## F-statistic: 544.4 on 10 and 1449 DF,  p-value: < 2.2e-16
```

<br /> 

Including *ExcellentGarage* increased the adjusted R-squared from 0.7871 to 0.7883. All estimators are significant. 

<br /> 

---

### PoolQC

<br /> 

The variable *PoolQC* describes the quality of the pool. The new variable *ExcellentPool* flags properties with excellent pools. 

<br /> 




<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-38-1.png)<!-- -->

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-39-1.png)<!-- -->

<br /> 

Running the model with *ExcellentPool* gives the following result. 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale + IsReduced + 
             KitchenQualGroup + ExcellentFireplace + ExcellentGarage + ExcellentPool, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale + IsReduced + KitchenQualGroup + ExcellentFireplace + 
##     ExcellentGarage + ExcellentPool, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -525458  -17696    -265   14985  255218 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              30634.759   4222.363   7.255 6.51e-13 ***
## NeighborhoodGroupGroupB  24451.458   2565.963   9.529  < 2e-16 ***
## NeighborhoodGroupGroupC  55518.337   3438.102  16.148  < 2e-16 ***
## SinceRemod                -300.701     63.277  -4.752 2.21e-06 ***
## OverallArea                 43.640      1.258  34.700  < 2e-16 ***
## IsAbnormalSale          -17647.202   3831.823  -4.605 4.48e-06 ***
## IsReduced               -13919.965   3847.417  -3.618 0.000307 ***
## KitchenQualGroupHigh     59135.120   4965.524  11.909  < 2e-16 ***
## KitchenQualGroupMedium    8909.968   2758.574   3.230 0.001266 ** 
## ExcellentFireplace       26817.001   7886.709   3.400 0.000691 ***
## ExcellentGarage          64770.585  21089.808   3.071 0.002172 ** 
## ExcellentPool           108539.628  26504.527   4.095 4.45e-05 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 36350 on 1448 degrees of freedom
## Multiple R-squared:  0.7922,	Adjusted R-squared:  0.7906 
## F-statistic: 501.8 on 11 and 1448 DF,  p-value: < 2.2e-16
```

Including *ExcellentPool* in the model increased the adjusted R-squared from 0.7883 to 0.7906. All estimators are significant. 

<br /> 

---

### OverallQual, MasVnrArea, CentralAir

<br /> 

The variable *OverallQual* describes the overall quality of the house. This variable has 10 different levels. When I included this variable in the model as is, the estimator was not significant. The different levels are coded as integers. Upon reviewing the box plot of this variable, I noticed a clear trend that houses with better overall quality sold for higher prices. 

The variable *OverallQualityHigh* flags properties with quality scores of 8, 9, and 10. I also tried breaking the 10 different levels into high, medium, and low; however, this resulted in some estimators that were not significant. 

The variable *MasVnrArea* is the veneer area in square feet. 

The variable *CentralAir* indicates if property has central air conditioning or not. 

<br /> 



```r
#OverallQual
house_data$OverallQualityHigh <- 0
house_data$OverallQualityHigh[house_data$OverallQual %in% c(8,9,10)] <- 1
```

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-42-1.png)<!-- -->

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-43-1.png)<!-- -->

<br /> 

Running the model with *OverallQualityHigh* gives the following result. 

<br /> 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale + IsReduced + 
             KitchenQualGroup + ExcellentFireplace + ExcellentGarage + ExcellentPool + 
              OverallQualityHigh, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale + IsReduced + KitchenQualGroup + ExcellentFireplace + 
##     ExcellentGarage + ExcellentPool + OverallQualityHigh, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -507915  -16263    -176   14493  265628 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              38919.246   4212.929   9.238  < 2e-16 ***
## NeighborhoodGroupGroupB  24724.972   2498.321   9.897  < 2e-16 ***
## NeighborhoodGroupGroupC  45168.215   3539.968  12.759  < 2e-16 ***
## SinceRemod                -284.823     61.630  -4.622 4.15e-06 ***
## OverallArea                 40.195      1.283  31.327  < 2e-16 ***
## IsAbnormalSale          -17413.701   3730.625  -4.668 3.33e-06 ***
## IsReduced               -12302.462   3750.041  -3.281  0.00106 ** 
## KitchenQualGroupHigh     47462.397   5005.854   9.481  < 2e-16 ***
## KitchenQualGroupMedium    7195.338   2692.430   2.672  0.00761 ** 
## ExcellentFireplace       23207.879   7688.739   3.018  0.00259 ** 
## ExcellentGarage          59661.403  20540.205   2.905  0.00373 ** 
## ExcellentPool           104081.991  25808.689   4.033 5.80e-05 ***
## OverallQualityHigh       32872.630   3659.353   8.983  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 35390 on 1447 degrees of freedom
## Multiple R-squared:  0.8032,	Adjusted R-squared:  0.8015 
## F-statistic: 492.1 on 12 and 1447 DF,  p-value: < 2.2e-16
```

<br /> 

Including *OverallQualityHigh* in the model increased the adjusted R-squared from 0.7906 to 0.8015. All estimators are significant. 

<br />

Inculding *MasVnrArea* in the model increased the adjusted R-squared to 0.8048. All estimators are significant. 

<br /> 


```r
summary(lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale + IsReduced + 
             KitchenQualGroup + ExcellentFireplace + ExcellentGarage + ExcellentPool + 
              OverallQualityHigh + MasVnrArea, data=house_data))
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale + IsReduced + KitchenQualGroup + ExcellentFireplace + 
##     ExcellentGarage + ExcellentPool + OverallQualityHigh + MasVnrArea, 
##     data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -504314  -16424     -17   13922  247510 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              42718.818   4247.930  10.056  < 2e-16 ***
## NeighborhoodGroupGroupB  24847.742   2477.169  10.031  < 2e-16 ***
## NeighborhoodGroupGroupC  42874.282   3560.382  12.042  < 2e-16 ***
## SinceRemod                -294.750     61.049  -4.828 1.53e-06 ***
## OverallArea                 38.052      1.341  28.368  < 2e-16 ***
## IsAbnormalSale          -17252.257   3693.129  -4.671 3.27e-06 ***
## IsReduced               -10299.096   3739.744  -2.754  0.00596 ** 
## KitchenQualGroupHigh     46220.170   4967.850   9.304  < 2e-16 ***
## KitchenQualGroupMedium    7916.816   2672.772   2.962  0.00311 ** 
## ExcellentFireplace       22824.924   7617.646   2.996  0.00278 ** 
## ExcellentGarage          63899.310  20345.619   3.141  0.00172 ** 
## ExcellentPool           117917.603  25682.422   4.591 4.79e-06 ***
## OverallQualityHigh       31406.265   3655.204   8.592  < 2e-16 ***
## MasVnrArea                  30.844      5.951   5.183 2.49e-07 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 35030 on 1438 degrees of freedom
##   (8 observations deleted due to missingness)
## Multiple R-squared:  0.8065,	Adjusted R-squared:  0.8048 
## F-statistic: 461.1 on 13 and 1438 DF,  p-value: < 2.2e-16
```



Lastyly, adding *CentralAir* to the model increased the adjusted R-squared to 0.8065. All estimators are significant. 


```r
model <- lm(SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + IsAbnormalSale + IsReduced + 
             KitchenQualGroup + ExcellentFireplace + ExcellentGarage + ExcellentPool + 
              OverallQualityHigh + MasVnrArea + CentralAir, data=house_data)
summary(model)
```

```
## 
## Call:
## lm(formula = SalePrice ~ NeighborhoodGroup + SinceRemod + OverallArea + 
##     IsAbnormalSale + IsReduced + KitchenQualGroup + ExcellentFireplace + 
##     ExcellentGarage + ExcellentPool + OverallQualityHigh + MasVnrArea + 
##     CentralAir, data = house_data)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -500221  -16098     161   13705  249142 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              29597.605   5534.000   5.348 1.03e-07 ***
## NeighborhoodGroupGroupB  24363.267   2469.974   9.864  < 2e-16 ***
## NeighborhoodGroupGroupC  42587.343   3545.845  12.010  < 2e-16 ***
## SinceRemod                -250.497     61.966  -4.043 5.57e-05 ***
## OverallArea                 37.628      1.341  28.069  < 2e-16 ***
## IsAbnormalSale          -17385.937   3677.338  -4.728 2.49e-06 ***
## IsReduced                -9549.326   3729.152  -2.561 0.010547 *  
## KitchenQualGroupHigh     46712.205   4948.178   9.440  < 2e-16 ***
## KitchenQualGroupMedium    7982.469   2661.273   2.999 0.002751 ** 
## ExcellentFireplace       22853.123   7584.708   3.013 0.002632 ** 
## ExcellentGarage          61809.474  20265.609   3.050 0.002331 ** 
## ExcellentPool           118176.450  25571.458   4.621 4.15e-06 ***
## OverallQualityHigh       32106.491   3644.377   8.810  < 2e-16 ***
## MasVnrArea                  29.824      5.932   5.028 5.58e-07 ***
## CentralAirY              14439.168   3927.211   3.677 0.000245 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 34880 on 1437 degrees of freedom
##   (8 observations deleted due to missingness)
## Multiple R-squared:  0.8083,	Adjusted R-squared:  0.8065 
## F-statistic: 432.9 on 14 and 1437 DF,  p-value: < 2.2e-16
```



<br /> 

The variance inflation factor for the final model is 5.217287. Usually, VIF values under 10 does not suggest multicolinearity. 



```r
VIF(model)
```

```
## [1] 5.217287
```

<br /> 

![](STinapunan_Data605_FINAL_MLR_version2_files/figure-html/unnamed-chunk-48-1.png)<!-- -->

<br /> 

The residual vs fitted plot shows an approximately horizontal line, which suggests that the relationship is linear. 

The normal Q-Q plot is somewhat approximately normal, which suggests that the residuals are approximately normally distributed; however, the points towards the end of the tail deviate from the line. 

The scale-location plot should show a horizontal line with equally spread points, which is a good indication of homoscedasticity (constant variance of the residuals). This is not the case here. 

In the residual vs leverage plot there are some observations with high leverage. 

---

### Final Model 

<br /> 

This is the function that would predict the sale price.  

<br /> 

<em> 

<b>Predicted Sale Price</b> = 
  
  29597.605 + 24363.267(NeighborhoodGroupGroupB) + 42587.343(NeighborhoodGroupGroupC) +  -250.497(SinceRemod) + 
  
  37.628(OverallArea) + -17385.937(IsAbnormalSale) + -9549.326(IsReduced) + 46712.205(KitchenQualGroupHigh) + 
  
   7982.469(KitchenQualGroupMedium) + 22853.123(ExcellentFireplace) + 61809.474(ExcellentGarage) + 
  
   118176.450(ExcellentPool) + 32106.49(OverallQualityHigh) + 29.824(MasVnrArea) + 14439.168(CentralAir)
  
</em>

---

### <span style="color:blue"> Kaggle Score</span>

<br /> 

I ran the predictions on the test data and submitted it to Kaggle. 

My score is 0.18037 (root mean squared logarithmic error)

<br /> 


![](Kaggle_score2.jpg)

<br /> 
<br /> 






