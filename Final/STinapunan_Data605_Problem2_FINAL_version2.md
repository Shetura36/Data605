---
title: "Data 605 Final - Problem 2"
author: "S. Tinapunan"
date: "December 14, 2018"
output: 
  html_document: 
    keep_md: yes
---





---

## <span style="color:blue"> Part 1: Descriptive and Inferential Statistics </span>

Provide univariate descriptive statistics and appropriate plots for the training data set.  Provide a scatter plot matrix for at least two of the independent variables and the dependent variable. Derive a correlation matrix for any THREE quantitative variables in the data set.  Test the hypotheses that the correlations between each pairwise set of variables is 0 and provide a 80% confidence interval.  Discuss the meaning of your analysis.  Would you be worried about family wise error? Why or why not?

<br/> 

---

#### Load training data set

Source: https://www.kaggle.com/c/house-prices-advanced-regression-techniques

- No. of observations: 1460
- No. of attributes: 81


```r
training_data <- read.csv(file="train.csv", header=TRUE, sep=",")
```

<br/> 

#### Preview of training data set

<!--html_preserve--><div id="htmlwidget-331fcb566fc0228768c0" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-331fcb566fc0228768c0">{"x":{"filter":"none","data":[["1","2","3","4","5","6"],[1,2,3,4,5,6],[60,20,60,70,60,50],["RL","RL","RL","RL","RL","RL"],[65,80,68,60,84,85],[8450,9600,11250,9550,14260,14115],["Pave","Pave","Pave","Pave","Pave","Pave"],[null,null,null,null,null,null],["Reg","Reg","IR1","IR1","IR1","IR1"],["Lvl","Lvl","Lvl","Lvl","Lvl","Lvl"],["AllPub","AllPub","AllPub","AllPub","AllPub","AllPub"],["Inside","FR2","Inside","Corner","FR2","Inside"],["Gtl","Gtl","Gtl","Gtl","Gtl","Gtl"],["CollgCr","Veenker","CollgCr","Crawfor","NoRidge","Mitchel"],["Norm","Feedr","Norm","Norm","Norm","Norm"],["Norm","Norm","Norm","Norm","Norm","Norm"],["1Fam","1Fam","1Fam","1Fam","1Fam","1Fam"],["2Story","1Story","2Story","2Story","2Story","1.5Fin"],[7,6,7,7,8,5],[5,8,5,5,5,5],[2003,1976,2001,1915,2000,1993],[2003,1976,2002,1970,2000,1995],["Gable","Gable","Gable","Gable","Gable","Gable"],["CompShg","CompShg","CompShg","CompShg","CompShg","CompShg"],["VinylSd","MetalSd","VinylSd","Wd Sdng","VinylSd","VinylSd"],["VinylSd","MetalSd","VinylSd","Wd Shng","VinylSd","VinylSd"],["BrkFace","None","BrkFace","None","BrkFace","None"],[196,0,162,0,350,0],["Gd","TA","Gd","TA","Gd","TA"],["TA","TA","TA","TA","TA","TA"],["PConc","CBlock","PConc","BrkTil","PConc","Wood"],["Gd","Gd","Gd","TA","Gd","Gd"],["TA","TA","TA","Gd","TA","TA"],["No","Gd","Mn","No","Av","No"],["GLQ","ALQ","GLQ","ALQ","GLQ","GLQ"],[706,978,486,216,655,732],["Unf","Unf","Unf","Unf","Unf","Unf"],[0,0,0,0,0,0],[150,284,434,540,490,64],[856,1262,920,756,1145,796],["GasA","GasA","GasA","GasA","GasA","GasA"],["Ex","Ex","Ex","Gd","Ex","Ex"],["Y","Y","Y","Y","Y","Y"],["SBrkr","SBrkr","SBrkr","SBrkr","SBrkr","SBrkr"],[856,1262,920,961,1145,796],[854,0,866,756,1053,566],[0,0,0,0,0,0],[1710,1262,1786,1717,2198,1362],[1,0,1,1,1,1],[0,1,0,0,0,0],[2,2,2,1,2,1],[1,0,1,0,1,1],[3,3,3,3,4,1],[1,1,1,1,1,1],["Gd","TA","Gd","Gd","Gd","TA"],[8,6,6,7,9,5],["Typ","Typ","Typ","Typ","Typ","Typ"],[0,1,1,1,1,0],[null,"TA","TA","Gd","TA",null],["Attchd","Attchd","Attchd","Detchd","Attchd","Attchd"],[2003,1976,2001,1998,2000,1993],["RFn","RFn","RFn","Unf","RFn","Unf"],[2,2,2,3,3,2],[548,460,608,642,836,480],["TA","TA","TA","TA","TA","TA"],["TA","TA","TA","TA","TA","TA"],["Y","Y","Y","Y","Y","Y"],[0,298,0,0,192,40],[61,0,42,35,84,30],[0,0,0,272,0,0],[0,0,0,0,0,320],[0,0,0,0,0,0],[0,0,0,0,0,0],[null,null,null,null,null,null],[null,null,null,null,null,"MnPrv"],[null,null,null,null,null,"Shed"],[0,0,0,0,0,700],[2,5,9,2,12,10],[2008,2007,2008,2006,2008,2009],["WD","WD","WD","WD","WD","WD"],["Normal","Normal","Normal","Abnorml","Normal","Normal"],[208500,181500,223500,140000,250000,143000]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>Id<\/th>\n      <th>MSSubClass<\/th>\n      <th>MSZoning<\/th>\n      <th>LotFrontage<\/th>\n      <th>LotArea<\/th>\n      <th>Street<\/th>\n      <th>Alley<\/th>\n      <th>LotShape<\/th>\n      <th>LandContour<\/th>\n      <th>Utilities<\/th>\n      <th>LotConfig<\/th>\n      <th>LandSlope<\/th>\n      <th>Neighborhood<\/th>\n      <th>Condition1<\/th>\n      <th>Condition2<\/th>\n      <th>BldgType<\/th>\n      <th>HouseStyle<\/th>\n      <th>OverallQual<\/th>\n      <th>OverallCond<\/th>\n      <th>YearBuilt<\/th>\n      <th>YearRemodAdd<\/th>\n      <th>RoofStyle<\/th>\n      <th>RoofMatl<\/th>\n      <th>Exterior1st<\/th>\n      <th>Exterior2nd<\/th>\n      <th>MasVnrType<\/th>\n      <th>MasVnrArea<\/th>\n      <th>ExterQual<\/th>\n      <th>ExterCond<\/th>\n      <th>Foundation<\/th>\n      <th>BsmtQual<\/th>\n      <th>BsmtCond<\/th>\n      <th>BsmtExposure<\/th>\n      <th>BsmtFinType1<\/th>\n      <th>BsmtFinSF1<\/th>\n      <th>BsmtFinType2<\/th>\n      <th>BsmtFinSF2<\/th>\n      <th>BsmtUnfSF<\/th>\n      <th>TotalBsmtSF<\/th>\n      <th>Heating<\/th>\n      <th>HeatingQC<\/th>\n      <th>CentralAir<\/th>\n      <th>Electrical<\/th>\n      <th>X1stFlrSF<\/th>\n      <th>X2ndFlrSF<\/th>\n      <th>LowQualFinSF<\/th>\n      <th>GrLivArea<\/th>\n      <th>BsmtFullBath<\/th>\n      <th>BsmtHalfBath<\/th>\n      <th>FullBath<\/th>\n      <th>HalfBath<\/th>\n      <th>BedroomAbvGr<\/th>\n      <th>KitchenAbvGr<\/th>\n      <th>KitchenQual<\/th>\n      <th>TotRmsAbvGrd<\/th>\n      <th>Functional<\/th>\n      <th>Fireplaces<\/th>\n      <th>FireplaceQu<\/th>\n      <th>GarageType<\/th>\n      <th>GarageYrBlt<\/th>\n      <th>GarageFinish<\/th>\n      <th>GarageCars<\/th>\n      <th>GarageArea<\/th>\n      <th>GarageQual<\/th>\n      <th>GarageCond<\/th>\n      <th>PavedDrive<\/th>\n      <th>WoodDeckSF<\/th>\n      <th>OpenPorchSF<\/th>\n      <th>EnclosedPorch<\/th>\n      <th>X3SsnPorch<\/th>\n      <th>ScreenPorch<\/th>\n      <th>PoolArea<\/th>\n      <th>PoolQC<\/th>\n      <th>Fence<\/th>\n      <th>MiscFeature<\/th>\n      <th>MiscVal<\/th>\n      <th>MoSold<\/th>\n      <th>YrSold<\/th>\n      <th>SaleType<\/th>\n      <th>SaleCondition<\/th>\n      <th>SalePrice<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,2,4,5,18,19,20,21,27,35,37,38,39,44,45,46,47,48,49,50,51,52,53,55,57,60,62,63,67,68,69,70,71,72,76,77,78,81]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

---

<br/>

###  <span style="color:blue">Provide univariate descriptive statistics and appropriate plots for the training data set </span>

<br/> 

The descriptive statistics below gives the minimum, 1st quartile, median, 3rd quartile, max, and number of missing data if any. For categorical data, the summary provides the frequency of the first few levels. Please scroll to the right to view all 81 variables in the training data. 

<br/>

<!--html_preserve--><div id="htmlwidget-017e806534823a661b89" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-017e806534823a661b89">{"x":{"filter":"none","data":[["Min.   : 20.0  ","1st Qu.: 20.0  ","Median : 50.0  ","Mean   : 56.9  ","3rd Qu.: 70.0  ","Max.   :190.0  ",null],["C (all):  10  ","FV     :  65  ","RH     :  16  ","RL     :1151  ","RM     : 218  ",null,null],["Min.   : 21.00  ","1st Qu.: 59.00  ","Median : 69.00  ","Mean   : 70.05  ","3rd Qu.: 80.00  ","Max.   :313.00  ","NA's   :259  "],["Min.   :  1300  ","1st Qu.:  7554  ","Median :  9478  ","Mean   : 10517  ","3rd Qu.: 11602  ","Max.   :215245  ",null],["Grvl:   6  ","Pave:1454  ",null,null,null,null,null],["Grvl:  50  ","Pave:  41  ","NA's:1369  ",null,null,null,null],["IR1:484  ","IR2: 41  ","IR3: 10  ","Reg:925  ",null,null,null],["Bnk:  63  ","HLS:  50  ","Low:  36  ","Lvl:1311  ",null,null,null],["AllPub:1459  ","NoSeWa:   1  ",null,null,null,null,null],["Corner : 263  ","CulDSac:  94  ","FR2    :  47  ","FR3    :   4  ","Inside :1052  ",null,null],["Gtl:1382  ","Mod:  65  ","Sev:  13  ",null,null,null,null],["NAmes  :225  ","CollgCr:150  ","OldTown:113  ","Edwards:100  ","Somerst: 86  ","Gilbert: 79  ","(Other):707  "],["Norm   :1260  ","Feedr  :  81  ","Artery :  48  ","RRAn   :  26  ","PosN   :  19  ","RRAe   :  11  ","(Other):  15  "],["Norm   :1445  ","Feedr  :   6  ","Artery :   2  ","PosN   :   2  ","RRNn   :   2  ","PosA   :   1  ","(Other):   2  "],["1Fam  :1220  ","2fmCon:  31  ","Duplex:  52  ","Twnhs :  43  ","TwnhsE: 114  ",null,null],["1Story :726  ","2Story :445  ","1.5Fin :154  ","SLvl   : 65  ","SFoyer : 37  ","1.5Unf : 14  ","(Other): 19  "],["Min.   : 1.000  ","1st Qu.: 5.000  ","Median : 6.000  ","Mean   : 6.099  ","3rd Qu.: 7.000  ","Max.   :10.000  ",null],["Min.   :1.000  ","1st Qu.:5.000  ","Median :5.000  ","Mean   :5.575  ","3rd Qu.:6.000  ","Max.   :9.000  ",null],["Min.   :1872  ","1st Qu.:1954  ","Median :1973  ","Mean   :1971  ","3rd Qu.:2000  ","Max.   :2010  ",null],["Min.   :1950  ","1st Qu.:1967  ","Median :1994  ","Mean   :1985  ","3rd Qu.:2004  ","Max.   :2010  ",null],["Flat   :  13  ","Gable  :1141  ","Gambrel:  11  ","Hip    : 286  ","Mansard:   7  ","Shed   :   2  ",null],["CompShg:1434  ","Tar&amp;Grv:  11  ","WdShngl:   6  ","WdShake:   5  ","ClyTile:   1  ","Membran:   1  ","(Other):   2  "],["VinylSd:515  ","HdBoard:222  ","MetalSd:220  ","Wd Sdng:206  ","Plywood:108  ","CemntBd: 61  ","(Other):128  "],["VinylSd:504  ","MetalSd:214  ","HdBoard:207  ","Wd Sdng:197  ","Plywood:142  ","CmentBd: 60  ","(Other):136  "],["BrkCmn : 15  ","BrkFace:445  ","None   :864  ","Stone  :128  ","NA's   :  8  ",null,null],["Min.   :   0.0  ","1st Qu.:   0.0  ","Median :   0.0  ","Mean   : 103.7  ","3rd Qu.: 166.0  ","Max.   :1600.0  ","NA's   :8  "],["Ex: 52  ","Fa: 14  ","Gd:488  ","TA:906  ",null,null,null],["Ex:   3  ","Fa:  28  ","Gd: 146  ","Po:   1  ","TA:1282  ",null,null],["BrkTil:146  ","CBlock:634  ","PConc :647  ","Slab  : 24  ","Stone :  6  ","Wood  :  3  ",null],["Ex  :121  ","Fa  : 35  ","Gd  :618  ","TA  :649  ","NA's: 37  ",null,null],["Fa  :  45  ","Gd  :  65  ","Po  :   2  ","TA  :1311  ","NA's:  37  ",null,null],["Av  :221  ","Gd  :134  ","Mn  :114  ","No  :953  ","NA's: 38  ",null,null],["ALQ :220  ","BLQ :148  ","GLQ :418  ","LwQ : 74  ","Rec :133  ","Unf :430  ","NA's: 37  "],["Min.   :   0.0  ","1st Qu.:   0.0  ","Median : 383.5  ","Mean   : 443.6  ","3rd Qu.: 712.2  ","Max.   :5644.0  ",null],["ALQ :  19  ","BLQ :  33  ","GLQ :  14  ","LwQ :  46  ","Rec :  54  ","Unf :1256  ","NA's:  38  "],["Min.   :   0.00  ","1st Qu.:   0.00  ","Median :   0.00  ","Mean   :  46.55  ","3rd Qu.:   0.00  ","Max.   :1474.00  ",null],["Min.   :   0.0  ","1st Qu.: 223.0  ","Median : 477.5  ","Mean   : 567.2  ","3rd Qu.: 808.0  ","Max.   :2336.0  ",null],["Min.   :   0.0  ","1st Qu.: 795.8  ","Median : 991.5  ","Mean   :1057.4  ","3rd Qu.:1298.2  ","Max.   :6110.0  ",null],["Floor:   1  ","GasA :1428  ","GasW :  18  ","Grav :   7  ","OthW :   2  ","Wall :   4  ",null],["Ex:741  ","Fa: 49  ","Gd:241  ","Po:  1  ","TA:428  ",null,null],["N:  95  ","Y:1365  ",null,null,null,null,null],["FuseA:  94  ","FuseF:  27  ","FuseP:   3  ","Mix  :   1  ","SBrkr:1334  ","NA's :   1  ",null],["Min.   : 334  ","1st Qu.: 882  ","Median :1087  ","Mean   :1163  ","3rd Qu.:1391  ","Max.   :4692  ",null],["Min.   :   0  ","1st Qu.:   0  ","Median :   0  ","Mean   : 347  ","3rd Qu.: 728  ","Max.   :2065  ",null],["Min.   :  0.000  ","1st Qu.:  0.000  ","Median :  0.000  ","Mean   :  5.845  ","3rd Qu.:  0.000  ","Max.   :572.000  ",null],["Min.   : 334  ","1st Qu.:1130  ","Median :1464  ","Mean   :1515  ","3rd Qu.:1777  ","Max.   :5642  ",null],["Min.   :0.0000  ","1st Qu.:0.0000  ","Median :0.0000  ","Mean   :0.4253  ","3rd Qu.:1.0000  ","Max.   :3.0000  ",null],["Min.   :0.00000  ","1st Qu.:0.00000  ","Median :0.00000  ","Mean   :0.05753  ","3rd Qu.:0.00000  ","Max.   :2.00000  ",null],["Min.   :0.000  ","1st Qu.:1.000  ","Median :2.000  ","Mean   :1.565  ","3rd Qu.:2.000  ","Max.   :3.000  ",null],["Min.   :0.0000  ","1st Qu.:0.0000  ","Median :0.0000  ","Mean   :0.3829  ","3rd Qu.:1.0000  ","Max.   :2.0000  ",null],["Min.   :0.000  ","1st Qu.:2.000  ","Median :3.000  ","Mean   :2.866  ","3rd Qu.:3.000  ","Max.   :8.000  ",null],["Min.   :0.000  ","1st Qu.:1.000  ","Median :1.000  ","Mean   :1.047  ","3rd Qu.:1.000  ","Max.   :3.000  ",null],["Ex:100  ","Fa: 39  ","Gd:586  ","TA:735  ",null,null,null],["Min.   : 2.000  ","1st Qu.: 5.000  ","Median : 6.000  ","Mean   : 6.518  ","3rd Qu.: 7.000  ","Max.   :14.000  ",null],["Maj1:  14  ","Maj2:   5  ","Min1:  31  ","Min2:  34  ","Mod :  15  ","Sev :   1  ","Typ :1360  "],["Min.   :0.000  ","1st Qu.:0.000  ","Median :1.000  ","Mean   :0.613  ","3rd Qu.:1.000  ","Max.   :3.000  ",null],["Ex  : 24  ","Fa  : 33  ","Gd  :380  ","Po  : 20  ","TA  :313  ","NA's:690  ",null],["2Types :  6  ","Attchd :870  ","Basment: 19  ","BuiltIn: 88  ","CarPort:  9  ","Detchd :387  ","NA's   : 81  "],["Min.   :1900  ","1st Qu.:1961  ","Median :1980  ","Mean   :1979  ","3rd Qu.:2002  ","Max.   :2010  ","NA's   :81  "],["Fin :352  ","RFn :422  ","Unf :605  ","NA's: 81  ",null,null,null],["Min.   :0.000  ","1st Qu.:1.000  ","Median :2.000  ","Mean   :1.767  ","3rd Qu.:2.000  ","Max.   :4.000  ",null],["Min.   :   0.0  ","1st Qu.: 334.5  ","Median : 480.0  ","Mean   : 473.0  ","3rd Qu.: 576.0  ","Max.   :1418.0  ",null],["Ex  :   3  ","Fa  :  48  ","Gd  :  14  ","Po  :   3  ","TA  :1311  ","NA's:  81  ",null],["Ex  :   2  ","Fa  :  35  ","Gd  :   9  ","Po  :   7  ","TA  :1326  ","NA's:  81  ",null],["N:  90  ","P:  30  ","Y:1340  ",null,null,null,null],["Min.   :  0.00  ","1st Qu.:  0.00  ","Median :  0.00  ","Mean   : 94.24  ","3rd Qu.:168.00  ","Max.   :857.00  ",null],["Min.   :  0.00  ","1st Qu.:  0.00  ","Median : 25.00  ","Mean   : 46.66  ","3rd Qu.: 68.00  ","Max.   :547.00  ",null],["Min.   :  0.00  ","1st Qu.:  0.00  ","Median :  0.00  ","Mean   : 21.95  ","3rd Qu.:  0.00  ","Max.   :552.00  ",null],["Min.   :  0.00  ","1st Qu.:  0.00  ","Median :  0.00  ","Mean   :  3.41  ","3rd Qu.:  0.00  ","Max.   :508.00  ",null],["Min.   :  0.00  ","1st Qu.:  0.00  ","Median :  0.00  ","Mean   : 15.06  ","3rd Qu.:  0.00  ","Max.   :480.00  ",null],["Min.   :  0.000  ","1st Qu.:  0.000  ","Median :  0.000  ","Mean   :  2.759  ","3rd Qu.:  0.000  ","Max.   :738.000  ",null],["Ex  :   2  ","Fa  :   2  ","Gd  :   3  ","NA's:1453  ",null,null,null],["GdPrv:  59  ","GdWo :  54  ","MnPrv: 157  ","MnWw :  11  ","NA's :1179  ",null,null],["Gar2:   2  ","Othr:   2  ","Shed:  49  ","TenC:   1  ","NA's:1406  ",null,null],["Min.   :    0.00  ","1st Qu.:    0.00  ","Median :    0.00  ","Mean   :   43.49  ","3rd Qu.:    0.00  ","Max.   :15500.00  ",null],["Min.   : 1.000  ","1st Qu.: 5.000  ","Median : 6.000  ","Mean   : 6.322  ","3rd Qu.: 8.000  ","Max.   :12.000  ",null],["Min.   :2006  ","1st Qu.:2007  ","Median :2008  ","Mean   :2008  ","3rd Qu.:2009  ","Max.   :2010  ",null],["WD     :1267  ","New    : 122  ","COD    :  43  ","ConLD  :   9  ","ConLI  :   5  ","ConLw  :   5  ","(Other):   9  "],["Abnorml: 101  ","AdjLand:   4  ","Alloca :  12  ","Family :  20  ","Normal :1198  ","Partial: 125  ",null],["Min.   : 34900  ","1st Qu.:129975  ","Median :163000  ","Mean   :180921  ","3rd Qu.:214000  ","Max.   :755000  ",null]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th>  MSSubClass<\/th>\n      <th>   MSZoning<\/th>\n      <th> LotFrontage<\/th>\n      <th>   LotArea<\/th>\n      <th> Street<\/th>\n      <th> Alley<\/th>\n      <th>LotShape<\/th>\n      <th>LandContour<\/th>\n      <th> Utilities<\/th>\n      <th>  LotConfig<\/th>\n      <th>LandSlope<\/th>\n      <th> Neighborhood<\/th>\n      <th>  Condition1<\/th>\n      <th>  Condition2<\/th>\n      <th>  BldgType<\/th>\n      <th>  HouseStyle<\/th>\n      <th> OverallQual<\/th>\n      <th> OverallCond<\/th>\n      <th>  YearBuilt<\/th>\n      <th> YearRemodAdd<\/th>\n      <th>  RoofStyle<\/th>\n      <th>   RoofMatl<\/th>\n      <th> Exterior1st<\/th>\n      <th> Exterior2nd<\/th>\n      <th>  MasVnrType<\/th>\n      <th>  MasVnrArea<\/th>\n      <th>ExterQual<\/th>\n      <th>ExterCond<\/th>\n      <th> Foundation<\/th>\n      <th>BsmtQual<\/th>\n      <th>BsmtCond<\/th>\n      <th>BsmtExposure<\/th>\n      <th>BsmtFinType1<\/th>\n      <th>  BsmtFinSF1<\/th>\n      <th>BsmtFinType2<\/th>\n      <th>  BsmtFinSF2<\/th>\n      <th>  BsmtUnfSF<\/th>\n      <th> TotalBsmtSF<\/th>\n      <th> Heating<\/th>\n      <th>HeatingQC<\/th>\n      <th>CentralAir<\/th>\n      <th>Electrical<\/th>\n      <th>  X1stFlrSF<\/th>\n      <th>  X2ndFlrSF<\/th>\n      <th> LowQualFinSF<\/th>\n      <th>  GrLivArea<\/th>\n      <th> BsmtFullBath<\/th>\n      <th> BsmtHalfBath<\/th>\n      <th>   FullBath<\/th>\n      <th>   HalfBath<\/th>\n      <th> BedroomAbvGr<\/th>\n      <th> KitchenAbvGr<\/th>\n      <th>KitchenQual<\/th>\n      <th> TotRmsAbvGrd<\/th>\n      <th>Functional<\/th>\n      <th>  Fireplaces<\/th>\n      <th>FireplaceQu<\/th>\n      <th>  GarageType<\/th>\n      <th> GarageYrBlt<\/th>\n      <th>GarageFinish<\/th>\n      <th>  GarageCars<\/th>\n      <th>  GarageArea<\/th>\n      <th>GarageQual<\/th>\n      <th>GarageCond<\/th>\n      <th>PavedDrive<\/th>\n      <th>  WoodDeckSF<\/th>\n      <th> OpenPorchSF<\/th>\n      <th>EnclosedPorch<\/th>\n      <th>  X3SsnPorch<\/th>\n      <th> ScreenPorch<\/th>\n      <th>   PoolArea<\/th>\n      <th> PoolQC<\/th>\n      <th>  Fence<\/th>\n      <th>MiscFeature<\/th>\n      <th>   MiscVal<\/th>\n      <th>    MoSold<\/th>\n      <th>    YrSold<\/th>\n      <th>   SaleType<\/th>\n      <th>SaleCondition<\/th>\n      <th>  SalePrice<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

The descriptive statistics below comes from the package *psych*, and provides information such as count of values that are not missing, standard deviation, interquartile range, and standard error. By default, categorical variables are converted to numeric. These are marked with `*`. 

Reference: https://www.rdocumentation.org/packages/psych/versions/1.8.10/topics/describe

<br/>

<!--html_preserve--><div id="htmlwidget-e5706d20373ed153994b" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-e5706d20373ed153994b">{"x":{"filter":"none","data":[["Id","MSSubClass","MSZoning*","LotFrontage","LotArea","Street*","Alley*","LotShape*","LandContour*","Utilities*","LotConfig*","LandSlope*","Neighborhood*","Condition1*","Condition2*","BldgType*","HouseStyle*","OverallQual","OverallCond","YearBuilt","YearRemodAdd","RoofStyle*","RoofMatl*","Exterior1st*","Exterior2nd*","MasVnrType*","MasVnrArea","ExterQual*","ExterCond*","Foundation*","BsmtQual*","BsmtCond*","BsmtExposure*","BsmtFinType1*","BsmtFinSF1","BsmtFinType2*","BsmtFinSF2","BsmtUnfSF","TotalBsmtSF","Heating*","HeatingQC*","CentralAir*","Electrical*","X1stFlrSF","X2ndFlrSF","LowQualFinSF","GrLivArea","BsmtFullBath","BsmtHalfBath","FullBath","HalfBath","BedroomAbvGr","KitchenAbvGr","KitchenQual*","TotRmsAbvGrd","Functional*","Fireplaces","FireplaceQu*","GarageType*","GarageYrBlt","GarageFinish*","GarageCars","GarageArea","GarageQual*","GarageCond*","PavedDrive*","WoodDeckSF","OpenPorchSF","EnclosedPorch","X3SsnPorch","ScreenPorch","PoolArea","PoolQC*","Fence*","MiscFeature*","MiscVal","MoSold","YrSold","SaleType*","SaleCondition*","SalePrice"],[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81],[1460,1460,1460,1201,1460,1460,91,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1452,1452,1460,1460,1460,1423,1423,1422,1423,1460,1422,1460,1460,1460,1460,1460,1460,1459,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,1460,770,1379,1379,1379,1460,1460,1379,1379,1460,1460,1460,1460,1460,1460,1460,7,281,54,1460,1460,1460,1460,1460,1460],[730.5,56.8972602739726,4.02876712328767,70.0499583680267,10516.8280821918,1.9958904109589,1.45054945054945,2.94246575342466,3.77739726027397,1.00068493150685,4.01917808219178,1.06232876712329,13.15,3.03150684931507,3.00821917808219,1.49315068493151,4.03835616438356,6.09931506849315,5.57534246575342,1971.26780821918,1984.86575342466,2.41027397260274,2.07534246575342,10.6246575342466,11.3397260273973,2.76101928374656,103.685261707989,3.53972602739726,4.73356164383562,2.39657534246575,3.26141953619115,3.81236823612087,3.26511954992968,3.73225579761068,443.639726027397,5.70815752461322,46.5493150684932,567.240410958904,1057.42945205479,2.03630136986301,2.53835616438356,1.93493150684932,4.68197395476354,1162.62671232877,346.992465753425,5.84452054794521,1515.46369863014,0.425342465753425,0.0575342465753425,1.56506849315068,0.382876712328767,2.86643835616438,1.04657534246575,3.33972602739726,6.51780821917808,6.74931506849315,0.613013698630137,3.73376623376623,3.27918781725888,1978.50616388687,2.18346627991298,1.76712328767123,472.980136986301,4.86439448875997,4.89992748368383,2.85616438356164,94.2445205479452,46.6602739726027,21.9541095890411,3.40958904109589,15.0609589041096,2.75890410958904,2.14285714285714,2.4270462633452,2.90740740740741,43.4890410958904,6.32191780821918,2007.81575342466,8.50958904109589,4.77054794520548,180921.195890411],[421.610009368848,42.3005709938104,0.632017441056658,24.2847517744832,9981.26493237915,0.0639961362875529,0.500305157184343,1.40915617527333,0.707665901269637,0.0261711961295107,1.62263441221627,0.276232464349089,5.89351184243101,0.868515109539234,0.259039944499839,1.19827712362784,1.91130471476323,1.38299654674159,1.11279933671273,30.2029040425253,20.6454068077094,0.834997790055461,0.599126808506423,3.19765939167586,3.54057029773184,0.615710742510224,181.066206587217,0.6939945515402,0.731807211890503,0.722393628357979,0.867750025796176,0.658655622144433,1.14748138655744,1.82593240711077,456.098090840928,0.936358170791167,161.319272806542,441.866955292434,438.705324459471,0.295123755593015,1.73952402532346,0.246731190635218,1.05162879579713,386.587738041074,436.528435886257,48.6230814335202,525.480383423203,0.518910606089806,0.238752646279212,0.550915801295432,0.502885381092891,0.815778044144228,0.220338198384031,0.830161338609947,1.62539329058405,0.979659238803503,0.64466638631223,1.13257826279472,1.78558830916787,24.6897247685902,0.812896339050744,0.747315010111109,213.80484145338,0.610527960034688,0.522491236270952,0.496591894445001,125.338794351724,66.2560276766497,61.1191486017286,29.3173305567819,55.7574152818742,40.1773069445302,0.899735410842437,0.863453300082574,0.445883414769754,496.123024457944,2.70362620835951,1.32809512055211,1.56093190066352,1.10085441352765,79442.5028828866],[1,20,1,21,1300,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1872,1950,1,1,1,1,1,0,1,1,1,1,1,1,1,0,1,0,0,0,1,1,1,1,334,0,0,334,0,0,0,0,0,0,1,2,1,0,1,1,1900,1,0,0,1,1,1,0,0,0,0,0,0,1,1,1,0,1,2006,1,1,34900],[1460,190,5,313,215245,2,2,4,4,2,5,3,25,9,8,5,8,10,9,2010,2010,6,8,15,16,4,1600,4,5,6,4,4,4,6,5644,6,1474,2336,6110,6,5,2,5,4692,2065,572,5642,3,2,3,2,8,3,4,14,7,3,5,6,2010,3,4,1418,5,5,3,857,547,552,508,480,738,3,4,4,15500,12,2010,9,6,755000],[1459,170,4,292,213945,1,1,3,3,1,4,2,24,8,7,4,7,9,8,138,60,5,7,14,15,3,1600,3,4,5,3,3,3,5,5644,5,1474,2336,6110,5,4,1,4,4358,2065,572,5308,3,2,3,2,8,3,3,12,6,3,4,5,110,2,4,1418,4,4,2,857,547,552,508,480,738,2,3,3,15500,11,4,8,5,720100],[11.034038245357,1.1070565398693,0.0165406524071653,0.700748480979844,261.221642165902,0.00167485543431244,0.0524462310010123,0.0368793026401893,0.0185204630962946,0.000684931506849315,0.0424662834486054,0.00722933400181807,0.154240254319856,0.0227300792731948,0.00677938519288284,0.0313603456199701,0.050021130553327,0.0361946738712102,0.0291232896938983,0.79044612537772,0.540314990738098,0.0218528909312495,0.0156798652118694,0.0836865710949207,0.09266095967226,0.0161582164968737,4.75175559610336,0.0181626675211704,0.0191522700713767,0.0189059053304655,0.0230034081508818,0.0174604709382287,0.0304295725177279,0.0484041108246039,11.9366325896933,0.0248308854456792,4.22191832809004,11.564186750108,11.4814430894894,0.00772374169010258,0.0455254244387362,0.00645725038138197,0.0275318137886571,10.1174635135369,11.4244713116878,1.27252420061783,13.7524501767791,0.0135805112456596,0.00624844233221294,0.0144181254865493,0.0131611119392458,0.0213498871914472,0.0057665142047315,0.0217263152118981,0.0425384865954659,0.0256388540788136,0.0168716904342803,0.0408152874554568,0.0480838463498372,0.664865986239527,0.0218903665893046,0.0195581277001451,5.59552843911536,0.0164408181168415,0.014070090062192,0.0129964038658454,3.28026616961538,1.73399949508789,1.59956122532455,0.767269607995235,1.45923825101651,1.05148818000085,0.340068020406802,0.0515093054310681,0.0606770472753139,12.9841329774549,0.0707571317598621,0.0347578378786154,0.0408514549170748,0.0288106767664695,2079.10532396724]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>vars<\/th>\n      <th>n<\/th>\n      <th>mean<\/th>\n      <th>sd<\/th>\n      <th>min<\/th>\n      <th>max<\/th>\n      <th>range<\/th>\n      <th>se<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,2,3,4,5,6,7,8]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

<br/>

#### Visualize dependent varirable Sale Price

<br/>


![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-6-1.png)<!-- -->




```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   34900  129975  163000  180921  214000  755000
```


As you can see, the distribution is skewed to the right with some prices that are outliers towards the tail. The minimum sale price is 34,900 USD and the maximum sale price is 755,00 USD. The median sale price is 163,000. 


<br/>

#### Visualize distribution of some of the explanatory variables in training set

<br/>

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-8-1.png)<!-- -->![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-8-2.png)<!-- -->![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-8-3.png)<!-- -->

---

<br/>

### <span style="color:blue">Provide a scatterplot matrix for at least two of the independent variables and the dependent variable </span>

<br/>

- <b>Dependent variable</b>: Sale Price
- <b>Selected independent continuous variables</b>: Garage Area, Above Ground Living Area, and Lot Frontage 

<br/>


![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-9-1.png)<!-- -->


<br/>


![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

<br/>

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

The *lot frontage* measures the linear feet of street connected to the property. 

---

<br/>

### <span style="color:blue">Derive a correlation matrix for any THREE quantitative variables in the dataset </span>

<br/>


<b> Data for Correlation </b>

The `corr_data` data frame only includes complete cases. 

Each of the variable are continuous. These variables measure area (in square feet) or distance (in feet). 



```r
corr_data <- data.frame(training_data$GarageArea, training_data$GrLivArea, training_data$LotFrontage)
corr_data <- corr_data[complete.cases(corr_data), ]
colnames(corr_data) <- c("GarageArea", "GrLivArea", "LotFrontage")
```

<br/> 

### Assumptions of Pearson Correlation

The Pearson correlation assumes that each of the variables are continuous, each observation is complete (no missing data), there are no outliers in each variable, and relationship between variables is linear and homoscedastic. Missing data were removed from `corr_data`. Below investigates the other assumptions. 

<br/>

#### Linear Relationship: Scatterplot of the Variables 

The plots below show a linear relationship. I do not observe any noticeable curved patterns. 

<br/> 



<b> Garage Area and Above Ground Living Area </b>

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

<b> Garage Area and Lot Frontage </b>

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-15-1.png)<!-- -->


<b> Above Ground Living Area and Lot Frontage </b>

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

<br/>

#### Normality 

One of the assumptions of the Pearson correlation is that the data has a normal distribution. 

The Shapiro-wilk normality test for *Garage Area* has a p-value much less than 0.05, which suggests that the distribution of this data is not normal. If the null hypothesis that the distribution is normal were true, then the probability of finding this observed data is 2.195e-12 (reject H0). 


```r
shapiro.test(corr_data$GarageArea)
```

```
## 
## 	Shapiro-Wilk normality test
## 
## data:  corr_data$GarageArea
## W = 0.97847, p-value = 2.195e-12
```

The Shapiro-wilk normality test for *Above Ground Living Area* has a p-value that is much less than 0.05, which suggests that the distribution of this data is not normal. If the null hypothesis that the distribution is normal were true, then the probability of finding this observed data is 2.2e-16 (reject H0). 


```r
shapiro.test(corr_data$GrLivArea)
```

```
## 
## 	Shapiro-Wilk normality test
## 
## data:  corr_data$GrLivArea
## W = 0.91971, p-value < 2.2e-16
```

The Shapiro-wilk normality test for *Log Frontage* has a p-value that is much less than 0.05, which suggests that the distribution of this data is not normal. If the null hypothesis that the distribution is normal were true, then the probability of finding this observed data is 2.2e-16 (reject H0). 



```r
shapiro.test(corr_data$LotFrontage)
```

```
## 
## 	Shapiro-Wilk normality test
## 
## data:  corr_data$LotFrontage
## W = 0.8804, p-value < 2.2e-16
```

Below is a visual representation of the q-q plots of each of the variable. 


```r
q1 <- ggqqplot(corr_data$GarageArea, ylab = "Garage Area")
q2 <- ggqqplot(corr_data$GrLivArea, ylab = "Above Ground Area")
q3 <- ggqqplot(corr_data$LotFrontage, ylab = "Lot Frontage")
grid.arrange(q1, q2, q3, nrow=2, ncol=2)
```

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-20-1.png)<!-- -->

<br/>

#### Linearity and Homoscedasticity

<br/>

The Pearson correlation assumes linear relationship and homoscedasticity (homogeneity of variance). 

A *Residual vs Fitted* plot that shows a horizontal red line that is close to zero suggests that the relationship is linear. 

A *Scale-location* plot that shows a horizontal red line with points approximately equally spread out suggests a constant variance in the residual errors (homoscedasticity).

Overall I think that there is a linear relationship between the variables; however, there are some outliers that is causing the line in the *Residual vs Fitted* plots to deviate a lot more. 

Overall, I think that the variance in the residual errors is somewhat constant. The residuals appear to be equally spread out.

<br/>

<b> Garage Area and Above Ground Living Area </b>


![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-21-1.png)<!-- -->


<b> Garage Area and Lot Frontage </b>


![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-22-1.png)<!-- -->

<b> Above Ground Living Area and Lot Frontage </b>


![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-23-1.png)<!-- -->

Reference: http://www.sthda.com/english/articles/39-regression-model-diagnostics/161-linear-regression-assumptions-and-diagnostics-in-r-essentials

<br/>

#### Correlation Matrix

The Pearson correlation is calculated by the  *cor* function calculates the correlation of each variable to one another. The assumptions of the Pearson correlations were investigated above. 



```r
cor <- cor(corr_data, method = "pearson", use = "complete.obs") 
kable(cor)
```

               GarageArea   GrLivArea   LotFrontage
------------  -----------  ----------  ------------
GarageArea      1.0000000   0.4737098     0.3449967
GrLivArea       0.4737098   1.0000000     0.4027974
LotFrontage     0.3449967   0.4027974     1.0000000


<br/>

### <span style="color:blue">Test the hypotheses that the correlations between each pairwise set of variables is 0 </span>

<br/>

- H0: The correlation is zero. 
- H1: The correlation is not zero. 
- Significance level is 0.05. 

The *cor.test* function of the *ggpubr* package is used to perform the hypothesis tests. 

<br/>


```r
corr_GarageArea_GrLivArea <- cor.test(corr_data$GarageArea, corr_data$GrLivArea, method = "pearson")
corr_Garagearea_LotFrontage <- cor.test(corr_data$GarageArea, corr_data$LotFrontage , method = "pearson")
corr_GrLivArea_LotFrontage <- cor.test(corr_data$GrLivArea, corr_data$LotFrontage , method = "pearson")
```

<br/>

<b>Results for *Garage Area* and *Above Ground Living Area* </b>

The correlation coefficient is 0.4737098, which is found to be significant with p-value (< 2.2e-16) that is much less than the significance level of 0.05. If the null hypothesis were true (correlation is zero), the probability of this observed data is < 2.2e-16. This is evidence to reject the null hypothesis and accept the alternative that the correlation is not zero. 



```r
corr_GarageArea_GrLivArea
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  corr_data$GarageArea and corr_data$GrLivArea
## t = 18.625, df = 1199, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.4286292 0.5164374
## sample estimates:
##       cor 
## 0.4737098
```

<br/>

<b> Results for *Garage Area* and *Lot Frontage* </b>

The correlation coefficient is 0.3449967, which is found to be significant with p-value (< 2.2e-16) that is much less than the significance level of 0.05. If the null hypothesis were true (correlation is zero), the probability of this observed data is < 2.2e-16. This is evidence to reject the null hypothesis and accept the alternative that the correlation is not zero. 



```r
corr_Garagearea_LotFrontage
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  corr_data$GarageArea and corr_data$LotFrontage
## t = 12.727, df = 1199, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.2941715 0.3938762
## sample estimates:
##       cor 
## 0.3449967
```

<br/>

<b> Results for *Above Ground Living Area* and *Lot Frontage* </b>

The correlation coefficient is 0.4491302, which is found to be significant with p-value (< 2.2e-16) that is much less than the significance level of 0.05. If the null hypothesis were true (correlation is zero), the probability of this observed data is < 2.2e-16. This is evidence to reject the null hypothesis and accept the alternative that the correlation is not zero. 


```r
corr_GrLivArea_LotFrontage
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  corr_data$GrLivArea and corr_data$LotFrontage
## t = 15.238, df = 1199, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.3543041 0.4491302
## sample estimates:
##       cor 
## 0.4027974
```

<br/>

### <span style="color:blue"> Provide a 80% confidence interval </span>

<br/>

The *CIr* function of the *Psychometric* package is used to calculate the 80% confidence interval. 



```r
corr_data_n <- nrow(corr_data)
```

<br/>

#### 80% confidence interval of the correlation between *GarageArea* and *GrLivArea*. 

As you can see *zero* does not fall within the range [0.4444933, 0.5019195]. 


```r
CIr(r=corr_GarageArea_GrLivArea$estimate , n = corr_data_n, level = .80)
```

```
## [1] 0.4444933 0.5019195
```

<br/>

#### 80% confidence interval of the correlation between *GarageArea* and *LotFrontage*. 

As you can see *zero* does not fall within the range [0.3119708, 0.3771899]. 


```r
CIr(r=corr_Garagearea_LotFrontage$estimate , n = corr_data_n, level = .80)
```

```
## [1] 0.3119708 0.3771899
```

<br/>

#### 80% confidence interval of the correlation between *GrLivArea* and *LotFrontage*. 

As you can see *zero* does not fall within the range [0.3713236, 0.4333466]


```r
CIr(r=corr_GrLivArea_LotFrontage$estimate , n = corr_data_n, level = .80)
```

```
## [1] 0.3713236 0.4333466
```

<br/>

### <span style="color:blue">Discuss the meaning of your analysis. Would you be worried about familywise error? Why or why not?</span>

<br/>

The variables have positive correlation values that range from 0.34 to 0.47 (weak to moderate), and the correlation coefficients were found to be significant. Garage Area and Above Ground Living Area has the strongest correlation at 0.47. Garage Area and Lot Frontage has the weakest correlation at 0.34. 

Houses that have big garages tend to have big above ground living spaces and longer street distance connected to their property. And houses that have big above ground living space tend to have longer distance of street connected to their property.

<br/>


               GarageArea   GrLivArea   LotFrontage
------------  -----------  ----------  ------------
GarageArea      1.0000000   0.4737098     0.3449967
GrLivArea       0.4737098   1.0000000     0.4027974
LotFrontage     0.3449967   0.4027974     1.0000000

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-34-1.png)<!-- -->

<br/>

#### Considering Familywise Error Rate

<br/>

The familywise error rate needs to be considered when multiple statistical analyses are conducted on *the same* data. For this pairwise correlation of 3 variables, a total of 3 different comparisons were made. The significance level was set to 0.05 per analysis, which means that there is a 5% chance of committing a Type I error. Type I error happens when the null hypothesis is rejected when in fact it is true in the population. This 5% Type I error rate is only for a single analysis. When multiple analyses are made, we need to consider the familywise error rate. This is the overall Type I error rate of the multiple comparisons, which is known to be larger than the per analysis error rate.

The formula for calculating the familywise error rate is *1 - (1 - alpha)^k* , where alpha is the significance level and k is the number of comparisons. 

The familywise error rate in this case is 0.142625. This means the probability of committing at least one Type I error is 14.26%. 


```r
k <- 3
alpha <- .05
1 - (1-alpha)^k
```

```
## [1] 0.142625
```

To control the familywise error rate, a common technique is to perform a *Bonferroni* correction. This simple approach adjusts alpha by dividing it by the number of comparisons. In this case, the adjusted alpha would be .05/3 or around 0.017. The p-values of the results would then need to be less than 0.017 in order for the null hypothesis to be rejected. This adjustment controls for the overall Type I error rate of the family of analyses to 0.05.

Below are the p-values of the analyses, and all are less than 0.017. This is evidence to reject the null hypothesis that the correlation is zero. 


Comparisons             P-value                Compare to adjusted P-value 
----------------------  ---------------------  ----------------------------
GarageArea-GrLivArea    3.33606210043948e-68   less than 0.017             
GarageArea-GrLivArea    6.73480729281281e-35   less than 0.017             
GrLivArea-LotFrontage   4.61242260931362e-48   less than 0.017             

Since we are doing multiple analyses on the same data, I would consider controlling for the familywise error rate. 


Reference: https://www.youtube.com/watch?v=rMuNniCTsOw

<br/> 

---

## <span style="color:blue">Part 2: Linear Algebra and Correlation<span> 

Invert your 3 x 3 correlation matrix from above. (This is known as the precision matrix and contains variance inflation factors on the diagonal.) Multiply the correlation matrix by the precision matrix, and then multiply the precision matrix by the correlation matrix. Conduct LU decomposition on the matrix.

---

<br/> 


<b>`cor_matrix` is the 3 X 3 matrix of the correlation coefficients</b>


```r
cor_matrix <- data.matrix(cor)
rownames(cor_matrix) <- c()
colnames(cor_matrix) <- c()
cor_matrix
```

```
##           [,1]      [,2]      [,3]
## [1,] 1.0000000 0.4737098 0.3449967
## [2,] 0.4737098 1.0000000 0.4027974
## [3,] 0.3449967 0.4027974 1.0000000
```


<br /> 

#### <span style="color:blue">Precision Matrix: invert your 3 x 3 correlation matrix</span>

<br /> 

The determinant of the correlation matrix is not zero. This means that this matrix has an inverse. 


```r
det(cor_matrix)
```

```
## [1] 0.6259876
```


The *inv* function from the *matlib* package is used to generate the inverse of the correlation matrix. 


```r
precision_matrix <- inv(cor_matrix)
precision_matrix
```

```
##            [,1]       [,2]       [,3]
## [1,]  1.3382921 -0.5347486 -0.2463111
## [2,] -0.5347486  1.4073399 -0.3823863
## [3,] -0.2463111 -0.3823863  1.2390007
```


<br /> 

####<span style="color:blue"> Multiply the correlation matrix by the precision matrix </span>

<br /> 

The operator `%*%` performs the matrix multiplication. 


```r
result1 <- cor_matrix %*% precision_matrix
result1
```

```
##               [,1]          [,2]         [,3]
## [1,]  1.000000e+00 -4.854738e-09 5.875876e-09
## [2,] -2.944996e-09  1.000000e+00 6.229884e-09
## [3,]  1.509716e-09  5.486613e-10 1.000000e+00
```

We expect to get the identity matrix; however, at first glance it does not look like it is the identity matrix. The off diagonal values are very tiny. We can use the *zapsmall* function to round very small values to zero. 


```r
result1 <- zapsmall(result1)
result1
```

```
##      [,1] [,2] [,3]
## [1,]    1    0    0
## [2,]    0    1    0
## [3,]    0    0    1
```


<br /> 

#### <span style="color:blue">Multiply the precision matrix by the correlation matrix</span> 

<br /> 

As expected, multiplying the precision matrix by the correlation matrix also results in the identity matrix. 


```r
result2 <- zapsmall(precision_matrix %*% cor_matrix)
result2
```

```
##      [,1] [,2] [,3]
## [1,]    1    0    0
## [2,]    0    1    0
## [3,]    0    0    1
```

<br /> 

#### <span style="color:blue">Conduct LU decomposition on the matrix</span> 

<br /> 

The function *lu.decomposition* is used from the *matrixcalc* package. 



```r
lu_decomp <- lu.decomposition(cor_matrix)
```

<br /> 

<b> The lower triangular matrix L </b> 


```r
L <- lu_decomp$L
L
```

```
##           [,1]      [,2] [,3]
## [1,] 1.0000000 0.0000000    0
## [2,] 0.4737098 1.0000000    0
## [3,] 0.3449967 0.3086248    1
```

<br /> 

<b>The upper triangular matrix U</b> 


```r
U <- lu_decomp$U
U
```

```
##      [,1]      [,2]      [,3]
## [1,]    1 0.4737098 0.3449967
## [2,]    0 0.7755991 0.2393691
## [3,]    0 0.0000000 0.8071020
```

<br /> 

Multiplying L and U should result in the correlation matrix. 


```r
L %*% U
```

```
##           [,1]      [,2]      [,3]
## [1,] 1.0000000 0.4737098 0.3449967
## [2,] 0.4737098 1.0000000 0.4027974
## [3,] 0.3449967 0.4027974 1.0000000
```

<br /> 

As you can see, LU is equivalent to the `cor_matrix`. 


```r
cor_matrix
```

```
##           [,1]      [,2]      [,3]
## [1,] 1.0000000 0.4737098 0.3449967
## [2,] 0.4737098 1.0000000 0.4027974
## [3,] 0.3449967 0.4027974 1.0000000
```


<br /> 

References: https://cran.r-project.org/web/packages/matlib/vignettes/inv-ex1.html, https://www.youtube.com/watch?v=UlWcofkUDDU&t=350s 

<br /> 


---

## <span style="color:blue">Part 3: Calculus-Based Probability & Statistics</span>

Many times, it makes sense to fit a closed form distribution to data.  Select a variable in the Kaggle.com training data set that is skewed to the right, shift it so that the minimum value is absolutely above zero if necessary.  Then load the MASS package and run fitdistr to fit an exponential probability density function.  (See  https://stat.ethz.ch/R-manual/R-devel/library/MASS/html/fitdistr.html ).  Find the optimal value of  for this distribution, and then take 1000 samples from this exponential distribution using this value (e.g., rexp(1000, )).  Plot a histogram and compare it with a histogram of your original variable.   Using the exponential pdf, find the 5th and 95th percentiles using the cumulative distribution function (CDF).   Also generate a 95% confidence interval from the empirical data, assuming normality.  Finally, provide the empirical 5th percentile and 95th percentile of the data. Discuss.

---

<br /> 

#### <span style="color:blue">Select a variable in the training dataset that is skewed to the right, shift it so that the minimum value is absolutely above zero if necessary.</span> 

<br /> 

I selected the variable *MasVnrArea*.

The *MasVnArea* is the masonry veneer area measured in square feet. 
 
 

```r
fit_data <- training_data$MasVnrArea
fit_data <- fit_data[complete.cases(fit_data)]
```

<br /> 

As you can see, the distribution is skewed to the right. 


```r
hist(fit_data)
```

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-49-1.png)<!-- -->


<br /> 

As you can see, we have values that are zeroes. This would represent houses that do not have masonry veneers. The total number of observations is 1452.


```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##     0.0     0.0     0.0   103.7   166.0  1600.0
```

```
##    vars    n   mean     sd min  max range   se
## X1    1 1452 103.69 181.07   0 1600  1600 4.75
```

Out of the 1452 houses, there are 861 that have no masonry veneers (area is zero). 


```r
length(fit_data[fit_data == 0])
```

```
## [1] 861
```

Because the data measures area, adding a value of .01 should be negligible and would get rid of the zero values. A property with a masonry veneer area of .01 square feet would mean this property does not really have any masonry veneer. 


```r
fit_data <- fit_data + .01
```

Below is the updated histogram and summary after the adjustment.  

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-53-1.png)<!-- -->

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    0.01    0.01    0.01  103.70  166.01 1600.01
```

```
##    vars    n  mean     sd  min     max range   se
## X1    1 1452 103.7 181.07 0.01 1600.01  1600 4.75
```

<br /> 


####<span style="color:blue">Load the MASS package and run fitdistr to fit an exponential probability density function.</span> 


```r
library(MASS)
fit <- fitdistr(fit_data, densfun="exponential")
```

<br /> 

####<span style="color:blue">Find the optimal value for this distribution, and then take 1000 samples from this exponential distribution using this value (e.g., `rexp(1000,)`).  Plot a histogram and compare it with a histogram of your original variable.</span> 


<br /> 

<b>Optimal value for the fitted distribution</b> 


```r
fit$estimate
```

```
##        rate 
## 0.009643642
```

<br /> 

<b>Generate exponential distribution with the same rate</b> 


```r
exp_dist <- rexp(length(fit_data), rate = fit$estimate) 
```

<br /> 

<b> Histogram of fitted data </b> 

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-57-1.png)<!-- -->

<br /> 

<b> Histogram of exponentially distributed data with same rate as fitted data </b> 

![](STinapunan_Data605_Problem2_FINAL_version2_files/figure-html/unnamed-chunk-58-1.png)<!-- -->

The histogram of `fit_data` and `exp_dist` have similar general shape; however, the first bin of `fit_data` has a frequency that is about double the frequency of `exp_data`. Both have the same count, but the distribution of the frequency is not similar. 

<br /> 

#### <span style="color:blue">Using the exponential pdf, find the 5th and 95th percentiles using the cumulative distribution function (CDF).</span> 

<br /> 


```r
qexp(.05, rate=fit$estimate)
```

```
## [1] 5.318872
```

```r
qexp(.95, rate=fit$estimate)
```

```
## [1] 310.6432
```

<br /> 

#### <span style="color:blue"> Generate a 95% confidence interval from the empirical data, assuming normality.</span> 

<br /> 

This is a function that calculates the confidence interval assuming normality. 


```r
norm.interval = function(data, variance = var(data), conf.level = 0.95) 
{
      z = qnorm((1 - conf.level)/2, lower.tail = FALSE)
      xbar = mean(data)
      sdx = sqrt(variance/length(data))
      c(xbar - z * sdx, xbar + z * sdx)
}
```

Reference: https://www.stat.wisc.edu/~yandell/st571/R/append7.pdf 

<br /> 

<b>95% confidence interval of the mean of the empirical data</b> 


```r
norm.interval(fit_data, variance=var(fit_data), conf.level = 0.95)
```

```
## [1]  94.38199 113.00853
```

<br /> 

#### <span style="color:blue">Provide the empirical 5th percentile and 95th percentile of the data.</span> 

<br /> 


```r
quantile(x=fit_data, probs=c(.05, .95))
```

```
##     5%    95% 
##   0.01 456.01
```

<br /> 
