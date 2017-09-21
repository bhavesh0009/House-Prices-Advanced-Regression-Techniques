
<!-- rnb-text-begin -->

---
title: "Kaggle House prize prediction"
output: html_notebook
---


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeShnZ3Bsb3QyKVxubGlicmFyeShkcGx5cilcbmxpYnJhcnkodGlkeXIpXG5saWJyYXJ5KGRhdGEudGFibGUpXG5saWJyYXJ5KGtuaXRyKVxucmVxdWlyZShjb3dwbG90KVxubGlicmFyeShSbWlzYylcbmBgYCJ9 -->

```r
library(ggplot2)
library(dplyr)
library(tidyr)
library(data.table)
library(knitr)
require(cowplot)
library(Rmisc)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiTG9hZGluZyByZXF1aXJlZCBwYWNrYWdlOiBsYXR0aWNlXG5Mb2FkaW5nIHJlcXVpcmVkIHBhY2thZ2U6IHBseXJcbi0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLVxuWW91IGhhdmUgbG9hZGVkIHBseXIgYWZ0ZXIgZHBseXIgLSB0aGlzIGlzIGxpa2VseSB0byBjYXVzZSBwcm9ibGVtcy5cbklmIHlvdSBuZWVkIGZ1bmN0aW9ucyBmcm9tIGJvdGggcGx5ciBhbmQgZHBseXIsIHBsZWFzZSBsb2FkIHBseXIgZmlyc3QsIHRoZW4gZHBseXI6XG5saWJyYXJ5KHBseXIpOyBsaWJyYXJ5KGRwbHlyKVxuLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tXG5cbkF0dGFjaGluZyBwYWNrYWdlOiDjpLzjuLFwbHly46S847iyXG5cblRoZSBmb2xsb3dpbmcgb2JqZWN0cyBhcmUgbWFza2VkIGZyb20g46S847ixcGFja2FnZTpkcGx5cuOkvOO4sjpcblxuICAgIGFycmFuZ2UsIGNvdW50LCBkZXNjLCBmYWlsd2l0aCwgaWQsIG11dGF0ZSwgcmVuYW1lLCBzdW1tYXJpc2UsIHN1bW1hcml6ZVxuIn0= -->

```
Loading required package: lattice
Loading required package: plyr
---------------------------------------------------------------------------------------------------------------------------
You have loaded plyr after dplyr - this is likely to cause problems.
If you need functions from both plyr and dplyr, please load plyr first, then dplyr:
library(plyr); library(dplyr)
---------------------------------------------------------------------------------------------------------------------------

Attaching package: <U+393C><U+3E31>plyr<U+393C><U+3E32>

The following objects are masked from <U+393C><U+3E31>package:dplyr<U+393C><U+3E32>:

    arrange, count, desc, failwith, id, mutate, rename, summarise, summarize
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuc2V0d2QoXCJEOi9LYWdnbGUvSG91c2UgUHJpY2VzIEFkdmFuY2VkIFJlZ3Jlc3Npb24gVGVjaG5pcXVlc1wiKVxuYGBgIn0= -->

```r
setwd("D:/Kaggle/House Prices Advanced Regression Techniques")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gPC0gZnJlYWQoXCJ0cmFpbi5jc3ZcIiwgc3RyaW5nc0FzRmFjdG9ycyA9IFRSVUUpXG50ZXN0IDwtIGZyZWFkKFwidGVzdC5jc3ZcIiwgc3RyaW5nc0FzRmFjdG9ycyA9IFRSVUUpXG5gYGAifQ== -->

```r
train <- fread("train.csv", stringsAsFactors = TRUE)
test <- fread("test.csv", stringsAsFactors = TRUE)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxua2FibGUoaGVhZCh0cmFpbikpXG5gYGAifQ== -->

```r
kable(head(train))
```

<!-- rnb-source-end -->
<!--html_preserve-->
<!-- rnb-html-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbImtuaXRfYXNpcyJdLCJzaXppbmdQb2xpY3kiOltdfX0= -->

<table style="width:100%;">
<colgroup>
<col width="0%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="0%" />
<col width="0%" />
<col width="0%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="0%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
<col width="0%" />
<col width="0%" />
<col width="1%" />
<col width="0%" />
<col width="0%" />
<col width="0%" />
<col width="1%" />
<col width="1%" />
<col width="1%" />
</colgroup>
<thead>
<tr class="header">
<th align="right">Id</th>
<th align="right">MSSubClass</th>
<th align="left">MSZoning</th>
<th align="right">LotFrontage</th>
<th align="right">LotArea</th>
<th align="left">Street</th>
<th align="left">Alley</th>
<th align="left">LotShape</th>
<th align="left">LandContour</th>
<th align="left">Utilities</th>
<th align="left">LotConfig</th>
<th align="left">LandSlope</th>
<th align="left">Neighborhood</th>
<th align="left">Condition1</th>
<th align="left">Condition2</th>
<th align="left">BldgType</th>
<th align="left">HouseStyle</th>
<th align="right">OverallQual</th>
<th align="right">OverallCond</th>
<th align="right">YearBuilt</th>
<th align="right">YearRemodAdd</th>
<th align="left">RoofStyle</th>
<th align="left">RoofMatl</th>
<th align="left">Exterior1st</th>
<th align="left">Exterior2nd</th>
<th align="left">MasVnrType</th>
<th align="right">MasVnrArea</th>
<th align="left">ExterQual</th>
<th align="left">ExterCond</th>
<th align="left">Foundation</th>
<th align="left">BsmtQual</th>
<th align="left">BsmtCond</th>
<th align="left">BsmtExposure</th>
<th align="left">BsmtFinType1</th>
<th align="right">BsmtFinSF1</th>
<th align="left">BsmtFinType2</th>
<th align="right">BsmtFinSF2</th>
<th align="right">BsmtUnfSF</th>
<th align="right">TotalBsmtSF</th>
<th align="left">Heating</th>
<th align="left">HeatingQC</th>
<th align="left">CentralAir</th>
<th align="left">Electrical</th>
<th align="right">1stFlrSF</th>
<th align="right">2ndFlrSF</th>
<th align="right">LowQualFinSF</th>
<th align="right">GrLivArea</th>
<th align="right">BsmtFullBath</th>
<th align="right">BsmtHalfBath</th>
<th align="right">FullBath</th>
<th align="right">HalfBath</th>
<th align="right">BedroomAbvGr</th>
<th align="right">KitchenAbvGr</th>
<th align="left">KitchenQual</th>
<th align="right">TotRmsAbvGrd</th>
<th align="left">Functional</th>
<th align="right">Fireplaces</th>
<th align="left">FireplaceQu</th>
<th align="left">GarageType</th>
<th align="right">GarageYrBlt</th>
<th align="left">GarageFinish</th>
<th align="right">GarageCars</th>
<th align="right">GarageArea</th>
<th align="left">GarageQual</th>
<th align="left">GarageCond</th>
<th align="left">PavedDrive</th>
<th align="right">WoodDeckSF</th>
<th align="right">OpenPorchSF</th>
<th align="right">EnclosedPorch</th>
<th align="right">3SsnPorch</th>
<th align="right">ScreenPorch</th>
<th align="right">PoolArea</th>
<th align="left">PoolQC</th>
<th align="left">Fence</th>
<th align="left">MiscFeature</th>
<th align="right">MiscVal</th>
<th align="right">MoSold</th>
<th align="right">YrSold</th>
<th align="left">SaleType</th>
<th align="left">SaleCondition</th>
<th align="right">SalePrice</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="right">1</td>
<td align="right">60</td>
<td align="left">RL</td>
<td align="right">65</td>
<td align="right">8450</td>
<td align="left">Pave</td>
<td align="left">NA</td>
<td align="left">Reg</td>
<td align="left">Lvl</td>
<td align="left">AllPub</td>
<td align="left">Inside</td>
<td align="left">Gtl</td>
<td align="left">CollgCr</td>
<td align="left">Norm</td>
<td align="left">Norm</td>
<td align="left">1Fam</td>
<td align="left">2Story</td>
<td align="right">7</td>
<td align="right">5</td>
<td align="right">2003</td>
<td align="right">2003</td>
<td align="left">Gable</td>
<td align="left">CompShg</td>
<td align="left">VinylSd</td>
<td align="left">VinylSd</td>
<td align="left">BrkFace</td>
<td align="right">196</td>
<td align="left">Gd</td>
<td align="left">TA</td>
<td align="left">PConc</td>
<td align="left">Gd</td>
<td align="left">TA</td>
<td align="left">No</td>
<td align="left">GLQ</td>
<td align="right">706</td>
<td align="left">Unf</td>
<td align="right">0</td>
<td align="right">150</td>
<td align="right">856</td>
<td align="left">GasA</td>
<td align="left">Ex</td>
<td align="left">Y</td>
<td align="left">SBrkr</td>
<td align="right">856</td>
<td align="right">854</td>
<td align="right">0</td>
<td align="right">1710</td>
<td align="right">1</td>
<td align="right">0</td>
<td align="right">2</td>
<td align="right">1</td>
<td align="right">3</td>
<td align="right">1</td>
<td align="left">Gd</td>
<td align="right">8</td>
<td align="left">Typ</td>
<td align="right">0</td>
<td align="left">NA</td>
<td align="left">Attchd</td>
<td align="right">2003</td>
<td align="left">RFn</td>
<td align="right">2</td>
<td align="right">548</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">Y</td>
<td align="right">0</td>
<td align="right">61</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="right">0</td>
<td align="right">2</td>
<td align="right">2008</td>
<td align="left">WD</td>
<td align="left">Normal</td>
<td align="right">208500</td>
</tr>
<tr class="even">
<td align="right">2</td>
<td align="right">20</td>
<td align="left">RL</td>
<td align="right">80</td>
<td align="right">9600</td>
<td align="left">Pave</td>
<td align="left">NA</td>
<td align="left">Reg</td>
<td align="left">Lvl</td>
<td align="left">AllPub</td>
<td align="left">FR2</td>
<td align="left">Gtl</td>
<td align="left">Veenker</td>
<td align="left">Feedr</td>
<td align="left">Norm</td>
<td align="left">1Fam</td>
<td align="left">1Story</td>
<td align="right">6</td>
<td align="right">8</td>
<td align="right">1976</td>
<td align="right">1976</td>
<td align="left">Gable</td>
<td align="left">CompShg</td>
<td align="left">MetalSd</td>
<td align="left">MetalSd</td>
<td align="left">None</td>
<td align="right">0</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">CBlock</td>
<td align="left">Gd</td>
<td align="left">TA</td>
<td align="left">Gd</td>
<td align="left">ALQ</td>
<td align="right">978</td>
<td align="left">Unf</td>
<td align="right">0</td>
<td align="right">284</td>
<td align="right">1262</td>
<td align="left">GasA</td>
<td align="left">Ex</td>
<td align="left">Y</td>
<td align="left">SBrkr</td>
<td align="right">1262</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">1262</td>
<td align="right">0</td>
<td align="right">1</td>
<td align="right">2</td>
<td align="right">0</td>
<td align="right">3</td>
<td align="right">1</td>
<td align="left">TA</td>
<td align="right">6</td>
<td align="left">Typ</td>
<td align="right">1</td>
<td align="left">TA</td>
<td align="left">Attchd</td>
<td align="right">1976</td>
<td align="left">RFn</td>
<td align="right">2</td>
<td align="right">460</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">Y</td>
<td align="right">298</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="right">0</td>
<td align="right">5</td>
<td align="right">2007</td>
<td align="left">WD</td>
<td align="left">Normal</td>
<td align="right">181500</td>
</tr>
<tr class="odd">
<td align="right">3</td>
<td align="right">60</td>
<td align="left">RL</td>
<td align="right">68</td>
<td align="right">11250</td>
<td align="left">Pave</td>
<td align="left">NA</td>
<td align="left">IR1</td>
<td align="left">Lvl</td>
<td align="left">AllPub</td>
<td align="left">Inside</td>
<td align="left">Gtl</td>
<td align="left">CollgCr</td>
<td align="left">Norm</td>
<td align="left">Norm</td>
<td align="left">1Fam</td>
<td align="left">2Story</td>
<td align="right">7</td>
<td align="right">5</td>
<td align="right">2001</td>
<td align="right">2002</td>
<td align="left">Gable</td>
<td align="left">CompShg</td>
<td align="left">VinylSd</td>
<td align="left">VinylSd</td>
<td align="left">BrkFace</td>
<td align="right">162</td>
<td align="left">Gd</td>
<td align="left">TA</td>
<td align="left">PConc</td>
<td align="left">Gd</td>
<td align="left">TA</td>
<td align="left">Mn</td>
<td align="left">GLQ</td>
<td align="right">486</td>
<td align="left">Unf</td>
<td align="right">0</td>
<td align="right">434</td>
<td align="right">920</td>
<td align="left">GasA</td>
<td align="left">Ex</td>
<td align="left">Y</td>
<td align="left">SBrkr</td>
<td align="right">920</td>
<td align="right">866</td>
<td align="right">0</td>
<td align="right">1786</td>
<td align="right">1</td>
<td align="right">0</td>
<td align="right">2</td>
<td align="right">1</td>
<td align="right">3</td>
<td align="right">1</td>
<td align="left">Gd</td>
<td align="right">6</td>
<td align="left">Typ</td>
<td align="right">1</td>
<td align="left">TA</td>
<td align="left">Attchd</td>
<td align="right">2001</td>
<td align="left">RFn</td>
<td align="right">2</td>
<td align="right">608</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">Y</td>
<td align="right">0</td>
<td align="right">42</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="right">0</td>
<td align="right">9</td>
<td align="right">2008</td>
<td align="left">WD</td>
<td align="left">Normal</td>
<td align="right">223500</td>
</tr>
<tr class="even">
<td align="right">4</td>
<td align="right">70</td>
<td align="left">RL</td>
<td align="right">60</td>
<td align="right">9550</td>
<td align="left">Pave</td>
<td align="left">NA</td>
<td align="left">IR1</td>
<td align="left">Lvl</td>
<td align="left">AllPub</td>
<td align="left">Corner</td>
<td align="left">Gtl</td>
<td align="left">Crawfor</td>
<td align="left">Norm</td>
<td align="left">Norm</td>
<td align="left">1Fam</td>
<td align="left">2Story</td>
<td align="right">7</td>
<td align="right">5</td>
<td align="right">1915</td>
<td align="right">1970</td>
<td align="left">Gable</td>
<td align="left">CompShg</td>
<td align="left">Wd Sdng</td>
<td align="left">Wd Shng</td>
<td align="left">None</td>
<td align="right">0</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">BrkTil</td>
<td align="left">TA</td>
<td align="left">Gd</td>
<td align="left">No</td>
<td align="left">ALQ</td>
<td align="right">216</td>
<td align="left">Unf</td>
<td align="right">0</td>
<td align="right">540</td>
<td align="right">756</td>
<td align="left">GasA</td>
<td align="left">Gd</td>
<td align="left">Y</td>
<td align="left">SBrkr</td>
<td align="right">961</td>
<td align="right">756</td>
<td align="right">0</td>
<td align="right">1717</td>
<td align="right">1</td>
<td align="right">0</td>
<td align="right">1</td>
<td align="right">0</td>
<td align="right">3</td>
<td align="right">1</td>
<td align="left">Gd</td>
<td align="right">7</td>
<td align="left">Typ</td>
<td align="right">1</td>
<td align="left">Gd</td>
<td align="left">Detchd</td>
<td align="right">1998</td>
<td align="left">Unf</td>
<td align="right">3</td>
<td align="right">642</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">Y</td>
<td align="right">0</td>
<td align="right">35</td>
<td align="right">272</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="right">0</td>
<td align="right">2</td>
<td align="right">2006</td>
<td align="left">WD</td>
<td align="left">Abnorml</td>
<td align="right">140000</td>
</tr>
<tr class="odd">
<td align="right">5</td>
<td align="right">60</td>
<td align="left">RL</td>
<td align="right">84</td>
<td align="right">14260</td>
<td align="left">Pave</td>
<td align="left">NA</td>
<td align="left">IR1</td>
<td align="left">Lvl</td>
<td align="left">AllPub</td>
<td align="left">FR2</td>
<td align="left">Gtl</td>
<td align="left">NoRidge</td>
<td align="left">Norm</td>
<td align="left">Norm</td>
<td align="left">1Fam</td>
<td align="left">2Story</td>
<td align="right">8</td>
<td align="right">5</td>
<td align="right">2000</td>
<td align="right">2000</td>
<td align="left">Gable</td>
<td align="left">CompShg</td>
<td align="left">VinylSd</td>
<td align="left">VinylSd</td>
<td align="left">BrkFace</td>
<td align="right">350</td>
<td align="left">Gd</td>
<td align="left">TA</td>
<td align="left">PConc</td>
<td align="left">Gd</td>
<td align="left">TA</td>
<td align="left">Av</td>
<td align="left">GLQ</td>
<td align="right">655</td>
<td align="left">Unf</td>
<td align="right">0</td>
<td align="right">490</td>
<td align="right">1145</td>
<td align="left">GasA</td>
<td align="left">Ex</td>
<td align="left">Y</td>
<td align="left">SBrkr</td>
<td align="right">1145</td>
<td align="right">1053</td>
<td align="right">0</td>
<td align="right">2198</td>
<td align="right">1</td>
<td align="right">0</td>
<td align="right">2</td>
<td align="right">1</td>
<td align="right">4</td>
<td align="right">1</td>
<td align="left">Gd</td>
<td align="right">9</td>
<td align="left">Typ</td>
<td align="right">1</td>
<td align="left">TA</td>
<td align="left">Attchd</td>
<td align="right">2000</td>
<td align="left">RFn</td>
<td align="right">3</td>
<td align="right">836</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">Y</td>
<td align="right">192</td>
<td align="right">84</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="left">NA</td>
<td align="right">0</td>
<td align="right">12</td>
<td align="right">2008</td>
<td align="left">WD</td>
<td align="left">Normal</td>
<td align="right">250000</td>
</tr>
<tr class="even">
<td align="right">6</td>
<td align="right">50</td>
<td align="left">RL</td>
<td align="right">85</td>
<td align="right">14115</td>
<td align="left">Pave</td>
<td align="left">NA</td>
<td align="left">IR1</td>
<td align="left">Lvl</td>
<td align="left">AllPub</td>
<td align="left">Inside</td>
<td align="left">Gtl</td>
<td align="left">Mitchel</td>
<td align="left">Norm</td>
<td align="left">Norm</td>
<td align="left">1Fam</td>
<td align="left">1.5Fin</td>
<td align="right">5</td>
<td align="right">5</td>
<td align="right">1993</td>
<td align="right">1995</td>
<td align="left">Gable</td>
<td align="left">CompShg</td>
<td align="left">VinylSd</td>
<td align="left">VinylSd</td>
<td align="left">None</td>
<td align="right">0</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">Wood</td>
<td align="left">Gd</td>
<td align="left">TA</td>
<td align="left">No</td>
<td align="left">GLQ</td>
<td align="right">732</td>
<td align="left">Unf</td>
<td align="right">0</td>
<td align="right">64</td>
<td align="right">796</td>
<td align="left">GasA</td>
<td align="left">Ex</td>
<td align="left">Y</td>
<td align="left">SBrkr</td>
<td align="right">796</td>
<td align="right">566</td>
<td align="right">0</td>
<td align="right">1362</td>
<td align="right">1</td>
<td align="right">0</td>
<td align="right">1</td>
<td align="right">1</td>
<td align="right">1</td>
<td align="right">1</td>
<td align="left">TA</td>
<td align="right">5</td>
<td align="left">Typ</td>
<td align="right">0</td>
<td align="left">NA</td>
<td align="left">Attchd</td>
<td align="right">1993</td>
<td align="left">Unf</td>
<td align="right">2</td>
<td align="right">480</td>
<td align="left">TA</td>
<td align="left">TA</td>
<td align="left">Y</td>
<td align="right">40</td>
<td align="right">30</td>
<td align="right">0</td>
<td align="right">320</td>
<td align="right">0</td>
<td align="right">0</td>
<td align="left">NA</td>
<td align="left">MnPrv</td>
<td align="left">Shed</td>
<td align="right">700</td>
<td align="right">10</td>
<td align="right">2009</td>
<td align="left">WD</td>
<td align="left">Normal</td>
<td align="right">143000</td>
</tr>
</tbody>
</table>


<!-- rnb-html-end -->
<!--/html_preserve-->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW5fbnVsbHMgPC0gYXMuZGF0YS5mcmFtZShjb2xTdW1zKGlzLm5hKHRyYWluKSkpI2FzLmRhdGEuZnJhbWUoc2FwcGx5KFggPSB0cmFpbiwgRlVOID0gZnVuY3Rpb24oeCkgc3VtKGlzLm5hKHgpKSkpXG50cmFpbl9udWxscyA8LSBhZGRfcm93bmFtZXModHJhaW5fbnVsbHMsIFwiQ29sdW1uXCIpXG5gYGAifQ== -->

```r
train_nulls <- as.data.frame(colSums(is.na(train)))#as.data.frame(sapply(X = train, FUN = function(x) sum(is.na(x))))
train_nulls <- add_rownames(train_nulls, "Column")
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiRGVwcmVjYXRlZCwgdXNlIHRpYmJsZTo6cm93bmFtZXNfdG9fY29sdW1uKCkgaW5zdGVhZC5cbiJ9 -->

```
Deprecated, use tibble::rownames_to_column() instead.
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY29sbmFtZXModHJhaW5fbnVsbHMpWzJdIDwtIFwibnVsbHNcIlxudHJhaW5fbnVsbHMkbm90TnVsbHMgPSBucm93KHRyYWluKSAtIHRyYWluX251bGxzJG51bGxzXG5gYGAifQ== -->

```r
colnames(train_nulls)[2] <- "nulls"
train_nulls$notNulls = nrow(train) - train_nulls$nulls
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW5fbnVsbHMgJT4lXG4gIGZpbHRlcihudWxscyA+IDApICU+JVxuICBnYXRoZXIoXCJudWxsX2ZsYWdcIiwgXCJjb3VudFwiLCAtQ29sdW1uKSAlPiVcbiAgZ2dwbG90KGFlcyh4ID0gQ29sdW1uLCB5ID0gY291bnQsIGZpbGwgPSBudWxsX2ZsYWcpKSArXG4gIGdlb21fYmFyKHN0YXQgPSBcImlkZW50aXR5XCIscG9zaXRpb24gPSBcImZpbGxcIikgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcImJvdHRvbVwiKSArXG4gIGNvb3JkX2ZsaXAoKVxuYGBgIn0= -->

```r
train_nulls %>%
  filter(nulls > 0) %>%
  gather("null_flag", "count", -Column) %>%
  ggplot(aes(x = Column, y = count, fill = null_flag)) +
  geom_bar(stat = "identity",position = "fill") +
  theme(legend.position = "bottom") +
  coord_flip()
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb252ZXJ0aW5nIHN1YmNsYXNzIHRvIGZhY3RvclxudHJhaW4kTVNTdWJDbGFzcyA9IGFzLmZhY3Rvcih0cmFpbiRNU1N1YkNsYXNzKVxuYGBgIn0= -->

```r
# Converting subclass to factor
train$MSSubClass = as.factor(train$MSSubClass)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBWaXN1YWxpemluZyBzYWxlIHByaWNlIHZzIE1zU3ViQ2xhc3NcbmdncGxvdCh0cmFpbiwgYWVzKHggPSBNU1N1YkNsYXNzLCB5ID0gU2FsZVByaWNlKSkgK1xuICBnZW9tX2JveHBsb3QoKVxuYGBgIn0= -->

```r
# Visualizing sale price vs MsSubClass
ggplot(train, aes(x = MSSubClass, y = SalePrice)) +
  geom_boxplot()
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyB2aXN1YWxpemUgbnVtYmVyIG9mIG9ic2VydmF0aW9uIGZvciBlYWNoIGNhdGVnb3J5XG5nZ3Bsb3QodHJhaW4sIGFlcyh4ID0gTVNTdWJDbGFzcywgZmlsbCA9IE1TU3ViQ2xhc3MpKSArXG4gIGdlb21fYmFyKCkgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSAgXCJub25lXCIpXG5gYGAifQ== -->

```r
# visualize number of observation for each category
ggplot(train, aes(x = MSSubClass, fill = MSSubClass)) +
  geom_bar() +
  theme(legend.position =  "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyB2aXN1YWxpemUgbnVtYmVyIG9mIG9ic2VydmF0aW9uIGZvciBlYWNoIGNhdGVnb3J5XG5nZ3Bsb3QodHJhaW4sIGFlcyh4ID0gTVNab25pbmcpKSArXG4gIGdlb21fYmFyKClcbmBgYCJ9 -->

```r
# visualize number of observation for each category
ggplot(train, aes(x = MSZoning)) +
  geom_bar()
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBWaXN1YWxpemluZyBzYWxlIHByaWNlIHZzIE1zU3ViQ2xhc3NcbmdncGxvdCh0cmFpbiwgYWVzKHggPSBNU1pvbmluZywgeSA9IFNhbGVQcmljZSkpICtcbiAgZ2VvbV9ib3hwbG90KClcbmBgYCJ9 -->

```r
# Visualizing sale price vs MsSubClass
ggplot(train, aes(x = MSZoning, y = SalePrice)) +
  geom_boxplot()
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucGxvdDEgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IExvdEZyb250YWdlKSkgK1xuICAgICAgICAgICAgZ2VvbV9oaXN0b2dyYW0oYmlud2lkdGggPSAxMCkgXG4jIFZpc3VhbGl6aW5nIHNhbGUgcHJpY2UgdnMgTG90RnJvbnRhZ2VcbnBsb3QyIDwtIGdncGxvdCh0cmFpbiwgYWVzKHggPSBMb3RGcm9udGFnZSwgeSA9IFNhbGVQcmljZSkpICtcbiAgICAgICAgICBnZW9tX3BvaW50KCkgK1xuICAgICAgICAgIGdlb21fc21vb3RoKG1ldGhvZCA9IFwibG1cIikgXG5wbG90X2dyaWQocGxvdDEsIHBsb3QyLCBhbGlnbj0naCcpXG5gYGAifQ== -->

```r
plot1 <- ggplot(train, aes(x = LotFrontage)) +
            geom_histogram(binwidth = 10) 
# Visualizing sale price vs LotFrontage
plot2 <- ggplot(train, aes(x = LotFrontage, y = SalePrice)) +
          geom_point() +
          geom_smooth(method = "lm") 
plot_grid(plot1, plot2, align='h')
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiUmVtb3ZlZCAyNTkgcm93cyBjb250YWluaW5nIG5vbi1maW5pdGUgdmFsdWVzIChzdGF0X2JpbikuUmVtb3ZlZCAyNTkgcm93cyBjb250YWluaW5nIG5vbi1maW5pdGUgdmFsdWVzIChzdGF0X3Ntb290aCkuUmVtb3ZlZCAyNTkgcm93cyBjb250YWluaW5nIG1pc3NpbmcgdmFsdWVzIChnZW9tX3BvaW50KS5cbiJ9 -->

```
Removed 259 rows containing non-finite values (stat_bin).Removed 259 rows containing non-finite values (stat_smooth).Removed 259 rows containing missing values (geom_point).
```



<!-- rnb-output-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9bG9nKCBMb3RBcmVhKSwgeSA9IFNhbGVQcmljZSkpICtcbiAgZ2VvbV9wb2ludCgpICtcbiAgZ2VvbV9zbW9vdGgobWV0aG9kID0gXCJsbVwiKVxuYGBgIn0= -->

```r
ggplot(train, aes(x =log( LotArea), y = SalePrice)) +
  geom_point() +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBTdHJvbmcgcmVsYXRpb24gc2hpcCBiZXR3ZWVuIGxvdCBhcmVhIGFuZCBzYWxlIHByaWNlXG4jIENyZWF0aW5nIG5ldyBmZWF0dXJlIGZvciBwcml6ZSBwZXIgc3F1YXJlIGZlZXRcbnRyYWluJHBzZiA8LSB0cmFpbiRTYWxlUHJpY2UgLyB0cmFpbiRMb3RBcmVhXG5gYGAifQ== -->

```r
# Strong relation ship between lot area and sale price
# Creating new feature for prize per square feet
train$psf <- train$SalePrice / train$LotArea
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KFN0cmVldCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSlcbmBgYCJ9 -->

```r
train %>%
  group_by(Street) %>%
  summarise(count = n())
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MiwibnJvdyI6Mn0sInJkZiI6Ikg0c0lBQUFBQUFBQUJtVlFRVTdETUJEY3hFNnFXZ0pWNGgyTkJBZGVnTVFWd2FWWGs3b1E0ZHFWNHdTT3ZJZ25KcXp0YkVYTndkN1Zlc1k3TTg4UHV6dXhFd0JRQXVNRmxBeGJYdUpWQUlkMXFGOEE3Q1lDZ0YybGlvK3hYZ0JyclVhbGUrdzI4VFZOK2FNYk5mVlBjbFFacTJxMTdJbDAvdW9nVzI4ZGRoTWVXbG9qK2lmUjJad3h4RjU2MlJ5Y1BQNWJZSENXcTZwZnZGUEtuelhZd2ZpTXQzYjJzeUZ1bFBDTjF6elBVNUoxQVY3WmsrK3NRV2dab3FveWRZWExCcHZCaEsvMzIvWjlNQi9iMi90Z1lja1ZsbjFMeG4vN3NKT1Q5WXE4S1BQV0dVVmV0SHhWRlBnMWVvZ1dtcFByRE5rVk9PMGJiNzBrbkdpdHBrbktmUG9GaldhMHh4a0NBQUE9In0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Street"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]}],"data":[{"1":"Grvl","2":"6"},{"1":"Pave","2":"1454"}],"options":{"columns":{"min":{},"max":[10],"total":[2]},"rows":{"min":[10],"max":[10],"total":[2]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBUb28gbGVzcyB2YWx1ZXMgZm9yIEdydmwuIFdlIGNhbiBpZ25vcmUgdGhhdCwgYnV0IExldCdzIGZpcnN0IGNoZWNrIGJveC1wbG90IGlmIGdyYXZlbCBjYW4gZXhwbGFpbiBvdXRsaWVycz9cbmdncGxvdCh0cmFpbiwgYWVzKHggPSBTdHJlZXQsIHkgPSBwc2YpKSArXG4gIGdlb21fdmlvbGluKGZpbGwgPSBcInJlZFwiKVxuYGBgIn0= -->

```r
# Too less values for Grvl. We can ignore that, but Let's first check box-plot if gravel can explain outliers?
ggplot(train, aes(x = Street, y = psf)) +
  geom_violin(fill = "red")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEFsbGV5KSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpKVxuYGBgIn0= -->

```r
train %>%
  group_by(Alley) %>%
  summarise(count = n())
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MiwibnJvdyI6M30sInJkZiI6Ikg0c0lBQUFBQUFBQUJtVlFzVzdDTUJDOTJBNFZrYWlRK0FvR0lzSEVXcWtTSytwRVJ6ZVlOc0xZeUhFQzNmcmpKYjNFT1NUY3dmSHo1YjI3ZSsvdGRiZktkaGtBTU9BaUFjWVJDb2FmQkFTTXUvc0t3R2M5QWZnRWI5Ny94UGNQUUV3ZWFkVW9YU0dhOW9wUUZSdlhhTUpiMmFoSWxSWmFWaVM2dHpySXdsdUg2SWFIQnEvd3pGSHhIbHJ3TmxKbGUrbGxmbkR5OUcrSXdWcThXZnFpdGZxK3IyRnI0eVBaMk5sTFR0SUoyVzdiOWpkczlrQitzbWRmV29OVTFpV1dSc3NsTGlwTWE5TzEzaStLcjlvY0Y4dDE1MkNJRjRaNXllQ2NNQXN6QlRsUEtTOWxQa3VqeUl1V0g0b3lmMFlQdllYODdFcDBPRVNGMVNyMzFrdmlaWVhWVkFteDMvNEFUbkY4cnlBQ0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Alley"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]}],"data":[{"1":"Grvl","2":"50"},{"1":"Pave","2":"41"},{"1":"NA","2":"1369"}],"options":{"columns":{"min":{},"max":[10],"total":[2]},"rows":{"min":[10],"max":[10],"total":[3]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBUb28gbWFueSBudWxsIHZhbHVlcyAsIGJ1dCBoZXJlIE5BIG1lYW5zIG5vIGFsbGV5IGFjY2VzcywgY2FuIGJlIGdvb2QgZmVhdHVyZS4gTGV0J3MgY2hhbmdlIHZhbHVlIGZvciB0aGF0LlxudHJhaW5baXMubmEoQWxsZXkpXSRBbGxleSA9IFwiTm9cIlxuYGBgIn0= -->

```r
# Too many null values , but here NA means no alley access, can be good feature. Let's change value for that.
train[is.na(Alley)]$Alley = "No"
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBUb28gbGVzcyB2YWx1ZXMgZm9yIEdydmwuIFdlIGNhbiBpZ25vcmUgdGhhdCwgYnV0IExldCdzIGZpcnN0IGNoZWNrIGJveC1wbG90IGlmIGdyYXZlbCBjYW4gZXhwbGFpbiBvdXRsaWVycz9cbmdncGxvdCh0cmFpbiwgYWVzKHggPSBBbGxleSwgeSA9IHBzZiwgZmlsbCA9IEFsbGV5KSkgK1xuICBnZW9tX2JveHBsb3QoKVxuYGBgIn0= -->

```r
# Too less values for Grvl. We can ignore that, but Let's first check box-plot if gravel can explain outliers?
ggplot(train, aes(x = Alley, y = psf, fill = Alley)) +
  geom_boxplot()
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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v707vKv5L9yScijf9T1et7q1r4MGN8dtHu/y01esefNUueVkWTxuMdiHA4JxvOddzXfTdUcezMMB+WiOlpcFRxsy5U4P251aA7bZtw0Pr38LIYe19gvdqpn5UGrw+tOBHOclulngJdnAS7KBl2QDL8kGXpINvCQbeEk28JJs4CXZwEuygbdv60Vz5c16Ya/VGsetjRqBt2/LaXN5C3hzB96+lQ8/9xeOgTd34O3Zav74fdG8tQR48wbentXFc/NuOXu8P/ymKCa/dJfM2hWF+CXfww28/XLvQ+VvltjhNavg5t3LPNt6QLdgjirw9su9p8hyao3u8JbFT942699bsqVdDpdDupliTIG3X26n698GcIvXU25uM9e/UWzAgbdX7v665j1H9nibXzM7YQuXVUOqwNur7fuKWKhf4LW74+rhlVVDqsDbp93bBpdm77rHe3BP7nL6a1YNqQJvn5rlrX+wxbteTH71ttl837yK+yD9pjSDDrx9qrbLWXuBw/tDZf6Sh2pQb9wwrsDbo9V8B7MqZscnKYqvv3O/sds5U/TAmziONaQLvGn7gYsd0gXelNnDwNpvBzbowJuy9aL45tZzGHHgJdnAS7KBl2QDL8kGXpINvCQbeEk28JJs4CXZwEuy/RMl6kLCPnR+6wAAAABJRU5ErkJggg==" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KExvdFNoYXBlKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpKVxuYGBgIn0= -->

```r
train %>%
  group_by(LotShape) %>%
  summarise(count = n(),
            avg = mean(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6NH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0JqS0FNc3k4SUZtd0pFZ0RXQXpFUjlIQWxwTmFscHBUREdRSmdHVWhvc3llUVlZSXBoR0NhUXhqQnFXbW81bkVtcHlUV0F3ekNHNThXbUp5U1g0UmtQVVBpS0VPWW53Q3BEV0JHT2dUNXJsQW1nOGs3bUM4dUVWZDVtbXhnMEhWdmdZaEZWRUgxY3plOXc2aGV4M01sR0tDbDB1cVE2eGovbzltQTFkS1lrbWlYbHBSWW00cXVvUHlnR0l3QnpGREJUbDg4a3VDTXhJTFV1R3V6aS9OSzRINUtyRU0zVmVjUmZubGVqQ0RRTzVuYWdBUy8vLy8vd1B4RTRwaTl2eUNrc3o4UEtCU0psQWNzS0k1bGJFSVRVQ2dOQTlrZElwdWNrWnBYcmF1a1NFa1RNQVJ4Z0MxanhFYWlUQTJNOFJPRmxnNHNNSkNPalV2UFRNUDdxMmN4S1RVSENpSEQrZ0hzQmYwQ29veTRaN2xBb29XNjVYa2x5VEMxSEVsNStmQVJDQVI5ZzhBdndKREVISUNBQUE9In0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["LotShape"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"IR1","2":"484","3":"19.63874"},{"1":"IR2","2":"41","3":"16.47947"},{"1":"IR3","2":"10","3":"10.70616"},{"1":"Reg","2":"925","3":"22.13422"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[4]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBJUjMgc2hvdWxkIGhhdmUgbGVhc3QgcHJpemUsIFJlZyBoaWdoZXN0IGluIG15IG9waW5pb24uIExldCdzIGNoZWNrXG5nZ3Bsb3QodHJhaW4sIGFlcyh4ID0gTG90U2hhcGUsIHkgPSBwc2YsIGZpbGwgPSBMb3RTaGFwZSkpICtcbiAgZ2VvbV9ib3hwbG90KClcbmBgYCJ9 -->

```r
# IR3 should have least prize, Reg highest in my opinion. Let's check
ggplot(train, aes(x = LotShape, y = psf, fill = LotShape)) +
  geom_boxplot()
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KExhbmRDb250b3VyKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpKVxuYGBgIn0= -->

```r
train %>%
  group_by(LandContour) %>%
  summarise(count = n(),
            avg = mean(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6NH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVJUVXJEUUJTZVpOSnFJNWFDQnlpSUlBaU5VQkdYQm5XaGtsWGRkRHVtYVMwZFo4cGtrZ3BTS0hvUGNTdDRDMC9nemt0NEEybDhrK1FGbXNXYitlWjd2OSs4d2RXdzd3NWRRb2hOcUdNUm13SjBiRGdzNHBDV3VaOElvWHNBd0VOM2pUZDNtb1NjTSsrTmhDYVAwb2pIZ0RxNXQyRHBoWmdodkE3dUVBWnlVY0dVMXlvMVFzNWlMRlNWSDdOUVN3Vm9EWVlEbllQMXdRNGdxd3QzMi9EKzhlZlJVcjN2KzJkcDkvYnI0OFUvL0w3WmRwdEwvL1I1OFBQNjlsdTBvMW10Z3p0aW1ubGp4UjZqK2tBQ09CeUlsdVJPd01Ub1Vnb3RFMVVOTGhPaFVSaExKN1U2TFNVWEh0WXlFdXdWSEZtVy9SV3lOb0szNUZ4UHBZQlEyNnloVVp2V1VqV2lrd2hUZXRRTEh4SXg2L1ZQaktSeVo2VHNaNVhmaHBnV1BSMzhpZ1orZGlRbVV4R2hMTTd1STE0KzJxQWhsK0ROMWJRUzZ3SWJlMXBxaG5GdUtEa3l4YzdXLzVGSWlDOTFBZ0FBIn0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["LandContour"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"Bnk","2":"63","3":"15.83626"},{"1":"HLS","2":"50","3":"23.46141"},{"1":"Low","2":"36","3":"11.90876"},{"1":"Lvl","2":"1311","3":"21.48173"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[4]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KFV0aWxpdGllcykgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSkgJT4lXG4gIGFycmFuZ2UoZGVzYyhjb3VudCksIGRlc2MoYXZnKSlcbmBgYCJ9 -->

```r
train %>%
  group_by(Utilities) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(count), desc(avg))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6Mn0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVJ2VTdETUJCMjRnUVVTMVNWK2dTSWxXYW95bDRrQmliRWp4QmQzY1F0RnNhdUhLY3dzckR6TEREeUZMeEZueUxobk5pUjZzSDIzWGQzMzNkM3ZyOWF6c2lTSUlSaWhKTUl4UmpNSklZclFnbks3UHVPRUo2QUFSRjgwaVhhWVBjZUpCNEp0bU9pQW12Y1JSMTZLY1J0dmZMZWpYcGdUelNvVEF0QksxODQwSzFwWVpRR3E0SGpoTk1mSno2eS91Smlzci83KzcxZW5KMlc1NTlmM3owdGJnTW1VbEpEODdXbXJ5d1Vsb0I1WWV6QTdORnd3UTJIZ0c5UDFkSTRCOVBkSm1ESnRIckxQVlBYNkFkY2JkczJmZk1IeWNkcWE3aVNrQnJicGFaQnI1RU9nSEV0TFhVNUxaNXIrVEtkemUxQWJnbkk2Ym5mR0d6Y2F5WitFYWxmS1pNYkxwa2ZTOUFWRTg0WndRemRDUGxXODJGWUFtaVZHMldvenlPRkVoN3BmNmI1QitWN01tSkRBZ0FBIn0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Utilities"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"AllPub","2":"1459","3":"21.077764"},{"1":"NoSeWa","2":"1","3":"9.565217"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[2]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogV2UgY2FuIGlnbm9yZSB0aGlzIHZhcmlhYmxlLlxuYGBgIn0= -->

```r
# Conclusion : We can ignore this variable.
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KExvdENvbmZpZykgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSkgJT4lXG4gIGFycmFuZ2UoZGVzYyhjb3VudCksIGRlc2MoYXZnKSlcbmBgYCJ9 -->

```r
train %>%
  group_by(LotConfig) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(count), desc(avg))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6NX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJtVlJQMHZEUUJTLzVGSkxBOVpDRVJ4MGRCRWFNVkluaDBDTFVIRFFDdEpGNFV5VEducTlxNWVrT2pycDkvQVQrQ1VjbmV3SGNPcnVMRFMrSkhmUnh1SGQvZDd2M3IvZnZYNTNZSnNERXlHa0kyeG9TTWNBRFIwT0RSbW9sdDRQQ09FbUFIakI2M0JYcEdsWlVzWkQ2R3JTR3ZWbUhnMEJOYkpveVhhNFlKNlFYclVUMCs0RmNhV0xUL3IyTHp4VUtUMFdCa092Vkw3aVVoS3E2a1ZQbjdnUkY0Q1dZSEpTWXhzQ3FvQ3Z3ZmJ6U1ZFOWZYT09kbnJqK2VlclkyOHVLb3ZkTCtmQXY1cWNQVzg0N1MyNk43OThjNDZmWHQ3dlBzN3oxamdwZFRPSEpDS1dMOGprMzNBTU9EVWNsbVR0bEVjZHp2eGdWRWpnTVl1VVlESWJsYXJVQkwrM1ZLVlVqUDRJUjVJazM3bkFsZUFxbjBZQlp4Q3FOK1YyL3M2cWlSTFJpRmxhZXRoeWIyTTJidG50VkpCY0taTDlORmxJWVp6M05OUkhGRXYxMkNoZ25wSkZ5WTFIcFZNSERaa0VheXFDUXF3SmJHaEZQQ0lxem5RNVZVeSt2ZVVQUVFudlBKZ0NBQUE9In0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["LotConfig"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"Inside","2":"1052","3":"22.11440"},{"1":"Corner","2":"263","3":"18.08554"},{"1":"CulDSac","2":"94","3":"17.39986"},{"1":"FR2","2":"47","3":"21.09540"},{"1":"FR3","2":"4","3":"28.52592"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[5]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogSG1tbS4uLlxuYGBgIn0= -->

```r
# Conclusion : Hmmm...
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KExhbmRTbG9wZSkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSkgJT4lXG4gIGFycmFuZ2UoZGVzYyhjb3VudCksIGRlc2MoYXZnKSlcbmBgYCJ9 -->

```r
train %>%
  group_by(LandSlope) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(count), desc(avg))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6M30sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVJ6VTZFTUJBdUZEUVEzV3ppelhlQUE4bDZaaE9UdmVqRjliRFhDbVZsclMyQmducnpibndVRTUvR2kwL2l3Y1VwdE1UdGdjN0hONy9mek0zbEpnazNJVUxJUmRoemtJc0JlaTQ4RHZKUW9Pd3pRdmdNQUhqdzZXakJxUklHZkJCOHhHaEhXUU5vUG5oSEZxOGtNL0JhNUFhdWFXZWwreGtqamNtZWFoWWtrNklHdElkUFQrQVhZSmY2ZjZhNGRISDc4VVhKUzVyczNsZWZTNTZlbHlmZmI5SFAyQUwzVnRVd0o1TEVSVTBlcVQwRUI4NldFRndSbnErWnFPZzBxbWk1TkZKSXQ3V3FCTFY0aWswbE5hVDdDay9mOTcramtJUGdZMUhKVW5BSWRkV21mV3RXcDdhSWVjdFY2VHpLN2x2K0VDVVhTcEErQzlMOUhIMnFmMWoxOU13aWZMTmV5cmNsbjJReGNrZk5zV2FnWVpBUVYzVTVpUTJCYldJcEpERnhZU2FZWWNZcjdmOEFHbm1SL2xnQ0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["LandSlope"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"Gtl","2":"1382","3":"21.330778"},{"1":"Mod","2":"65","3":"18.416218"},{"1":"Sev","2":"13","3":"6.602588"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[3]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTmljZSBPbmUhISBTcGVpY2FsbHkgd2UgY2FuIHBlbmFsaXplIFNldiBzbG9wZXNcbmBgYCJ9 -->

```r
# Conclusion : Nice One!! Speically we can penalize Sev slopes
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KE5laWdoYm9yaG9vZCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSkgJT4lXG4gIGFycmFuZ2UoZGVzYyhjb3VudCksIGRlc2MoYXZnKSlcbmBgYCJ9 -->

```r
train %>%
  group_by(Neighborhood) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(count), desc(avg))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6MjV9LCJyZGYiOiJINHNJQUFBQUFBQUFCbDJVVFV3VFFSVEh0OSsySUlLZ1VxS1NhREI4dElVV2lGRVRtUmJrSzlDYUZncEdPR3k3UTd2cGRxZHV0MVREQldNTVhBd0hFcU1lVElqb0JlTUJENW9ZYnhqRWhBUTltbmdnTVpKNDBLZ0hqQWZxMjNabm9UMzhkdlkvOCthOW1YbHZKdGd6N3JHTjJ4aUcwVE1HbzQ3UkcrRFhxSWVQampFeVZxVzl5VENHYXZpQkVjTmhhTzJBMHBxQm84QWg0RGlnR0ZjQk5jQVI0SmppQ2JBQTVVQWxVQXNvd1V6QUNhQTZINGhoeWdyKzg3NHI4b3NwWG9SWndOTllTS3RlN0dxdnhTY2t4WmdzN3NzTVRzdVl6dkZKUGF5QXRVRXBFZUk1VFhZTG1KVzZKVTBTUVlnZGtCS2JuU0thdk1KbFdZbExVOW5IQ3hFc3lUVE9RRTlnSkJpa2c4T1k1VWcyckVsZWpzYXhvRXFUMzV2RW1oLy8xVVNZRitpWTJUOVdORWlDUEJmVDF1dVhRUFhUbUphQXdJMlFMTjI1S1RRMkVCcWxma0pzOWhiVzFsNVFZNW9rU1N5bE5UOGhtWWpZUjQzTkkzd3lzajgxakxHWUFGbWNDMU5VWU5NMEZWcUNwdGlvREFmR01IdHFlU2lwM0FidUF6Y0FEZ2dEQVdBWUdBUUdnRXZBUmFBZGNBTk53RG1nQVRpcCtyR3JwVldsUmkxVHkwMnZsb3NkdVJ4M3VKLzlWdFRKdmVxcS8zY0t1YTNZNk4zMklOZWZ4eFVOcjNua2ZWT2ZjbzRQSWM5aXN1bjc5VTNVbFJ5OHRucDZIYlg4MlAyOXU3U0cybTRMN29XdEt0UnUySHJnL25BWHVXZHIreTcvMWFIT01zZVR4bzE1MUNiNk8xclBiS0lMSytWcloydGR5QlA1V05mYW0wTE5FN3BuRDcrTm9wYUZkMC9YemZlUXp6cXZlei9qUUo2bG1jbkZDU2NhK2lRa2Q3NjhSTDJyYzg5bnh4MW91R215NCt2Y0N2TFV2RzBNTkFkUi84YXZGNS9KUEJwOTVGMnU4eTRYanRxUUt6bGRHOGZLckd0S1lwTzROQmtpcTlSTXdkeWdkcGI3TVIrTFI0Z1VKNFRUc2tZeUlrMjdnWjJPbFRpeVNpVHJvczZVL09sbjRaUEw1WFlLT1MweXRwQ1V6Qk1SVFBYVjZtMCt1RnlkVk5KUm1SRVYxNXd6R3MrSUNhZm52UG9NS0ZlZlVlUHBtUDJuUlZkNERwU1lSbm9XSmxwcFdJenhJcjBYSm9HTmFMZXJBdmFRMzRJckpmSGFabTNRbTNiSlJHYXBuUzFLQk5wVEtOaTkvMnpRYnp3SUJRQUEifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Neighborhood"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"NAmes","2":"225","3":"15.08694"},{"1":"CollgCr","2":"150","3":"21.39342"},{"1":"OldTown","2":"113","3":"17.03670"},{"1":"Edwards","2":"100","3":"15.47582"},{"1":"Somerst","2":"86","3":"35.46190"},{"1":"Gilbert","2":"79","3":"18.57588"},{"1":"NridgHt","2":"77","3":"31.42692"},{"1":"Sawyer","2":"74","3":"13.96674"},{"1":"NWAmes","2":"73","3":"16.50556"},{"1":"SawyerW","2":"59","3":"19.01490"},{"1":"BrkSide","2":"58","3":"17.50037"},{"1":"Crawfor","2":"51","3":"21.04365"},{"1":"Mitchel","2":"49","3":"16.43088"},{"1":"NoRidge","2":"41","3":"25.66816"},{"1":"Timber","2":"38","3":"18.38600"},{"1":"IDOTRR","2":"37","3":"13.17970"},{"1":"ClearCr","2":"28","3":"13.78080"},{"1":"StoneBr","2":"25","3":"36.07446"},{"1":"SWISU","2":"25","3":"18.63079"},{"1":"Blmngtn","2":"17","3":"57.64393"},{"1":"MeadowV","2":"17","3":"45.39477"},{"1":"BrDale","2":"16","3":"58.32316"},{"1":"Veenker","2":"11","3":"18.08101"},{"1":"NPkVill","2":"9","3":"49.57769"},{"1":"Blueste","2":"2","3":"86.41026"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[25]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IE5laWdoYm9yaG9vZCwgeSA9IHBzZiwgZmlsbCA9IE5laWdoYm9yaG9vZCkpICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICBjb29yZF9mbGlwKCkgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIilcbmBgYCJ9 -->

```r
ggplot(train, aes(x = Neighborhood, y = psf, fill = Neighborhood)) +
  geom_boxplot() +
  coord_flip() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzdGlvbiA6IERlZmluZXRlbHkgYSBkaWZmZXJlbnRpYXRvclxuYGBgIn0= -->

```r
# Conclustion : Definetely a differentiator
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KENvbmRpdGlvbjEpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZikpICU+JVxuICBhcnJhbmdlKGRlc2MoYXZnKSwgZGVzYyhjb3VudCkpXG5gYGAifQ== -->

```r
train %>%
  group_by(Condition1) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(avg), desc(count))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6OX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVN2eThFUVJTZTJ4KzRGU0t1MHlra0ltNzlGbmZWSENMUlhMaUtjdHdPTHRiTVpXN3ZVUEV2cU5VNm91RXYwQ2trQ0JHMUtFUkVOQ0s0OVhadjVxd3R2dG52dlgzejV2dmVUR0YyYWRSYXNoQkNHdEtOQk5KMG9JWUdTd0laS0JsOHR4SFNVMERnajk0QjM2UkVVTmtHTUFHdFlRUFlHVzVFcUNYV3BNV2xOZXBXZ0hXRnUyVTJKendxZG1Sa3psSHFDQmtZZVM0MkZWL2dsVnlFNXhVdkZISTB3dGtmejBmeWVSWVRZeFpkVWxGYW1ncFhTZEhqQWxnZG9IeUNOK05GZWd0bTBBTllsTDZIQWUyQXpxQVdUOTVrZi9ZUHMzamlMVzNlUFIvZzhlWG56OTdiYnp4bTloM2RUei9oNFhuU3ZYajZpTzNkdWVPTDh5K2N6cjczRHZpdmVQRDZKRk0vRzhMOWx6dGpEMU5YRGFtNkgxTm5PY1FqOXFvZ216UnVoa0ZPbWRGVitReG5Uc2tyY1RiUzlNeXJ6Sk9CVG1wcnNUWkp3YmRzMVNwd3IrM0I0dnYrUjJNaS80cGJlVG5vRGFWYVNqNkFxTmlFaUNXNnFpeG83YVNMNjFXMmtSN05CQkxsUzBIeXZJU2N1T0o2NDB4RFRjSlU5MFRaV29tcDZ6VmRza0pkR1hTQ2g5Q0NYUmFscGxrTHNoWGI0eDVSZFZhUnV5clR1Tzc2TDNLM3YySUhBd0FBIn0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Condition1"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"RRNn","2":"5","3":"22.82512"},{"1":"Norm","2":"1260","3":"21.93819"},{"1":"RRNe","2":"2","3":"20.35124"},{"1":"PosN","2":"19","3":"19.02011"},{"1":"RRAn","2":"26","3":"16.28664"},{"1":"Feedr","2":"81","3":"15.24859"},{"1":"PosA","2":"8","3":"14.61513"},{"1":"Artery","2":"48","3":"14.41149"},{"1":"RRAe","2":"11","3":"12.40327"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[9]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzdGlvbiA6IFBlb3BsZSBkb24ndCBsaWtlIGJ1aWxkaW5nIGFkamFjZW50IHRvIHJhaWwgcm9hZHMgb3Igc3RyZWV0cy5cbmBgYCJ9 -->

```r
# Conclustion : People don't like building adjacent to rail roads or streets.
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KENvbmRpdGlvbjIpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZikpICU+JVxuICBhcnJhbmdlKGRlc2MoYXZnKSwgZGVzYyhjb3VudCkpXG5gYGAifQ== -->

```r
train %>%
  group_by(Condition2) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(avg), desc(count))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6OH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVJ2MC9DUUJTKy9nSnBBaUdTc0xtUlNJd1V4Wmc0bU5CR2dwUEVNTEhXOXNDR2NvZlhncmc1RUhkbmRYQndNZndKR2xjM25SejAvekFtSnRRcnZRUHM4TzU5Ny9YcmUrOTdyMWxyVmRTV0NnQVFnU1FMUUpRb2xFWDZDRUFHcWRDUEFKQnlGTkF2VXByNmxaQVJ4VUNaL1JqbEJHcEphb2xZZ1lRTGg5RDFLTXJPbUN4ckVCK1NDeFlwZFFodHdnSzVnVW1QNDJQc0dVdTR3WEd6YWNBbGpCYTRnV0lES0pacmVyei9mS3EyYWZtWVVEU2xsbDVvVUI2WXBnVHpJdE1XV2liazZYdXIzK1BuKzdLK1c2aVc4NzgxWGJ0NytrcXEyL3JtMFEyNSt0alhOOFRYL0ZtaXJoYy9qVW54MXRmWDM2cVA0OG1MWGxoN3Z6N3NqcUx4cENBMmtXcWJ2cW0xaWRtRGNRR0k1cmdBaWRNUE1MSWQzOEdvTXRlSkI4aG5nV1FPTzdFeUtZTFBOVjRxVkN4ZTBpY0lncDlvQy8vSVNkd1BhMU9xbUdPSFhoNVdJTEZFZG9EQzBuYkpPaDJnYm1sbkt4eVJiUTJ3ZmdMYk1zZFMxRlBtbTFENGJTRHFPSWlmVjNITkUraXlJRU0xekNSb2ZlTE14YW8wNjJrKzlrM09VeTNzOGt4MDR1a2ZjdkFwUk9zQ0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Condition2"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"PosA","2":"1","3":"24.07407"},{"1":"Norm","2":"1445","3":"21.14159"},{"1":"PosN","2":"2","3":"15.30808"},{"1":"Feedr","2":"6","3":"14.15158"},{"1":"RRNn","2":"2","3":"13.00543"},{"1":"Artery","2":"2","3":"12.42628"},{"1":"RRAn","2":"1","3":"11.90478"},{"1":"RRAe","2":"1","3":"10.05823"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[8]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBOZWVkIHRvIG1peCBpdCB3aXRoIGNvbmRpdGlvbiAxIHRvIGdldCBiZXR0ZXIgcmVzdWx0XG5gYGAifQ== -->

```r
# Need to mix it with condition 1 to get better result
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEJsZGdUeXBlKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpKSAlPiVcbiAgYXJyYW5nZShkZXNjKGF2ZyksIGRlc2MoY291bnQpKSBcbmBgYCJ9 -->

```r
train %>%
  group_by(BldgType) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(avg), desc(count)) 
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6NX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVJ6VXJEUUJEZVpOTnFBNVpDd2F0M1N3T3RYaFNVWUZzdklvSVc2VW5ZcHRzMnV0ME4rV25yUlR6NEFJTDBSWHdEUVJBOGVQVlJQQWlOazJZMzJCeG1aK2FiYjJmbTI3MXM5NXBtejBRSTZRZ2JHdEl4aElZT2g0WU1WRXI4SENGY2hRQXFlQXQ4SVdGSXI2VTRYRjYvVkdSMFNsa0FVV1hGVEZHamNVb21pdEVjVGxxQ3E2d2RlWXpPWlZib3p2ZzRVS1ZWMHNrTktEaU1CS3AvTm5WSW5GRDRFQzNCMUs0MU1NQ01kL0Q3WUR0ZzVhUm1uNzhzUG02K251Mk8rOVkvaUJkMnMzYjk5QjJmMmZXamg5ZkQ2ckc5ZS92emVYRzFuWTdHY1c2YU9TQWhzWVkrbWREOGNod3d0UnlXNE9ZSkc0eTY5eDdORklpSWh6TEJaRHJLTlNuNVltYXBSb2tXL1JHT09JNS9VMzFyNUEzaGhhN2dRTldyVXZiL1ZUVS9CMVFpbnJRZTFKMXh4Ty9xZTQxRWoveFBKT2Rwc3BHS2NUclRVTytnZnJWSStjamxtU3hHK3BUSnBBd2FWaElzejNjenNTYWdnUldLa0NpZTZRaW1rUFR6bG44NHZjbXFtUUlBQUE9PSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BldgType"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"Twnhs","2":"43","3":"59.15301"},{"1":"TwnhsE","2":"114","3":"42.82621"},{"1":"1Fam","2":"1220","3":"18.16929"},{"1":"Duplex","2":"52","3":"14.62011"},{"1":"2fmCon","2":"31","3":"13.20892"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[5]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogU3VwZXJiIEZlYXR1cmVcbmBgYCJ9 -->

```r
# Conclusion : Superb Feature
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEhvdXNlU3R5bGUpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZikpICU+JVxuICBhcnJhbmdlKGRlc2MoYXZnKSwgZGVzYyhjb3VudCkpIFxuYGBgIn0= -->

```r
train %>%
  group_by(HouseStyle) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(avg), desc(count)) 
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6OH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0JqS0FNc3k4UUpvRGlObUFtQjBpQmxRR0VXTUZHd0xTaUdvQVcwNXFXV3BPTVpBbEFGWUpGVFhVTTNYTHpFUGloZWFsd1huQkpmbEZsVENlRVlwS0l4U1ZSaWdxZzkzeUsxT0xvRHlXWUoreUhEUzNzQ2JuSkJiRG5BSjNZRnBpTXRBVUlPc2ZFRU85eUxnWFNLc0NmWFFONmoxSElPWUdZajRnbmdXbE9Sd3N0M1J2Q3RwKzBjSGN0MkEyZzlkOUIrUDFTdzAzdEtvN0dMN1o2YVd6YjQyRFlVYnI0bGxtZHh3TUpmWXNmZWl4MDhIQVBweFpoU2ZFd1VEODg2THphemREbk1mOEg4MUZYQ21KSllsNmFVV0p1YW5vSHNnRGlzRTh3QXhUN3BGZldwd2FYRktaa3dyM1ozNXBYZ21VdzV4WWxvNW1ER2RSZnJrZXpDaVFqNWthZ01ULy8vOS9RRUlCUlRGN2ZrRkpabjRlVUNtVE1EU2VrUjNMV0lRbUlGQ2FCekk2UlRjNW96UXZXOWZZQ09SRVNNSUFBMTRvbXdPSnpReXhrd1VXRXF5d3VFbk5TOC9NZzNzckp6RXBOUWZLNFFQNkFld0Z2WUtpVExobnVZQ2l4WG9sK1NXSk1IVmN5Zms1TUJGSUZQOERBR3FZdVFYMkFnQUEifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["HouseStyle"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"2Story","2":"445","3":"25.70526"},{"1":"SFoyer","2":"37","3":"23.30250"},{"1":"1Story","2":"726","3":"19.68611"},{"1":"2.5Fin","2":"8","3":"17.92470"},{"1":"SLvl","2":"65","3":"17.40829"},{"1":"2.5Unf","2":"11","3":"17.09663"},{"1":"1.5Unf","2":"14","3":"16.24742"},{"1":"1.5Fin","2":"154","3":"16.09356"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[8]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEhvdXNlU3R5bGUsIHkgPSBwc2YsIGZpbGwgPSBIb3VzZVN0eWxlKSkgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKVxuYGBgIn0= -->

```r
ggplot(train, aes(x = HouseStyle, y = psf, fill = HouseStyle)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogMiBzdG9yeSBnZXR0aW5nIHByZW1pdW0gcHJpemVcbmBgYCJ9 -->

```r
# Conclusion : 2 story getting premium prize
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4kT3ZlcmFsbFF1YWwgPSBhcy5mYWN0b3IodHJhaW4kT3ZlcmFsbFF1YWwpXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoT3ZlcmFsbFF1YWwpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZikpICU+JVxuICBhcnJhbmdlKGRlc2MoYXZnKSwgZGVzYyhjb3VudCkpIFxuYGBgIn0= -->

```r
train$OverallQual = as.factor(train$OverallQual)
train %>%
  group_by(OverallQual) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(avg), desc(count)) 
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6MTB9LCJyZGYiOiJINHNJQUFBQUFBQUFCZ3R5aVREaWl1QmlZR0JnWW1CbVlXUmdZZ1l5V1ppQUJDTURDd01uaUs1Z1lHQVdCaktBTXN5OFFCcWtHQ1RCQVdXekF6RWJTQmNRczBMVUFUV0RERVExaUMwbnRTdzFweGpJRWdEcmhCcHZDR01Zd1JqR01JWUpqR0VLWTVqQkdPWXdoZ1dNWVFsbE1Ca2FvRm5NbXB5VFdBeXpGKzZhdE1Ua2t2d2lJT3NmRU1QOHBRM0VLNEJZQ0tqUUhvakxnT3dTSU4wTHBFVWdmZ0w3ancrazNzRk9VOUg4eGN0TkRqYkcyK3V6Zm5rNzJBam9kL2orLytsZzhmcHcxWi9GT2c2bWZBN3lpckh2SEF4RVh1WWZaemR3MEo5d3FqT3dxdHBCWFZsc3p6YzJEUWZwcDU3Vyt5SnJIS1F2YjM2ci9Lb0w0bXptLzJndTVVcEpMRW5VU3l0S3pFMUY5MWdlVUF6bU1XYW9JTGQvV1dwUllrNU9ZR2xpRGp3QThrdnpTcUFjNXNTeWREUnpPSXZ5eS9WZ1pvR0NncWtCU1B6Ly8vOGJKSGhRRkxQbkY1Ums1dWNCbFRJSlEyTWMyYldNUldnQ0FxVjVJS05UZEpNelN2T3lkWTFOb0VFTlNpSU1VUHNZb1dJd05qUEVUaFpZVUxEQ0lpMDFMejB6THhYbXJaekVwRlNZSC9tQWZnQjdRYStnS0JQdVdTNmdhTEZlU1g0SlBDeTRrdk56WUNLUXVQOEhBRm4yZS9BRUF3QUEifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["OverallQual"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"9","2":"43","3":"30.160663"},{"1":"8","2":"168","3":"28.202019"},{"1":"10","2":"18","3":"28.063225"},{"1":"7","2":"319","3":"24.920952"},{"1":"6","2":"374","3":"21.055666"},{"1":"4","2":"116","3":"16.081687"},{"1":"5","2":"397","3":"15.782795"},{"1":"3","2":"20","3":"11.568533"},{"1":"1","2":"2","3":"6.973912"},{"1":"2","2":"3","3":"6.956741"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[10]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KE92ZXJhbGxRdWFsKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpKSAlPiVcbiAgZ2dwbG90KGFlcyh4ID0gT3ZlcmFsbFF1YWwsIHkgPSBjb3VudCwgZmlsbCA9IE92ZXJhbGxRdWFsKSkgK1xuICAgIGdlb21fYmFyKHN0YXQgPSBcImlkZW50aXR5XCIpICtcbiAgICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIilcbmBgYCJ9 -->

```r
train %>%
  group_by(OverallQual) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  ggplot(aes(x = OverallQual, y = count, fill = OverallQual)) +
    geom_bar(stat = "identity") +
    theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdncGxvdChhZXMoeCA9IE92ZXJhbGxRdWFsLCB5ID0gcHNmLCBmaWxsID0gT3ZlcmFsbFF1YWwpKSArXG4gICAgZ2VvbV9ib3hwbG90KCkgK1xuICAgIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKVxuYGBgIn0= -->

```r
train %>%
  ggplot(aes(x = OverallQual, y = psf, fill = OverallQual)) +
    geom_boxplot() +
    theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBEZWZpbmV0bHkgYSBkZWNpZGVyLiBQb3NzaWJhbHkgbW9zdCBpbXBvcnRhbnQgZmVhdHVyZVxuYGBgIn0= -->

```r
# Definetly a decider. Possibaly most important feature
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4kT3ZlcmFsbENvbmQgPSBhcy5mYWN0b3IodHJhaW4kT3ZlcmFsbENvbmQpXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoT3ZlcmFsbENvbmQpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZikpICU+JVxuICBhcnJhbmdlKGRlc2MoYXZnKSwgZGVzYyhjb3VudCkpIFxuYGBgIn0= -->

```r
train$OverallCond = as.factor(train$OverallCond)
train %>%
  group_by(OverallCond) %>%
  summarise(count = n(),
            avg = mean(psf)) %>%
  arrange(desc(avg), desc(count)) 
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6MywibnJvdyI6OX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVN2VTRDUVJCZWJrSGtqQVFsZ3NZMzBIQUpmNEtWbTJoaFl6UldhTGNlQjE0ODc4aHhvQjFVTlA0VUZzYkdhTUlUNkJzWWJYa0EzOENZYUtHRmpRSG51QjBpVjh6T3QzTXozOHczZTdzYnBZeGNrZ2toRXFIQkFKRW93S0FFUjRBRVNjVDFwNFRRT0FENFFxZkJ1OEdROEpOZ0UyRGhJUUZVZW5sUVBFNHlZV2hOemFnRGlnMHJCWFVhUVFaQkZrRU9RUjdCQ29JQ2dpS0NWVis3a0dyd09uWWJ6VkRocW1QWmdQcGdRZ25OZzArQWJZTDlndldFT3FBa0M1NFNFblZ6V2VIaG83di8xbWE1dVU0M3pHZFlialpCVytkSmx0bTZXWHpSbjFqNnJwWDgrbjVrU3JxWHYxQXYyZkt0SG45KzMyRkx4YXZYcytzMU5yLzNlVzgzT3Q2b2RPQ2JUaTV6aHlzVm14OXJmakVteEZBTUZjR3A3YVptYzhOWXQ4enlTTFRWTUIxeG9ieFo5ZkZFYk90RVFTNVh2dFNHWXpBWS9IZ3JHVXNPV3pWSHQweElsZUppSS8rbkRkaStRS3hodXRUbGxIcllNSTlTMllJclNheVBpSDRCOGRNZ3BsN1BJSzRpaEErbG1WWGQxRkNXd1E4MFExeWlvR0VvUWFuWitraXNETkc2NGxnT3h6eFp0UXlNZU8vZC93TWhHTjdHNmdJQUFBPT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["OverallCond"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"5","2":"821","3":"23.695032"},{"1":"9","2":"22","3":"20.084086"},{"1":"8","2":"72","3":"20.070648"},{"1":"6","2":"252","3":"18.303102"},{"1":"7","2":"205","3":"17.623033"},{"1":"2","2":"5","3":"15.097269"},{"1":"4","2":"57","3":"13.807442"},{"1":"3","2":"25","3":"13.110495"},{"1":"1","2":"1","3":"6.087824"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[9]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4kT3ZlcmFsbENvbmQgPSBhcy5mYWN0b3IodHJhaW4kT3ZlcmFsbENvbmQpXG50cmFpbiAlPiVcbiAgZ2dwbG90KGFlcyh4ID0gT3ZlcmFsbENvbmQsIHkgPSBwc2YsIGZpbGwgPSBPdmVyYWxsQ29uZCkpICtcbiAgICBnZW9tX2JveHBsb3QoKSArXG4gICAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpXG5gYGAifQ== -->

```r
train$OverallCond = as.factor(train$OverallCond)
train %>%
  ggplot(aes(x = OverallCond, y = psf, fill = OverallCond)) +
    geom_boxplot() +
    theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI0NvbmNsdXNpb24gOiBOb3QgcXVpdGUgaW1wcmVzc2l2ZS5cbmBgYCJ9 -->

```r
#Conclusion : Not quite impressive.
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBBZ2FpbiBpbnRlcmVzdGluZyBmZWF0dXJlIDogWWVhckJ1aWx0OiBPcmlnaW5hbCBjb25zdHJ1Y3Rpb24gZGF0ZVxudHJhaW4gJT4lXG4gIGdncGxvdChhZXMoeCA9IFllYXJCdWlsdCkpICtcbiAgZ2VvbV9oaXN0b2dyYW0oYmlud2lkdGggPSA1KVxuYGBgIn0= -->

```r
# Again interesting feature : YearBuilt: Original construction date
train %>%
  ggplot(aes(x = YearBuilt)) +
  geom_histogram(binwidth = 5)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubWF4KHRyYWluJFllYXJCdWlsdClcbmBgYCJ9 -->

```r
max(train$YearBuilt)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIDIwMTBcbiJ9 -->

```
[1] 2010
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdncGxvdChhZXMoeCA9IFllYXJCdWlsdCwgeSA9IHBzZikpICtcbiAgICBnZW9tX2ppdHRlcihjb2xvciA9IFwicmVkXCIsIGFscGhhID0gMC4zKSArXG4gICAgZ2VvbV9zbW9vdGgobWV0aG9kID0gXCJsbVwiKVxuYGBgIn0= -->

```r
train %>%
  ggplot(aes(x = YearBuilt, y = psf)) +
    geom_jitter(color = "red", alpha = 0.3) +
    geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArwAAAGwCAMAAAB8TkaXAAABDlBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZrYzZv86AAA6ADo6AGY6OgA6Ojo6OmY6ZmY6ZpA6ZrY6kLY6kNtmAABmADpmOgBmOjpmZjpmZpBmkLZmkNtmtttmtv+QOgCQZgCQZjqQZmaQtraQ2/+2ZgC2Zjq2kDq2tpC2tra2ttu229u22/+2/7a2///WPj7WPz/WQEDWQUHWQ0PWRkbWSkrWT0/WV1fWYmLWcXHWiIjWqKjW1tbbkDrbkGbbtmbbtpDbtrbb27bb29vb2//b/9vb////AQH/AgL/AwP/BQX/Bwf/Cgr/Dw//FRX/Hh7/Kyv/PT3/V1f/fHz/srL/tmb/25D/27b/29v//7b//9v///9/qAJaAAAACXBIWXMAAA7DAAAOwwHHb6hkAAAgAElEQVR4nO2dC4PbuHbfZe+1d/beTTf1dNOmsdvU0zbJdtOuPaOHPUma22vPSCQBkJq5Gev7f5Hi4EECIPgAHxI5Ov9715ZnJBKSfjw8OA9gcUChZqrFqQeAQnUVwouarRBe1GyF8KJmqxB4H3//K/z1sFi8eG89QKFOoQB4ny5fArwPHFj4r3iAQp1E7eHldhbg/fbuDf/H1eviAQp1GrWG92Hx5gHgfbx4y/91+/LX/MF4g0Oh6hTi80p4f3gvH+YPxGFAowwQhapSMLzSy+V/5g+6HAqF6i+EFzVbDeQ2hB4KheqvcHgrJ2wIL+q4Coa3OlSG8KKOq2B4q5MUCC/quAqH93Crs8K3dnoY4UUdVwMSh/CijiuEFzVbIbyo2QrhRc1WCC9qtkJ4UbMVwouqUJZlpx5CgxBelF/Zfr+fOL0IL8ovhBc1WyG8qPkKfV4UajQhvKjZCuFFzVYIL2q2QnhRsxXCi5qtEF7UbIXwomYrhBc1WyG8qNkK4UXNVggvarZCeFGzFcKLmq0QXtRshfCiZiuEFzVbIbyo2QrhRc1WCC9qtkJ4UbMVwouarRBe1GyF8KJmK4QXNVshvKjZCuFFzVYIL2q2QnhRsxXCi5qtEF7UbIXwomYrhBc1WyG8qNkK4UXNVggvarZCeFHH08B7tCC8qKOJpemgu2MhvKhjKUsz/v8BD4jwoo4lhBc1W2X7NGVDHhDhRR1NQ++pifCiZiuEFzVbIbyo2QrhRc1WCC9qtkJ4UbMVwouarRBe1GyF8KJmK4QXdUQNm2NDeFHHU7bfD1kTifCijieEFzVHCYcB4UXNUApb9HlR89PANlcK4UUdQwgvar4auhAdhPCiKjQGbsMK4UX5NcqNflghvCi/EF7UbIXwouarsX3e/sdHeFGn0QCWPZi4h4XU28PTJfz9uvuhUOesU8Ar9HTJmX384f0Ah0KdqU4G7+3LX7kNhj96Hwp1rjqRz/t48Yb/efva/inCizquOhF3JWzu1Y/c5X2jDgMacFgoVLO6EPd0+Ub8+eoLJ/hNr0OhUN3VhbiHF8VMzXB8EV5UjUYIG3ch7gpMrtLjxds+h0Kdi8ZI2HUgTnoNSka8DOFFVWsi8CpjK/9CtwHVSmV4TxIq0y7vFYTKcMKGaieX1dMkKW61sb0SWeI+h0Kdr06WYRv7UKjnL4QXNV9hSSRqzurJL8KLOpn6eg4I7/nq5O3BCC+qo07fpCZG0OMSQnjPVqeHF2x/n1EgvGerjFJ6+vZgE95QI4zwnq0Y6NSDMOENNsII79mKcUN3engNc4vwotpqIvAWQnhRrTUFr8ES+ryosxHCi5qtEF7UbIXwomYrhBc1WyG8qNkK4UUVOmKd2RCnQnhRuY5YqpOladr7VAjvecpr+I4I7yDpPYT3LOXH9HTwdnMiEN6zVAWmx/N5bbeh41WD8J6ljl+IXlpzxPw3wosK0LH71+rxRHhR/TQqz9k+TWsmaOjzovqoTz9Oi6OnWdY/NuYI4UVJ9enHaSGWplNY4vQIh0IdXyPD2+A3dBLCi1IqfIUxrOQYB0V4z1G1catRjOQo5hzhPUO5HDn/HicIjPCiBlDG0hPAO0IIA+E9O3GvIEvr4D1SBgPX50UFi6OasqH3Nuk0DFwZHRWoky2w504LEd4RdPJ1a0fWid7f8J41wlvSBJb+fJYa3rNGeEtCeMfR8J8rwlsSwjuSBndXEN6ynrvPO0FhSSRqjgJusRgdNWn5+5UzJjZVQXhR7XQSt8jLJ+RLuBjCi2qncVsmnHPVr9kP8FJosUCfF9VKdtW5myke8VR+eGPauc4X4T07WUS5NTqjnarC52VpjxEgvOcn815+PHgrn9Hd9iO8Z61Sae/Qx2/yZXtlhBDeM9epMzJ9zo/woo4ppyyy35WD8KKOKNtLqNj1vTXSCC/qiCrDy0pOb3s3GOFFHVEIL2o4HX21SNfnLa/vj/CiKmXyc/raZc/mFOjzoiqUL7vUoxZxQPUZAcJ7ZsrXGs161CIOOR6EF9VWNrwnz1H08roR3jNTvore6Y2uEGbYUO2V03J6o3vA2gbUjIXwomYnbfYRXlSoTrKyXim+LIJ16POiQjR2Fa//pKaNHSZOh/Cen8bun6g6K8KL6q0JwDtMeg/hPT+JvjF29Iqc8hn7et4I7xkKirmOnKIY5XwI7/kpA7OL8I51KNSIEtUNZIx9AutOivCiBhDAS9Mx9gmsPesIPrZL3Ld3L3/99n///ssAh0JNUxLeSVTl9JRL3NPly1/hvwEOhZqouM9b7hw7yUA8EYgQlS3v4qf/efHiv/2dUJAFRnhnpCmUlPWON5eIe7hYFAqywAgvKkjDw3v49sd/vXz5D38U+n+eVzxdAtav+aOHxeLF+7pDoSarLOu4Ju6QYxgeXo7v3/6nGnfh8QcF7AMn98GgF+Gdj8SS5Cd3e6XP230FqHDiHpQv8e3dG/7n1eseh0KdStOAV0hFgBW0QfHgauL+5a9++sX381uF6+PFW/hX4RYjvPPR5ODV0PaHF4K93KG1PNpcVz/y37zR7sMDwjtLTcHnlQJcCSODwXu1ePWnd4s3D4vX5d89Xb7iDvHVG+XuKqdXxCa6DR51Hqq8VrIsZozRfbEUSlt5J2zvXrx/vHjxviZZwQ2uBW/VoVAoqZr1+yFZzUiH+4CPOID2YVGbaeMOL7oNqADVxMUEvF0qLargveUuw+PFq6qQGScXJ2yoANXBu6eUiELNwGNW+Lx/cbF4y//y+LySWW5wMVSGClFN16foCdLLUAWoItqwWPwlN8C/83kNAlc+YcMkBSpMtXOxweA9HP7tC+SJ/b+7WiwWYH0Pt5gefn4aMoDWdCz5e/XncPB2EcL7DDRkx0PTsaz0RMYIC42VVRD3L//xxx9/+oegoSK8z0Ejw2uRacKbPzdkAJU+74sL7vcGNVQgvM9A48Lr2clK7qqSscHgvVq8+uVw+PM7yAK3F8L7HDSqz+uQqX1eZlRa9IX36VLOw2rivG0PhUIZqiBTGt/wZYOrkhTm3z0OhXqW6mye3Rcq29txhwG/24CWF1WjwRzjvBCy2zIoFRO23/0i/gxqIkZ4z0XDwqsWn+rQ0Ox1G/7qx8Xiuz+ENmEivOeiig2vux2IGf8NA6+hv0B4UY4GW6nPtLoD+bzdhPCek0LgrS9q6G7GEV5UJwXA2/DU7v4HwovqpgbmjF83ct4VX4T3/HSMzksT2HYFOh2E8J6djrKutL19SuZ72H9ACO/ZqZqVAU1yTSK49GOEF9VWeVqroWym51m8F4L/FIwQhBfVSmZBQdDEaoBTey1vhyYKIYT3XKWqYdI0bTuxGuSsPp8X4UWFSaLKOE35kgktfN4xIhU5vKErpSO8ZyvBoQVvi9eMYJwz2GZAOjKwtEMAvwjvect0G9o8fXh4i0MKeEMWr0R4z1whfkCWjbARSzFxRHhRo8nq1ul8EE+ALoVS9BT+ZEGXB8KLaquSz9Bh9uZrh4d1oFjKGJUdmO3XLEN4UW3lgtfFAa6EN18pMuCoCO/UNJEFy31yhjYMvGr5SMINLsI7c42fKRjs6ug0VHvNnCzTq07nYQ+Ed74aHd4BT9D3MhBDYWr/+fxg7Y+K8E5Mc4K3r2T7Wvf95xHeqWlsn3dy8JZa2Fp/Agjv2Wk6M0K91gizVsxpf3UhvGetk4Kcr/IkG4jD14lEeM9Zp3Uh1NmZ3EEQ4UUFaQrwQl0byYzlpdHnRVWrgOPEkze7KBNXzEE1yupKP/3kLbCi2BTCe3Y6rrltvjxYp90vQQjv2emo8BptnhUY9zD+CO/56Zi+grFpSsBKDi2F8KJCFdR8ke/10wbeQA8C4Z2SJjB/alaYrcz3+iGpd99s82ihczeEdywN02YwQYWOUhvfigIc43NCeCeigdoMJqg2ozSvXGeLy4pngSS8WBJ5cj1feFvQ5ex0Cc/39f+UfgQ+Lxajn1792wxOomFG0MbMHioW9FedFW2E8I6l04PYQQPZ/lKrZuWSkcWew3kjhexpa3MahBdlqB+8RtGEXV1eMVkzNhUyTiy6iRFeVKh6wVv54splIDNGUg1vwXfrQSC8KCU5r+rh7Dg+rPGoAl74OWWyHl08Rb2k7SAQXpRUf3fXTgJb2Qd/goJxctNMNxHTlAQOAeFFSQXM8isPYW6MaXqx/nV3s5Tx/yl4hRVOheluvR4awouSCpjl1x6lDG/V5irc2CZxHgLm1hmyyCxgGAgvSqlxlt/GFTWWyVNbX1RtU8wvFsYYJbpYUq1BGXINIbworaZtVtukhUsLSbr1ZLlXwH9DE45vatf7IrwBmmIu4URjalhctDO8ZhatYBN8bMoISfPCB22q0edtqT5z7LEYq4rpjyyToOrf+35RsxtWeVlUDS9svkYYSSmHWyxyylJftrhOCG9neEcro+m8tVPP01qrJ/ieoJ1Yz+vs55ReZDw5ZRTenKggy1JufPVy/mI3laDPFOFFePVpxcr6TW/Kt8BuUHE6LCPNDTwRi/jrasmUxTThBJOAHSkQ3h73/vEKGCti+mMLTtto+vrCqw08TWExadH3A1dNzE+ekDQsWnf28PbQePOq08zY/CWKvic5PwoarfZOKGH6KmXgPTBGQvMkCC9Kq50J7X1hyeXQYU6a1zZwq1t4Ee2F8I6lKcbgGjTIkNsdBEoZoLCBET59g/0oYmiiIAS7h6egvFC17rucIeBNamk9xaSU7WkUZ1mcxAS2sQqeqCK8fVW1EIxaKqbuu5xYz9owhte5aKs+HrHvWpxsKSFRQhKAVxSZhexSiPD2VBWA/eE9tlmuKEHwjKJuZM77rlzVT7oKaRLtdl8ZSeIDiyNC44gGXM8Ib0815J3C4C13jB9R3hN6Wykbr7lik2KzMNJKZkC4l3sL9D5JoogTTAhlu/tdzAJiZQhvd1W1dJef1PKX9tc7U3jlEyhNffDqohwGEd00SenujqbxXZLQiCZsl1BKEN5jSN8g2++V2/KInn8cRV4PoRu8aUZVeUbRXJTJZZ8yVeCQEpLShGNLsh0jacQf3u0oxMxaDxjh7aw2Xm2nI+p/TSIUEerzit8LOJl7HebORFHMwGmmBPITSRRHUcL/xuWejqLh4Z0Ir/0l3YJipqbL5PKPLOXIirSaLG5ItveR6KRIV5+F2p0G4e2uFlOys5Vqy1AfUR7AVVcnpIXB4KqFybjBJR9X6/X606cNwntUtTCXz8WiBkjUKeiYg7G/cD7LjQkRVTn832R5s/ztw8fVZqPYRXino/MxzsbaDxmhaZpaAbN8ygZ+w12SiGX11subm5vlh//9282So/u9VLuzIbwt1SeocDbwimiY6uPMe9nFL6TyeANLI/Lx5sPm82Z9s7y5vr7+8L2ldqc7e3hb3tFb593bxpumpwF8G0GnmqoJeEnRSyw7MQFebmA3n65X18vfuJ9wbVPLad7w/7c7XThx394tFos3/MHTJX+weN3jUBNQW67awts+x1pzjNNV89b8unZQep0mE17uGhi5Xjj8ZrNarYRfu/m0XNrUfvzHDx9vVp/HhffbuxfvD7fA7OMP7/sdagpqDy8Uklg/qVy2s2+962nsdEPSt91v5Q4UrHgsf8xxXa3XnzabTxBPsKldfvjH366vbz78n+vl6maThfhnwcQ9Xrzlf96+/PXwwP/rdagpqDUpjFLL8lYtA3Pe8B6sizrb57EvMLU3NrXcwi5X1+ub3377+OHDmuyiJAnqYOtM3AOY39f2z2YJb7vb4aH87VVWk/W+5x8NXreyorYKoxFeq5ZRRbx07Mvxa1dLoZs1n6vdJCSO73e7mIJ5cA7ToI7EXXGre/Wjcn77HWrKMstKwJkTD3L3bizEjuTzhrV5Nl3kTDbAbSxqN46tlT/PoKAsTukWChtInPBH2ygSKTYdjWinbsQ9cGifLl994RRLemHqdh7wGu5dOGJTSlYM3GAP7uzqk3ITHGi/5z/6eHOzUXULGaWUW1oS0TiBZUdIfA9lvXx6xwyXuYU6EfdQxBgMx/fI8B4DBE81aqsW2+bDnV5Dwas9BAmvQ62C2Z7wArxxRLjZjWIoymEkSRKo5dU1O20/pC7EPRjOgpy/dT5Udw0OghfIss9bWjmu5tWlo1VM8k4UGuu5qNRnSza0N3wqtlyv18aNyyhvYNxfYPE2ZlFMCFToJMk2JiwRn2/rHSk6EXdrOrpGvGze8DYXqRZNWZ6FN6RT0YBhRRD4RPa48zVTR+1qvVmtrtdxsiUsS6HXR66bVxSW8U+K21qyE81rjLu8UZLu+d/cHGfVC6J6FU7c7ULaWmlz27oNg1uXo8OrnubvnlB7Nzb1x/ite22n0IS85IMX18KtBUE3O0u4MxtxeGmqcxYaYfF3tttF3OamjOPKPQaySwj/m1vgTNiA9m+5Q5xX290rcHyvCitcd6gRrMvAX6szwoaeYPe3fKbBSHC3ZXNN5US85BbUqmdyCwvdEbDymNhjQsKrNs2Gd0M4v1tCYz5ji6OEJrvt169fE8r9YJKFbj4cDO+tCCwsXnBv4Yr//bb4TS94T29hrBFULTxUGd2lDAxHGLwtlnY4daW7l1rtMMh8mXsWbk/BpYVOCp0tTmkmetphpgY16Nzucssb7wijcfx1e3f/dbdL9tLDGBXebodqbFOchoXJVZr0+qK7Jg0yaNrYE+5eIU1vutPn0idxrV9bS62ytcURxXp58tWw/COjUMsrFzsHIpkqMNtRbo2zLOa+QhSnfM5GIsIN793d12gbRZChGNlt6HioTlOZo6jCD7Xh9UV3Q9sljclI+x6M2suh1rVp+WP7QHlCt5Za53VyuVJ5ilQs40TseRes7RRzLrmXEEOzJbSq8U8YQg135Ov2672GNxt7wjbKoU4Hb9VXbUdsfHGlynZJD1T5nFuVuqqER6ca4Uyvfl/lwlTBWxUaEy/QnkArap2Xy+VKD3JDH7V4tLzRMKiJhDMTML4JJduIz+eI8BrILo5plETc5+VeQ6SXG5kfvKfzeStjr1aS3RfRl6+0HYGKlRx0L7j6lXbtujkF8rT7ykxqVVUm8aeDle/qTMM2n/Kamkpq1XGZhldU8FJoq8zkNhNMbrQmQ+Mc4H2U3HOco4Rst0lCEo50RCMSJ/H93U6sFxn2oUwF3pPJTKLV7K3gKwTIssznO3hMHP8RBOM16oxJJ3EceKvq4d3nqwoEl9qNMRlr7iWTx6VEvh0OKMzJ9FWtdgkEg0xScIP5JC0m2Y7QiFvdXQpOxP0O+GVxknq+hgadPbzFZ2XV9blYVYYZPPCWrTS/s4JJyn3AQeD1FGBVf+8mvC0mY58rihxLZzPHoSJhWZxSnZAQtnefJhFNOKRpTDm2sH1VdJ9wN5cl3BuGn8HCDR0+ipnCO4aXUQ9vhXvqm7Ux/eWZL08glqb/5VSoBY4zK8fX7Bmgz+kGyPwFimW/NtOBgtr7uPRqnfAL9x9IJHdlFW8b5nIC0GTHKNkRcdVyCxztopgbXApdmGyXEEY7uP/zhHeU+Z0Vy3JrXStPaDnH8htX+0E7Bzd8icZMXPjQxdH1fNAtPc42n0UDjkOt9muF92AdTXwQYlUQvw9vvAv3g+KzMX6hUuMVTNQyJPeE+wfKOZafERTjEJak4CbTLvseI7zGUavjNNqmMmY/3xqLsDsiWmR9eeaTff/wn6pdpY++1KSnUoZXuK/rdUVOrPQGWDHX2u8pIzTZZ0HwZiTizj21w4wpJQRywBDbFVE1eCG/NKI4jmB9XthHhWalu1WzEN5WB5Y/txNAuZOgvim1Ahe4t81VfbXeaQ0x/tFqN1vTmC+bZFOr4gc1RxGr7Gt4Ccc3LV2y9ntw4oVQr8BkuCG/J4G7TfiBoyjh9we1PzZQH9Mk3nIzHUExBNTpkEDrO094R4usVTIjfN4SvJDzLGr91PJx/Jlil5COXTXV8JaOaKS40lS5PEDnyrW1m5tPn9brT/5C5NxT5tSBHyo2mII3l8QJSRuuIxdewjFU2TZrr0txfSXcQUiYXs2Bw0vju13MyeX/bUkcx4EFxjOFdzRVzqzhS4IKPxNeuWejdmblvwksFMNq8TzU/1YHi4sm3GKBLzeIkR+FsdWG8+n6teDNbtZL2GbSn71Sc7ODuLuLnAGfWYHl5W+VQJ24M5F1nR8HXgougvnxCN9ZXN4qg0Eg/qDeYXLPgd2ShPPO7nJ4MVQWqqbtmuWtlFJi/kxsmWvGicHnzZctqMvGNnsFsFqSPI5a69abJ9G2duP2MHAPgcO8WUPlDKHaBa+LAPKxx9touwUzKMNqukjZeId2bEVsR2V9bIwmlOW/lvuxphRsugzW8dsSPNYfAVTmRDuyTWI+m0sikjUZelsIrzJ0RS1DESQyn7X3NFCUa20OmZqi18Unyq/yPUu7saLGJWXagBnPALO6Wq0casGxFfGDzaflihpxZwlMMat3DCenivsJSQR9ZdIt1fM/Zi17k7kjNMRIUvxMFomJvd1TlaDhb4KfRG6UDQk/Fu22MZwVgmk0FvNFhLf9zSfPiml4uZ3y5a685pIQ4jxNVaVnhc9bJEGMWH7z2Gx4ZVm38k+Eqd2sSrYWFgldr5cfV9Chq/JbNPfKVbFBvrV6pub8uVWNkoTEsDEPy9fNdbPdFfDqd0Yg2WD7NsK+GukzODZ3faE4Eswwdxm4z5BCsQNjFSaiWs8V3tbXrwsvTIcT3/oBHoPsKT+VvQC+77v8oGFcum8GihJSMaKNL4Tw/c2Gz8fWa/4X14qSlBMoXXR+D6d77ZUbmTnjURF95tMpyojIhqXmdNNNQxhvPzX3ncjEHinE3c0nE56UTrllYIQhI8EncXQPPjVNUuimiIio/ZhmSeSxFQivMS2S8JaMb8FekeDyweumnTzMtvt2DIvNNivPOknfc2KvlzcfuaW9WS+vJTWMEggSEO6e76ia2OsJWZrqepn8keJaWFjo75X9kJULVLgZCeMZ/A/KsWckK8V+oblCzwPAhyDgPEAXUMrdhTTJ0mSXcK+X0ay4b7XS2cPrflTQ0APOl2tv8oCSEcnSNQru4Rosrz+J55UqkXEDX6uP6+Wn1Wa1XH388AGYY0m0E9Xw3IzdJRCvAueSJEQFDg4imqCmSpAnIMJUMiqcCn3zScEdje01dc1x5mlt5y1LeIUXQPJ/G6/KGFMLR0K4ASw8lOskMbSwxQQiFCm/1PiVU7pv1eu5wts9Esy/AsfzsqypCW8mOl7L57MKIVyf1zlQReKtongGZmLc0N7AEh6fIRcrVnBm2TbecW8T/FtGvkbcoMFiCHwSz/JIVZ6Fg9t7ImCC/C+ENIqcHqxfsyXUhtf8aJyLVdl0UcFgOAfO58cNrfTJhGEVBHNXiELrVCZKJqHrbQcQM/e+Va9nC2+TauB2wwEWZha8xeS9clpTOp0Fr5XJNWtoHVv7WdeK82esaJSIFfHBxYFbNQd2l1AwvXvRcLON45RkfCbPp0HGzE/8DU4Bn5fBbmfgJwjvPq+7zxK2294lkaydyR2nfOzgfFuxQnO+AHPBVAVaoHbX3HRN/UIsVpjJ+jbhniUiTi7mbqoLUGbYzx3eBstbmyVwfucE4oVZdQNs5h3Vc2xPrJRPU+QtMq/59hSFf/5crFanusbg207kyZick/F/3++2hKjwAZTH8qkX+8rp3TIFLZhVmBuBnSPSx8gE9jCfgsZd+Sbiu69QnCA9/9J1WVhesyoi26tajrz7RKaAU8Fsga4eyV5HkTPIRObpYtUFuA9Ya2+m8DaHSRsu3/qcp3N0Y45mT7wYTLDlPM+Yu9XDq+Jo3CFdXm8MY1uiVi9Wt9EdurKkhelFm0XUVHz3bEe2u50KIjA5JdozGkWwtdkhE7MwqBcCd5PDy136WCRsxQpMRriWe8zkPoqYhJdm7tiLUk7laMiZX6pLIM2bisjXMGFUaaqLHNT0ULwN2dkBnjhRA68rYfNqGvCGOqgtElRt4a3MB1cVEuROhJrhZPlCMP6Akmc4kPy6uV4tl2LZxLKtLeywhY40SspiyZszQEnp/XYXxfAvOTFj8TYByKNoC5U1whuF8cGUCKJZYsZ0yDue4afy4mRsF++iCHK5Xnjz+LUFr6hfJiL6UsTOROM7hctD/LG3k45yDWowuGLBC+BWH3J28AaNuN0LGtfv9ASCal+v07WSIab9S2rbourzCH1WpnSzXn68XlVQq+sV3W9TP2JixpO7A4xyq5vcizpEUdAIxTEMVvxICSx6qyoOwdflP+VXG3dYIhl3kHtJKZaB8SS65/4wHEUU09hvwYik2GPLHYGizIPJrh/ogocwrnYniuleJlPFmbhKmDHDC7FjzxTe1qvIVRyplPos7o0iayBIoeA1NARv5fG1JYUNGUplCBuHWntkhUnX08MMnIV9XvLO778xt7GJrMcE5xHqvMWevowAl+AcgFlmROzbx4j0UVXtAaQNIGIGd3kCrekk9ng9xS3dmL3mPq5enbfgTx0cXJVYrOPgWlW4hYhJHczTxPMCV0UHzRPexuuzfY5CmLHSUz3wiuqS/DFL1edePxAjgsAfOYWK6/XScHrLQ5MSBSvyBzK3y+/EkI7S0yTG3ed7GtFYZ1ZE8SGRt31yfxeTbUwEXUSu+cESAX8mXdK9XM5GVM0AvEmaUDeaayWYjTtBMdNjqWWPU5IWEQia5j6v4fjD565mmHuSic6pUHanAe/w5bm+OZOv3gZCtc5OCDqOYFtus9xbeZ211t3yXN3UGEC7vlkpeGsmjkAcLHOQ215ow6Us4cYyzgNTUIUbZbJ2R5aBwQ1bwMtIvL3bEeH47imsm8AgmMtSiAnv4Z+QPubPFp3p2Q660KHbjlklG5nMZbiRabOSWd0T9LwMLL0oxRCnTW2/R3wPhacgL1ASskq71vHh7Qdq21eXUl+Zv1ccvigrHa+CvOXShqLkye4Yc2S7rg61sHrNMNMAABIQSURBVEuTqKlZr1erTf3afKoSiMSwHbqe7TMWQU8CdInlVXCArKJLJtHgZ1AaxrLdfRR9/UpFngLmZQTSFpz9JEoopLiIsLIiawubpsHcD9rN1AwuHwWUBiUQQBOOcJ4hNOE14lsqgCjr44vUxSG3CzLOWxQSZ4RPKKIOiwUfHd5wF6HLq8vPq4AXbq+JC68vTM4dSF29qyO9MlPg4KoCXL7JmKgWhwdydITEpToA+x2Ie328i2OivljoBYOmceHgKlsnLj4iGpbzzk+5rfqeJvcJn82lCl5uVClEHPZ7YJaIWK6Cdy8yXqKekyWiW0eNQt7dU/Bcs1gc3gj7Fg1Q1mcrNm7VhWmltaLFk+1uVD6VjEm57a9Rc4PXn10vydt1UGF5RS2JNT4rN6zqdWDmI2qr86KsVJR6O6oKfEl4zdldtueGsPrNZOoygXLtWBtCjlh8BzvnxLpSfQ8FWnEmw1V2wBVCVTuZdJBpsAhWHk1l9xgFD4I7H9qNhZCxgpdyP0PHrPW8StRDJPn6N0b0QT2w0+kQiVafdun7VnbeTOnQhKnqhzBNA97WrkTLNTArug488VdWnp1k1vej5/wcIpKqleA+6T6F9aqg16XWTPbq0Zu+TCZLA6vegZ4CWb3IsODBfQwIStOVQa4XSrS4+YWMmX5qJrdcpzAFS/nNHhZvThJIx8k+JiLghRBs7nbyA+Vx4GL7CFmNkIn2vTK85njt9Lh2DA6e71aE94pN7aDyIWFJ+50oCk3C521vjVta3raRsmxfsQyvDsZri8IgdErISnYoaHiX3Pa6XWNmdEHvJuJ9m7XwqoGJPIhxZxDV27DKF5UxXZh+7aBUQcRUaZGIJTEVSSx+M+aTMz5VI6JYB/wGWXkLUySzi4dP+wisr0/E0j55t1NRegQhNhldcCuNlCtr1YI07Ehl2CBlplnI/mtak4g2BMDb7pndXWPrV0ybELbe3Hy8XqutmqRbW5EaKyoRiryu/2xwNSTV8EqDL6L4RRtOKlafoYlY7xYaEGTfDvcMIqpTbCJDTEheQSvghQafiMJiTLL5PCERM7f0hBqfmMmYWT5hyzJWkzi0U46m5Nz2YLzOfWlx2GbSqzUzeBvrbZprZa2PtfrE4DXzbxKqZqFtfL1cFvuMOba25Pj6oraes+VJu/LQ9LfL5DxK34JFUJSTKsq2gF1CIQ/B0YRKHGgMYxCeguXuRNlPJlIUHN4oge1RYa0wCD0wes9hTqxWaOCdQJgM4sBUL6VWx1UlvM4PPIdx/LIuVhc0CXgHi/O2uAqce7fvxMJhgM3HVyIpJuAV2TG3rxyab4DnwtrWr6tonw3iF5Z3YzgxxZaFKrWrJj+ymkIWHMOtP9ptkzTZbbkfDM5oArMwDS/VmQKgkiZ32yS5hxdDI04MLzUtL9y9E+jNgeLEVDVEeOAtz9G88QRzvlt7mF7f/TTgHUrB8JalnFUZ1tpocv0eggJX7c1Q/S14++rF+jTWomalCkthOmW9eT5zh6RvLPxdDmx8B9uSMO49iAl8soP9UMX0HQLB0miLa4ADlkSEiOLfPXSMicWXTJOXiSI1SGAQaMzQGTPmdxUKg+mZNrh2tYdjUK+zhzffLteIaEEUwesh2A6tXsNWZZ6q0w17HZa1fipaCKgfXhGiihPRY5vK0m5teZlchAlSB1F8l8Ctnk/HCIHysCgmUPQoQEwLeGXwIYljwaRof9zGSWr3Oh1UcXCSihixlUwrf3rlB9Znqp03tSOxL7dpPbObJgLvYH5D4TVWHbH4BUC4WpeCtRvwGNzZGDgNK11bo+sVrcq0enjLy5dB60DCrMhfcQeGmVkCzqzVQyl83lisByru83EKGV5uZBOYYXF46S5OlLFUhV2iUlHkEA1vAI6tFyUrvIA0i7d3staIlVyB/K20gbd4clPUQddQdvv6pwFvv8xF8BFdUE10v3eoVcZWwws+xMb91HXaMwBecZOGyIEd+cs7FWDSz+HdEVnPrb5cMYuE+7oshxSb8EFuVRbcMNhIPc150fE+xvjsbJ/JJhxdSit2jjCLbEROLoFmi73qgfC/FzdOVlMQzfxzMcPAULlocdev/7zgLQUFDHhdam2tlkv+1L1RuFX61Gt93sKUGQl+K9NkjzqD5Tu4IeXkidIhVQwp2tDEZpEy8pCq3SUBSAgg0NzFUFk8sLYQwtW1GNJX1YtSFQRKeEUBY/VWLYFfgN/sGuU9uuQd4a09oieYpf3bZTk1pkoQDIl6riz/XvXa5yExPmbuF6Lh1YU0xqiZrp1NYyIWQuJTtkSxJlcHg4VzWZ7HVqW0Ygk7ccs3yoYE7bCMXaIdTx1AdjKL4mCQxaDaA2INi7e1+QK8R8ivIcixiNR265ySq2nAWx2y6nvEKmrLttYA2tgIx7KU4mtXNZFiR0dm3qIbxmNFReXFQEqt5HneX37FYEgjmIfRTHcnZpwxtehzJhq/cnhh/QbxhLyTUdhpCrO5lFmnV428xoclnWOmZ4aq3r7P5191XRvwqrL6Fn0vfk0EXp/6meP21Dozts1qbe5KalrKfHYjuwYL1zAgyqH+FrabFPVi+ll6mQXFntiEmiS6D11sbMZoxIwSWeXIqPVDMl0YqWwbFIKxokUs99Kt4g/L992r39eVyrQxK7Uz5vwGoAbfLZT2/OANs7WlGRtMyswVuvXHbDqCqtaqwDkkRJfTw5ItGEv3eXnVu+zQgc4Gkul0K1SKEVghybhqmFqMX690ojxJ+Qo5VyuNsAwvU26FXl6nDt78M/EGJFrdL00vprRXbls9B3g9lJo5rxoPwePgZmbt/8H8ouzkLauEt+Lbc/azkHkuSkq+nukcizgCSYpCAGGwwfrqKZxwep2tZmmx8VDRBexk9ywvU3ngVitPmpLqCagTG2yZcfceJLPWbgnTtOB1PuGGa7jawhZua20IgT/x5nq5tnrI1Hq4pj9Ymg9npdC7XVPl+/bcH8uVEvPaQ/8LmB22EiYKeIfomFpBCTJw7gYmhVUVneXeozuftFgE2lgorPazd+C1L90weINe4mpS8LaoOxCqcQxyeBuoVc9br5Y3Dj+6Y8sah1l2UNP+cDhU+m+lb0jsC1ljcDyZVT0KYbaZij8woh4bQ8gPW1X/XHoDcMNhsuSsBUj2Bd0X3s4z8+nC6/sUGqlttrWGDmZDuzkKt1xGdCWwivXnSvdjv/9WfjtNX1lmFhRbxxAOswpqySiDfUEZDz07+chaGXeMsvyRhQSt8ixwS5tT8fLumgm84dQuvZWKmlp9Dh+8JRxhHJDJSn3wlmZCacVejl2/K8uhVNM2FarLnRzVGqp7F0zeM/dK0/Hh8v5/e3/3Xrshhnl83Z7qalLwejz/TrZWbyVSTW1+Eta495fsgoVNyerhlWNv2afUU4VjIEt25bKM2sMwb8jlS6voIy2193tNcssRlScFXV4YpmnBa6gcMWiA1vAQyvC2Pauvjgq+YqgbSKwFEjMHDz1Nb9kh2lOOnUtlZ0UNvNI4wuoeSaa2bPM1+nW/P1g3zYC47TOBt42RbaA2p3ez2lSsQ1Mrny9oJTI9T7RKy/onulsVD+pwh/6nXLuH2TcBc5zKJYDn0aLg3QNv52FbrrnezqtNLmPm8HaltvapnUZSCW+eyKx8YqsYk/l8//OqSgLKt2VibOSjq7NKMYTMcINFNMx8G60iCx3eTx4UacXlXH3e6VCr5Pu4lZtgV7J4p+shX0LVF5v5i7GcG3FeA6EGVxEjsEOprFRu02LIXQyj40m1PlewTgPvKNT2JRdk7SZhyd66tfd3EQZvKQCnaiBYva9iQN0QnTaPXApBBL9T25PqfpwmHRfe9tCGUjsAuKDqWqiU1WTDupyoIqDqrab1JFDFASxfxTPZDPdqGyKBYWrOO/bTkeA9OrUdXc8aeAec3YBU4WK7UtCiDsB+VpNtK1YTa505qM/BdNZzhzeY2prztf2sWhsabSkHc91U4q56mHZ4wSTVCCYUm7v4/XWf99k8rJD30VYz9nmPRq1SV3jrq1Arj9vhm2mCtyae4VS0lIJ05URxSNJgBMjG0knhHYFapc7wdnp+51lNPbyOm9sAb0WpgXmwOYHZRqeBdzxqtRq/J22Twr7PAeE1R+E9U6nCp2RGK+EVxQ6WO8TSroULE9Zx4W1MjfWntqW68uafYY1BRWWO1Qjnmalq7T3I1mBjjdF8iAhvt0NNh1qlcN7qbPQo9+Mq/7qieqIww6LPwtm4ftLwTrye98jh2ma1dorzApweFTcdvxz/yyrrywsfItuX4G2fpeihru9T3zNCXz2FaMPRyQW1+6gKxnvUOg7rVYjuz8rwcB4RHmbpkCB1dsUs1z1AE4J3uJEMp5PD60ubpbSm4tDfUNHhPOE6S3iHG8LgMmb23d2GHvD6K4WGt6mD3By6V7KXe1xb6aTwDnfu0WRks7rbpu4vHTo0F3ae4KP0Mt9z8XmHO+kz13AZvU7nmbiOC+9wJzsDVZSKjXiyuWkKnRQon8Y1hpOENXRQCO9UNSq8k3QTggeF8E5VCG+jEN7Jqv1NtOaZNX2eCO84h0KFqK6wsio6jT7vaIdChagG3uMs4HMq9SHuYbF48X6YQ6F6COEN1wMn98GgF+E9lWpK2o+z+tSJ1J24b+/e8D+vXg9wKNRomqRvO5S6E/d48Zb/efvy1/6HQqG6qAe8P4DH8IDwok6l7sRJd1c5vQvQUGNCoVppIHj7HQqF6iJ0G1CzFU7YULMVhspQsxUmKVCzVR/ibjE9jDqlsDAHNVshvKjZCuFFzVYIL2q2QnhRs9WQ8KJQx9AY8E5L039j0x/h1Ic48eF11/Tf2PRHOPUhTnx43TX9Nzb9EU59iBMfHgpVLYQXNVshvKjZCuFFzVYIL2q2QnhRs9Uzgvfx96IjKa8yfig9OLXcEXJdvfpymNAIS0PkDxbQ7jWhIRZ6PvA+XYp2uiv+EYv2urzRw+34OJncER4ACYB3MiMsDfEWRrZ4O6UhGno28HLLAJ/70yV01t2++pK32JV67U4ld4QHeAzwTmaEng8RBjWlD9HSc4H3YfFGdOHnq0nkzc2lLuepjBBG9eq/cHinMsLyEHN4JzNES88F3oNaQkJ97ou3+bISpfUlTid7hGLpC/B5JzRCd4jabZjSEAs9N3iViVi8za1HaWWf08keobgXA7wTGqE7RD1Pm9IQCz03eNVcY8Lw5iMUfu8k4S2GeMX/+XjxZlJDLPTs4D1c8UnH//oP7yfrNtgjnKTbUAwxnzhMaIiFnh+8oMff/zq5CdvBHeGtagx4O6EROkMsT39PNzKPnie8kwyVuSMUf19NKlTmDlEyy382pSEWem7wPl2+Pji5ienE150Rgq6mlaRwh6h93ikNsdBzgxfi/kVm03lwarkjPOj08GRGWBoid34XYHQnNMRCzwhe1LkJ4UXNVggvarZCeFGzFcKLmq0QXtRshfCiZiuEFzVbIbyo2QrhHUlXMjEFD97WPe9BVud899dfzJ9+ewfVGZB9+7fxhjh7IbwjSbUycjjrq1ke9Kqz1tNyeP/p99Mq5JqUEN6xdCtw/PauoSLgQRrmP/9cep6A92piVYiTEsI7lr69AyxvtfdQJQUvND+WDoDw1gvhHU2PF6++PF3Kut0//9fF4oV0a//5D/Lht3evbxcvfyngfStxzV0G/t+f3rn+BMoQwjuerhZ/cyvRfLzI3VrVP/GGM/rdxeLVl9xt4CYW4Q0Twjueni6/u5DkXS3+PTe1/51zyudxv3CYL4FN4SjoCduLt4cyvOg21ArhHVEPC4neo2RYLuFx+OPf/e0fFsCm+GUebfjLLwhvoBDeESXaaQ6517BYiOVx1CNJqp6wffsfwpNAeEOE8I6oErwvf326XPy7v/77f7104TXSEghvWyG8I6qANw+DSVaffPBCj65sf0R42wnhHVEa3m/vXvxnDuo/c9f3YfH6y+HPP/vchtcyp8wncia8k+t6nJAQ3hGl4dV+AwcR+nKlA5HDq8MN79U/fvezAe8thsqqhfCOqBxekaRY/PQLPPp5sfjub65g+VAT3hfil4d/ulj89CfT5336efHqS+UJzlwIL2q2QnhRsxXCi5qtEF7UbIXwomYrhBc1WyG8qNkK4UXNVggvarZCeFGzFcKLmq0QXtRshfCiZqv/D50ofy2UIC3uAAAAAElFTkSuQmCC" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI0NvbmNsdXNpb24gOiBEZWZpbmV0bHkgbGF0ZXN0IGhvbWUgdGFraW5nIG1vcmUgcHJpemUuIFdlIGNhbiBkZWZpbmUgbmV3IGNvbnRpbm91cyB2YXJpYWJsZSBIb3VzZUFnZVxuYGBgIn0= -->

```r
#Conclusion : Definetly latest home taking more prize. We can define new continous variable HouseAge
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBZZWFyUmVtb2RBZGQ6IFJlbW9kZWwgZGF0ZSAoc2FtZSBhcyBjb25zdHJ1Y3Rpb24gZGF0ZSBpZiBubyByZW1vZGVsaW5nIG9yIGFkZGl0aW9ucylcbiMgU28gbGV0J3MgZmlyc3QgZmluZCBvdXQgaG91c2UgaXMgcmVtb2RlbGVkIG9yIG5vdFxudHJhaW4gJT4lXG4gIG11dGF0ZShyZW1vZGVsX2ZsYWcgPSBpZmVsc2UoWWVhckJ1aWx0ID09IFllYXJSZW1vZEFkZCwgXCJOXCIsIFwiWVwiKSkgJT4lXG4gIGdyb3VwX2J5KHJlbW9kZWxfZmxhZykgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
# YearRemodAdd: Remodel date (same as construction date if no remodeling or additions)
# So let's first find out house is remodeled or not
train %>%
  mutate(remodel_flag = ifelse(YearBuilt == YearRemodAdd, "N", "Y")) %>%
  group_by(remodel_flag) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6Mn0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVF3VXJFTUJSTTAxYlo0aTRMNHNsdjJJSlZSQkNoQncreW9BY1BzcDRrdHVsYVRKTTFUVjJQbmp4NDgyLzhCTC9IbzBqclN6WXAwa0plNXMwYjVtVjZmYjVJb2tXRUVNTElEenlFZllBQmh1S2hBSTMwL1lLUXY2dFpPRk1qdElNckIyNmhqTTBFNFY4NG40QW51aytQejk3VTNwTk1ENzkrNWhlWHF1ZVQwNCtiOTI4dlBhREYvbng5TWxnWlpvelV0VjNueUNnbmlzU0ZKQlVkeWpsd1RoNVlja2ZTU3VTVTNSV01MSHRmMFhCbEc1ODhPMzZyb25sSitNQjJKTVU2ZHRZbTNpdVVydXRhdU5xQmVGdXNWQ2s0U0xIK1YrSGc4WjRjRU5PR2ErdDhsajAwL0hGMmxPaUVacjc1eGhiamZ6alk3UFE3NnhXNjUxTytMRGwxSVJtNXA4dzJFOGhnSXNRcldmYlJJMkRyV0FsRm5DN0tCSE9NQ1lmYVAvdjQ3VFlhQWdBQSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["remodel_flag"],"name":[1],"type":["chr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"N","2":"764","3":"22.24033","4":"18.23269"},{"1":"Y","2":"696","3":"19.78507","4":"17.39609"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[2]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIG11dGF0ZShyZW1vZGVsX2ZsYWcgPSBpZmVsc2UoWWVhckJ1aWx0ID09IFllYXJSZW1vZEFkZCwgXCJOXCIsIFwiWVwiKSkgJT4lXG4gIGdncGxvdChhZXMoeCA9IHJlbW9kZWxfZmxhZywgeSA9IHBzZiwgZmlsbCA9IHJlbW9kZWxfZmxhZykpICtcbiAgZ2VvbV9ib3hwbG90KClcbmBgYCJ9 -->

```r
train %>%
  mutate(remodel_flag = ifelse(YearBuilt == YearRemodAdd, "N", "Y")) %>%
  ggplot(aes(x = remodel_flag, y = psf, fill = remodel_flag)) +
  geom_boxplot()
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIG11dGF0ZShyZW1vZGVsX2ZsYWcgPSBpZmVsc2UoWWVhckJ1aWx0ID09IFllYXJSZW1vZEFkZCwgXCJOXCIsIFwiWVwiKSkgJT4lXG4gIGZpbHRlcihyZW1vZGVsX2ZsYWcgPT0gXCJZXCIpICU+JVxuICBnZ3Bsb3QoYWVzKHggPSBZZWFyUmVtb2RBZGQsIHkgPSBwc2YpKSArXG4gIGdlb21faml0dGVyKGNvbG9yID0gXCJyZWRcIiwgYWxwaGEgPSAwLjMpICtcbiAgZ2VvbV9zbW9vdGgobWV0aG9kID0gXCJsbVwiKVxuYGBgIn0= -->

```r
train %>%
  mutate(remodel_flag = ifelse(YearBuilt == YearRemodAdd, "N", "Y")) %>%
  filter(remodel_flag == "Y") %>%
  ggplot(aes(x = YearRemodAdd, y = psf)) +
  geom_jitter(color = "red", alpha = 0.3) +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArwAAAGwCAMAAAB8TkaXAAABC1BMVEUAAAAAADoAAGYAOjoAOmYAOpAAZrYzZv86AAA6ADo6AGY6OgA6Ojo6OmY6ZmY6ZpA6ZrY6kLY6kNtmAABmADpmOgBmOjpmZgBmZjpmZpBmkLZmkNtmtttmtv+QOgCQZgCQZjqQZmaQtraQ2/+2ZgC2Zjq2tpC2tra2ttu229u22/+2/7a2///WPj7WQEDWQUHWQ0PWRkbWSkrWT0/WV1fWYmLWcXHWiIjWqKjW1tbbkDrbtmbbtpDbtrbb25Db27bb29vb2//b/9vb////AQH/AgL/AwP/BQX/Bwf/Cgr/Dw//FRX/Hh7/Kyv/PT3/V1f/fHz/srL/tmb/25D/27b/29v//7b//9v///+cbkRwAAAACXBIWXMAAA7DAAAOwwHHb6hkAAAgAElEQVR4nO2dC3vbNpaGmXSSunNr196d3Z1tPDMb785MJ50mbWyn6uzOJb5JIkFG7sb6/79kAV5xIwmQAElY3/u0iSJTFCy9OjwADqBoD0CgRHM3AIChQF4QLJAXBIu5vKsoil6wG7soevLSW4MAMMVY3hUVdsfs3bEbsBfMj6m8D6fP6Z9nz+mN4+IGADNjLe/9EcsdVk9feWwUACZYpw33n7GMYQd5weyYd9jKflqR7pZJb8Tw1TQAujFW74zG2vujY1FeqzMA4BZT9epUV0kbIC+YCVP16oCrdNggL5gJu8hLA64yVAZ5wUxY57zKJAXkBTNhrt5ZFEUs6LJ5Yn6CDfKCmRivHuQFMwF5QbBAXhAskBcEC+QFwQJ5QbBAXhAskBf4Icsy308BeYEXsg8fPvi2F/ICL0BeECyQF4QLcl4A2oG8IFggLwgWyAuCBfKCYIG8wJIJhhEMgbzAjikGcA2BvMAOyAuCBfKCcDHKeSdJjCEv8MA04RnyAg9AXhAskBeEC3JeALqAvCBYIC/wi8cEAvICr/jsukFe4BXIC4IF8oJwQc4LgArkBfPgICJDXjALLnJhyAtmAfKCYIG8IFyQ84JDBvKCYIG8IFggLwgWyAuCBfKCYIG8IFggLwgWyAuCBfKCYIG8IFggLwgWyAuCBfKCYIG8IFggL7BlMd+oAnmBJcvZ1x/yAksgLwgWJi9ZROYAeYEtWUaWEXwhL7BnIZkD5AX2QF4QLhkhkBeEyTJCL+QFA4C8IFggLwgXN1PEI88CecFsjI3fkBf4oyeyQl6wWPrkhLxgsfTKiZwXLBXfYxKQF/gjy/F2esgLfOI1+EJe4BPIC4IF8oJwQc4LgAZz9e6Poug5u7GLoicvh5wBAKcYq7d79n7/8YTau6Pm7jh7IS/opskcHOcQpuo9nB7TP1dPXxU3zp5bnwEcKE2fzXXvzVS9+8/KWHt/9GKfW2x7BhAcjuoea2VJms4i7+7pn06i6LiyeAd5Hz+OAmV9mizN6H/jT1hjqt4qoro+nD4v090y6Y0YDlsDloSrq3wVwLMPaUocnK/GWN4nZcAV5LU5AwgN1ymq8wkLY3nzPIEmvEgbDgfXEwyuz2ee8+byfvYSHTawFEzV+3jCnN1hqAwsB2P1Vs/eF4O9mKQAC8FcvV2UD5WxgQdMDwOReTZLR2EOGM9Me5BAXjAeyAuCBfKCcEHOC4AVkBdMg4fgDHnBJPhIiyEvGI1JUIW8YIkYeQl5wRIx8xI5L1ggs+3xD3nBaMyCqvvQC3nBNHiIz5AXTAPkBcECeUG4IOcFoAbygmCBvCBYIC8IFsgLggXygmCBvCBYIC8IFsgLggXygmCBvCBYIC8IFsgLJmOuzaV9ngEcBrNt6+/zDOAwgLwgWCAvCBfkvACUQF4wEVgGBEIFCzBBsEBeECyyvA6yCMgLJoKzNcsISccHYsgLJif7kGZJlkJeEB6QFwQLkzdNCXJeECA053Ux6At5QbBAXhAskBcEC+QFwQJ5gWfsptJsjoa8wC92NQ1WR0Ne4BfIC4JFr2NbdgB5wZLQedruKHJesHDcFPdCXjADpbwja3ohL5iDXNux8RfygtmAvCBYIC8IF+S84FCBvMAc9/uGjALyAmM8bL0wCsgLjIG8IFgcyuskAYG8gKPHKWc5L6aHgWsmywsgL3AN5AXBMl2PDDkvcM10A7kungnygjnIPqQpGXsSyAvmIEsz+t/Ik0BeMAeQF4QLSbktTgcmwLJ6D6dPXz38zx/eDz8DACbwG6UPHOSQ1ft48vQV+3/4GQCwxJW8D6fR5/999OQ/f59jEoEhLxiJK3n3u6OowSQCQ14wgmIlppucl8bev/315Okf/5bz90FnAIfG8BmHUXN6OvUefvfv+nTh7Bm7fxdFT152nwEcFCMMdC5vG7uIybuj5u44eyHvkphloc7y5P3Lrz7/Srjj4wmT9+H0mN4+e25wBjA586x1GPOsYz5tWvXYYC9NDoTsYL9fPfsNlff+6AW73XTlIO+C6NHIV1yeaWGmVr2z6Nk/TqPjXfScu/P+s5cs56V/0X/sIO8i6ZZ3prjszWxth+30ycv7oycvhckKli4weYt0t0x68/E0Ty0DQ+g0ZRZ5PT6pTj0m7S6SZtpWVFxF3rYzgEVyKPKuaMpwf/SsHjLLswWkDYEzR246sbw05/3FUfSC/tXkvKtyzu0FOmzADvUT0/EZsvp4tYw2RNEXNAD/RJodPsNQGRhPRyy2C9Mt6v3fezZPLN97hkkKMB7f8uoppodXmB4G9jQJgW95//JvP//5538ccwYAeHgtvee8T45o3muyoALyAgN8DDq0zbB9td//eBodDz0DACJTyfvxpMhp+XFeuzMAIONhjLltkoL/2/4MAEyAPm1A5AUNC9vMv6Glw/aTr/I/TRYRQ95HztL2Q2/Qpg2/+nkUffIzw0WYkPeRE5y8HL+AvIdNWPJOfQawbKbKea2fB/ICR4x13D7CQ14wCEXV0dkF5AXToJrmTl7jEA55wX7AJd+DvFUjzE8EecEQ8TSPcNWvg7zAhgFRc6iq/Y+DvMCGCb/CyuCZkPMCGyYrX1Dkdb7d08RnANMxd5GNLO9ku0T6OgOYjPmneqVPD+QFpsy0EV/HM0JeYMjyNuJDzgtMmWEjvml3iZz6DGAheJF36r3KJj4DWArOgqSDbwg0APIeKuai2ist7DAiyusyiYC8B4p5QOw/srs8Uvip0zg8ibxzj4wDnuLdcCivTYVZcPLOPzIOGsp3Q/umaKPMAHn3GSGPQ96MpJB3OVT6aERtMavvwqmTtz30Sidb9jhv9iHNUsi7GJxtMMo9Tt373PRMC59ho81LW64hYA7aY92Yb7IcWLLQHDggBE8iL+JuIAy+hg+rdKQHNQvXBmgyRc6LsYZHT1cuktP6oOpnC5UXPH46x8bSlg67OBoMecFM6IJrfp+pvMvMecFy8ZrRFW7W8uqG5kY+PeQ9YEwv1cMkq2ZDipy3fcZ4OJD3gDGUd+B4kTgK1vTOsow4GoCCvAeMYcnNwF0d6iniwluaPcTFjdYk2BbIGzQjr79mE7/22QV7RBNei8eTNEmSQt4kaaZclz09DPzhewKoSVvtGqPIm5IsS2koptJmaUKSlMjPQAZIDHlDxqu8/PyXZWNEeYvSLJJmWUITCSYvF3jL2D6o/gXyhowHeesoK8x/2TYmz3mlpUAkTVmRCxNVjryQ9xBxPlCbSZnq0MaUFe/C3G9RG6vLeSEvGIuQKIyK6nJPj1+9IQyVVXvyIucFo5AzVUEnuxivH6ao6+DdfEIgL6jpynItLWsZY6vTCCGxHthcyAsaumZwbS0Tc179TwecVgTyghpulkFed+h0XIP76pQhqW4N5AUNlb0kTeTev93CSZZ9kJi0PKSamRi7Mte3vGUpBtZSLB2+8quaDOs6vG+7STYVQVJ98B41uMvhWd6yJgOr2JaO8EZl5WRY3/FdP22Xt1oXBHmBKT3XeUHeD2lKhu6GWobwVnn5JZepnFnY4V/elLgq3wQj6Ikg1fyBVIDb8YC2gYTqRGrOSwgRGjK6sNd7zpvXZCDnnZ2+y5+r7xLu3aZMKIGQyiEs8T7agD1HloG1i6Mir+7wOilp9jEr8pP90CA8gbzY7WkR2H+98PCcV3s4qTPq5qEkTctoPGR1xQQ75mCfvYXTu55Ct6x9wHSx5ouxm1RigfIaZP5gZnqzYd3Pe9/Upu9HJAfyKFwPl9V58ICOkV95qzpOJL0LZpC8feGaG3XLs0ax1pfkkTYvTa9KIocYMoG8yBuWzTB5DU+ay6v02PM0Qe0LfV9g/CT+5SXCmiWwLOr1Oh0hUB1F66+n4eVV6iRqed+dX15+r2DceM/y0oSBkDhJIO8iaS6KmkHY8hDdBuraASSleD13nE1W1Kt+6kMuKecX7y4u3r1T7TVuvld585ciTtNkA3eXCGdhJS8LiOIhas7QPEzIZJXK8yrdTdmyd2bl5TvBVervu0XLm5KYFNOCwDljq/VUeVmobN6sfGYhTeV3r36YWL0u1d3sL99dXF5QN+nfF+dM1Ute3kuWMFR3fCpg3H7P8qbZ9vZ6myLw+mD0GCQ/+1kufeAjb9FjYWFTflyZ83K+8olHmQw08r6juS0Lsk2g/bQL4/b7znm322SziUc/CdDQJq95QO4uaKh2W2j9hNS+FrLmnS+qapXJ0rTg8rJKD/I7Ly/1ui4xbaC/V7JN4hhZw0AMyhiN7+47v7rqrL+eNat8bTJXGm/fvuUzWb2t5+cXF281Iw1Lkncfb2ICeQdiXQmmPqpLf2EAXt5job4lnoFLWJuOl9DtOr/oSgneXl5e5MK/pfpq5b28NE6FvNc2kM0G7g5kWFLLz7V2nUEY8RIHzTTDuJxcl9KowfctyQCXEhTdMxptz88Leek/zvXuvntn/DtP8vWtKOcdxtCS2qa+0FRecdwhzWuw9Rd1KmBfx6vsrsmjYHkH7uI7nbMDf2fPHTY2RRFjdngoHR97s4LFbnnrsQYWd+ntKvRdtE0ftA0TcGGT9cqURLiM18Xog2RrW9MN8D1URuJkE2N22Dm9CyCVBFY5ppnjJbTvdMGNwJ6/4+TtSgk+vZR7a9xA7jkXZC/f5fW8+YdF2kFSbdcyct4s3W7uyBazw+4ZuM6hQvCMZqG0/9QzPlDZWs445CG2/kMrLz9CXNfzFimNo1WNXuUlJIlv4ySO4a5rrOsU5eu/KO/52/M2a7nr/iU/mvuO9b9qefO7hQZkqryEkDKhDkDeLCHxep1ggs0DxssbNIlrI2+rrsqAwsXFWz4NZibTgJ1mwvQa3zBB3nzSmO0Gkc4i78NpFEXH7NYuip68NDpD3n4sHZ6MUqEWXfszWP6iL8l7TjNhNvdQPlG5aYj81RL7elXafi8stMyPL+TNx+HcDECZyvtwSoVdRc+pu/TGjrO3c7SBza6N3E3t0ePgjWwxrl/X6qKf/yWmr9U8RPEM9C0kCb9dE8mIOFpRDm/ItRB5optXTAihzIm9pvLeH72gf66evno4ZeH37LnRGWirkzgJpBh9puHoUeU1ci7Az3y1pATaHlaZyRZJrXbaLv9Ciaz+Rx5CK2X5QTch0y3Xu5e1atw2JG7WNdrlvDTi1habnIEVoq/TOA1huGGudaJ2z9uVEnR2uBrBNfIaNIf/aFdhuFkuUdRTEqLkEoSTl/uh/CxTrGE7e/rq/jOWMezM5I2TbXwLeUc9r72uLdby4bl5dqWuTC5H1zW5iLySvIWizT6mzaBYlmy3hAXepArLwt4NNDce9tpbybujPbYi3S2T3ojR8YBc3s16G8Lq4dlW6Cv+DLW1VVeGwfPmVJd4dd2aWG5G+KKd/G+pkL3cioH1eEhC8l33WNqQyjkve1jsX95d1V/b8z227rSBbNYxSQJwd9YSjM7o2mWtJqh26CqgWyOxryKvUGZeHM2X6zTlZtx0mSJvKTi1eJvLS8g6UXs/08i7y0fKrNKGLKUXjIxsH+MshRPXW81r07VTcDWD7Wi2Mi5Q3l1stSGvxxT2tGmGdsu0tuiulcu9MmGVBbuRsHWMJKEfllh90Ui5UHPAq2cu76oY5bXqsLH94QnLHcKIvTYMzDI6zRuaElS6GrSJ01Evr7ymRyNvMbjAySssJpaDNjs6Wa83e5Lop6uGL3E0lncVvcj/thoqY9em7dX1Nn18SzCN5e20bqyubW3iuk1ZyyH7rgU+5QwDt8WYUGfJbCUs7eDkrTZ+YBFWOG2W31X2ynqqcuwwH+c9Lm9ZTVKQJN6u13GyGHmdvXAd8nZa12Wttgixy9a23669JFIYyuJfC0n3KvRmmfqJKIt/c/lzGUkz45t9SKincpoYs/072OdBSDP6f48eTOVd5QML+bzwynx6+EO6vtuSu81i1g87HFLgX+Chtn4qlbwOtrbt11R/3zreSnuESI8QEgb5Jau/RJirZ6gfl5KtOClV5rSxmGZ0zbqavkueSyKzeLsl8XYxq9icyTtY1xJmqnY2d6CuIo2h6g444sRCfle5jSNpy3abyFttylA9pMl0y9k2fnsnLoZXY7m1vJ07mi5FXrKhufpyllIMl9fA1k5rxUOkUljnv2WdG2gXt4ubjlZWFT4pg2RCzyvl99Hlzk3Saje9LCO1x8LHoBzGKNOM5cvLBhvi9dZyFM/reKvFyd3qqpHXZqGs3S/JL8GUy6IyEosX/abWNle+9RUS5JWSDrGiQdiSpH4iblSBZsXdK0Hc5rwDz5DFd9vt1iryzjbTNV7XNmu5bHboL2n4dtZX6rSumZE3xaNdKpJ84Pr8VQkCmwJLOvI7Xl6p/by8Sr5dDjBI4xwuKg19rx7ebLbbtVVDJ5XXja1F+fa5fs2i/jeyvLw0RhhtQ9KMa1WqNo/NUukL0qpRAKauduSXa3Od84rt0Zf2cplH9fkoWyCMMA+/0k4i77D3yQ8W0bXLWjW6cmtjK2tH/0ZCdJS6Wdrj5W4Wm92spoiqu6QAW3ekMu20hZQfSGNxVSLLhSe1sqcu0alSDnGNxfD323POS+6S29sryyjjNue1trUjg20ZzSrkfXfRMno5+O1Ru/zaU4kRju9N0YgYb3J5m36UODlRxeiitEadthCfsEmmqymJegghqwJxKa/QqNxaEt8l5eaSfH9yqfIS2uCr7Xo78TBvu5Zt8hlmsG1jWyzIdr0HfR/Htp/LLrZkINx90pnyvQdYkiBsUM4dlIlfw6M2RBnMFYcJxJGKOj0oF080Y2VsoDclbFmCMJLRHD8oZvmVN06S23hD4szzOK9BOJXks+pwaR6vtmH4BaPVe938gPosHR+bfI9ZlvPm8iZqfRQ/LqF9AjH4E+Urp8oB32KPnayRkasVq9MVksZSh7Aa6Mg6f4tWvMpL0634Ot7EN5vN6KeRMNRVlc9O1wb2pCaF2gNo740JRbRtH46uvnteTZv7xYoL1MZrpo/lO9j8Qp2xCFkGd0zMrQqui3tjIaYqHcX6nB804xdG+I28d+vrzXp9FbvY5XSQrt8bd7g6rS3xLG9XCG3/elOWQVYxrj34Z+zrFTQnKCYNmmSdnk0M0Mo26PnnQRopq78enSu4pHmtNIlXLWHjJzfylUOLlDdO1nc38fo2GVSYM9TW4asNVF1FfA2EdCS09RO3TknVl+pywzHdmTvPni9Jr1dGKgNpyhdQqI3hAqjwzPJgiTKuxj9waTlvnGxvruPt3TYxi7xedLU4TV/7PI/iqf0z7ie98hLNl0aJ5QdtqQXt1G3qUlt5sFc3y6GVtzPuV8E1pcG3HClryiMG9xY8b/e0ubvebLbrrVKMPthTA2td6arpe/tdKaQM69Y/UPpV0qPykQBBXnEuQfck9R1JSvsmVZ9as/GCPL9MHdyI0YjolkjwZyjlTWkCmcRp4S8bjhgXDXxvtLe+3WzylaZL0dXE2rL1Xcb4Re02dbWjmRNudpPVJZKFz2reTpI1DbeVvM3mCm3Pm5FmFXCVCGiG4fhfpixYS5It7dvFacL2rxPWGg/C8/68m7v169dvLi66yqyH2Dqq32UIfdETzYLBKbCKSJlu61BNIpnVY1hEPkFKknIAVuyKtbSjjs517U2dF2vHoYscl32dYJxQefN56C1R2mGN5xm27Xrz+vXbt/kehG50tf4UtLWt90OvDi95zhr457Z4Jt13U2uHiNvk5evA0pRfU9x4J14H7OQtc9y89mcbJ8U8dCKvFhqA510i4+u719988925mbx9wbV1hstMV7Ft/cGNuzyaPsQONx+GUh2pIKZtskxKGyTjU1ZFxdUdNN7Jg79CpVhtf6y7VBWzztU4cSbtWjYCzx227frmz1+/+e7b7wbqKtInr02zTUyUtjZwLa+r80mrcloHLTK+KkHXBDZOton57Y0477StV8p6xaJKbi2FOItNnGxD47m24e7q6s9ff8PLOyqDVWoThjfbyBzpvVmovHtxVQ4/o6vdV6S9CWxrG8IPWDTeKYFSU1Ihj1Q0gVn+1Li55vhNG9ZXt3fdGaxZIjAuyLY0zv71c5zzOv4wyOWKmmEvbRMI9+UUtCeVCDs5Vt6pE3x8gK8k1chLdBvcOvrNPRfmrNe3ndHVQt7RDV0G/fFn9EeEm6PtkzfXkvsWK35uWJzh6KoRaoI+q4NowmzRAczSVNxlOhB5SRJfffP6/K3+uw7N5B3dQJ7pxgvaGtD7tpm+sSa/Sue+IuVp6DHlQJmUZrTJ21k3KSa4xUcj4b7urbeKwwbPOe/m6urNd68vWuXVVtiOblIrnud3nbSg7YjWWsW28+jHHJRnS7NtWk5RaNdRyk+v6aipJRRcAq6TN4Scd7/Z3Cbfvnn9reE47+i29LFoebsvqXLdC+lZ1Wr4q+bzctuknL7nIrU08qYvINf8CkXqwT+aEGneT31Qfzu1+F4GtE1ef/vmouU7kidPZC3l9ZFktJ6zJypJg1pKuUz38Z2HxfW8haYTpgx0dcib/yjespFiPhZnzcohu1r6PjzLG6+vvv76zes3yrfTj37aYVjpOG2c7nk2Wd6+/b4sUmdu3kLXCZNHabnJCfU501SZlhTy3O6E2RLPtQ3rayrv19++Pj8PcLRgUfJqJhe6P4nmn1P9M4uDZHLWov2GJ528GfetKx+Ikux0VNn341ne7d3V1dXN9WY7cyd/EBNnyHZXhdbw5/SZm+kJo/5irmIqlKXV+Q3bESrV1AaPqNzznDbcXt9cX13dLWeLUyuG5bxqwayf8bkpPltt+YESL+tQXHU7ywngOr8pVisp8o5aWOX5W9+3VF36362rndFnH6ftR61i8SSZi/M2Ywj6F7YlwGrWUohaynVndT9PytR1NW7m+JV3u75heYOzzaXnH+rqR7kSemv0+E+yrpjH4DnUi70sb7OYSJi0Vi9Ky428m3hzc7Vm0ddRzitO+iwzCithacGfOF0xj8Grqv5GkrzaZe5tH4Olyntze32X3FyvN3fuI+9inVASwv5pLs8fQ4OxZfmGrpiy64Ti8ENVJNH/i4361b3Ke7PZrq/WN1e3N3Z77bWjzEMuEsumGVQgjKJ/Vk+6umtGle0aqD2L7mnH4Xfp+/XN1U18dX1ruVGkEQuW13LUq+7cWL6lpsf3TX9oEvSR8gpV6NYNMsbzdk+3V1ckvr25i0c/jcpCc15rKnlt31Lj47sPVKYfVO2kf+mneS2eOAh5yWZ9c7vdNOuqgYZ6laPRW6qZwLV4jPbpdQl6e86bb41mXbbZtzp0EL6L0be0s+ZgneiScVU8bvSW6kpnRj67XYZQLJ60rQ7Tf0LG4jnyXt+uCclc7LO3WKaYpdU/W9vxlmpkWWYRzlvl7Xyknw6K78h7d5dk46ZR5sJRd8gxPflrNiB3tgvnbNub2Lq0MUR5SZpsycg5wB58ddscdYec039xth+gMgnnNW0De12vg64IzcEb53n18GaT6jdpcYW/uVc33aFJ6Za3/TeyehEHDN6q5R5uauI8R944jmlTPea8C5B3OVSDtDZFNsWPLD5/A14Y+SEdizGs8LwAMyOxw7pTDf5OvpyAao7NmNjg09m/MIHKy3bPtPz2Vks8OBaitiZYz+D5GkcxWAdihOdidJrzpnbf3jo/ASUMfj9mHl4I7RTIYDx/A2YcJ2ky0w7NQwlHXs8tdX96x2f0vIYtjbebrZMdAacD8tbndx11wpL3QxKvyTy7iw9ntvJa6xMF8zErCUpekiZss5+eLQYODIfvYHBdS7cN9rwAM92ut0T+gqUDJ7h4uVh8yxtv4m0c2HDDQJZZDDE7Hq8Ovpe+b7dp4mI8evmEOJ88AbqXxdUL4PvbgGjSkLgYj14+BxZQ25Hq2NWXxdkr5X2obLMOrxpyEJC3QK47D1heQlxtlrN4HtP1ZcTvohQyKFtUByKv91XdS+IRyTtGr8663s6yN2s8y3tA19LQflWLJWfOThzUJMXeYp106AQm7wyrdtrOO9gP3/LuW77S8/HxmOT1t7hKs9fv8BfOu7y6PdceJ2FdYGb8rPWPRxgygbxxEh+EvIEx32ctIHmTNIl97PYEQqVzMM0G/zkvSRIEXsATyFDZPriODAgH//IG1pEB4TBB5IW7wA/+O2zIGg6BWUIU5AUOmOddhrzAAY9UXuS8h8BjlRccAkYbY7sOY5AXTIT76Ax5wURAXhAskBeEyxJy3l0UPXk56gwAuMBevR01d8fZC3nBTFir93B6TP88ez78DAC4wVq9+6MX9M/V01eDzwCAG+zl/YxlDDvIC2bHWr0i3S2T3ojhvE0AGDFO3kFnAMANSBtAsKDDBoIFQ2UgWDBJAYJlgHorTA+DRYDCHBAskBcEiwN5AZgUh/LOS8DtR9PHspBmDCbg9qPpY1lIMwYTcPvR9LEspBkA2AN5QbBAXhAskBcEC+QFwQJ5QbCEJ+/9T/NS4ro86P4oivICTWk/iQUiN53eiFh19NKb/nBKG8oqYZuGqjdmIDh5P57kdfBn9BXL6+J3z97T+56rpZrLQ276irWY2bvwpj+c0ratIv41Vm/MQWjy0g86M+DjCQsEq2fvi9r41dNXSpH84lCbzhpLW7z0pteLZ+qGqjdmITB5d9FxvnyuXgZaLKnba5YnLQ2l6bW8i296Dnuxq4aqN2ZpUmDy7su1n6UB0Yvd0z+d5PmYsjB0gYhNr9OGEJpOP2VU1aqh6o1ZmhSovOUnPnqxYpdiFsOUJfkLRGx63dkJoenswtE0VL0xS5sClbfs9VB5n5Qf/RAMEJvOYhm9cRyEvLuqvwZ5x1Beo85o9+dP//yySLdoNAvh2is2vUkcl9/0XT5ShrRhLNwrdf/TV8W/6GsYQq9Hanrd6Vx801fFKC86bGPhDFg9e//x5EVx39LHmxhi04s3PoSmr4qpFM0IGYbK7NgVg6VVCkYtKF7ChY/0M6SmVznv0puet04foCAAAAMFSURBVDEHkxQjKcLXxxNufrK4qK2WPce6V5t+FkbTV8W6xzxUcDPb0o0ZCE9eAEogLwgWyAuCBfKCYIG8IFggLwgWyAuCBfKCYIG8IFgg7xDOouPqxouu43blppyf/Pq95TPcHxX1Avn6Mc394s0DBfIOoVxKWVS5drCr95S19awy8/6o+pyI9+8hL+QdSL6WVgmLCrsyMP/lyHb+vzLz7Om/CvWGkJcD8g7i4ZRpuRKjokolb3PDlNLMjyfPfxAeCnk5IO8w7o9YLfGzPJX98bdR9KTIan/4WXHz4fT5Knr6lSRvc+DZs3/8NnryH/sHes8X7/MfHUXR51/lp/sVve9/j8qNVF5Uz8Lfzx9ywEDegZxFX5Y12mzLnjKrLYsHj6m8nxxFz96LaQN34Nmz37CbX54Wh1c/KhZo5l28oyIvofecNTsDlffzhxwykHcgH08qec6if6Kh9r+op7QfR2Pn/QnbUCTPKJoO2xfCgfTms6+o0uzPH6jk9N9f5D9iaxPYUfRH7OR5Gfh96XF9v3DIIQN5h7KLip5UmXoWW4js//b73/0sYvLmP6yHyr6UDsyjaXHQw2mdgLA77qt8IQ/QzWHc/cIhhwzkHUq+nGdfX/EjFkDL20ze3MY8bfjxlCa30oFnlbbFn9VCmxVbjXlcn52tuYjqxKK+nz/koIG8Q1HkffqKyvbLX//hryeivPsyh+AONJS3zjryzwXklYG8Q2nkrcfLClc/yvLSe4r+WjOwJsmrTxvK3KOYx0PaoAJ5h1LJ+0CzAmreD9QoqtP7/Y//Esny0r/zNc71gbK8XIet6NblvbF6IDe/0dzP3zxoIO9Q6qt2mQ7Q4FrlqGwrBkHeohiiOVCRl/tRcfOX1Ndqu4RiJq+5n7950EDeoTQpJ5t7KCYYaNSNPvnyjG1fKspbJA7NgbK8xfzFF3+vTsdmIKoCin05lVfdvxduHjKQFwQL5AXBAnlBsEBeECyQFwQL5AXBAnlBsEBeECyQFwQL5AXBAnlBsEBeECyQFwTL/wNQMzWKN4gSyAAAAABJRU5ErkJggg==" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIG11dGF0ZShyZW1vZGVsX2ZsYWcgPSBpZmVsc2UoWWVhckJ1aWx0ID09IFllYXJSZW1vZEFkZCwgXCJOXCIsIFwiWVwiKSkgJT4lXG4gIGZpbHRlcihyZW1vZGVsX2ZsYWcgPT0gXCJZXCIpICU+JVxuICBnZ3Bsb3QoYWVzKHggPSBZZWFyUmVtb2RBZGQsIHkgPSBwc2YsIGZpbGwgPSBZZWFyQnVpbHQpKSArXG4gICAgZ2VvbV9iYXIoc3RhdCA9IFwiaWRlbnRpdHlcIilcbmBgYCJ9 -->

```r
train %>%
  mutate(remodel_flag = ifelse(YearBuilt == YearRemodAdd, "N", "Y")) %>%
  filter(remodel_flag == "Y") %>%
  ggplot(aes(x = YearRemodAdd, y = psf, fill = YearBuilt)) +
    geom_bar(stat = "identity")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogV2hhdCBoYXBwZW5kZWQgaW4gMTk1MD9cbmBgYCJ9 -->

```r
# Conclusion : What happended in 1950?
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI1Jvb2ZTdHlsZTogVHlwZSBvZiByb29mXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoUm9vZlN0eWxlKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
#RoofStyle: Type of roof
train %>%
  group_by(RoofStyle) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6Nn0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVN2VXZEUUJTLzVzUFNGRXVoZEhFb0RuWFMxQ29xamllSWRSRkVsK0oyVFZJTnBuYzFTYXR1RmFHamkxQkJjTkRCd2FudWd0MGMvQWRjbk1RSy9RdkV3WHFYNUZLYjRlNjkrNzNQMzd1M3MxNWVWTW9LQUVBQW9oUURna2hWU2FCWERFZ2d3ZVFKQUdLR29WUk9Vam5oR1ZrQUJYd2N5RDQrRmpoaEdVM0RjcWlXOXF3K0ttMVl5QTEwdVlRcWxoRTg0aVZVcTlpR0ZUekZUYlBPTFZzSU84aldlWWJkQTBPUDFKSTFDem04Vk5oQUZXa3VzYW4yU3c5dm5VcXBRV1dTT3VaWTlvQktpdGxobnZUM3pnYWZjSG03OXZ3NGRRR0xhcjdUdWkvQnBlL3FaYzk1aDhYWnVjN1ROWUF6bWJmMDZ2bERHRGY5OHBVOXVvSndVZWgxNTVJaW5GL3J0clBaUGx6NHlMeVNtelpVQjduYlFlNXVGTWZhRjRlUmpoVWR1YWhRdFZITmlCTEVGT01FcFFCTTdCQlMzWFZQd3huS0dtbGdQbDBSTmZmNUpHcUdiaUljeVptd3lYR0I1MlhqRVZyMEdnNkhQLzdJeHB6anBPNmFCRk5YSVJOOCtQL09ZM1lFU0Rjd1M2MnIya0VESDZwTEs0eGVzRGtncUJjYmZZbW5TMzVOaVk5RjV1MGJlTi9FSVVrTFZjSTFTVkVPSG9WQzNUWkQ2Z3BGbllKTFhNVDlGSTFZSFBIMzRmY1BtMEpLaVBzQ0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["RoofStyle"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Flat","2":"13","3":"10.21855","4":"8.390435"},{"1":"Gable","2":"1141","3":"21.31417","4":"18.010753"},{"1":"Gambrel","2":"11","3":"16.17634","4":"15.628300"},{"1":"Hip","2":"286","3":"20.97032","4":"17.887021"},{"1":"Mansard","2":"7","3":"16.16865","4":"14.957265"},{"1":"Shed","2":"2","3":"10.53876","4":"10.538758"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[6]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogUGFzcy4gTm90aGluZyB0byBkaWZmZXJlbnRpYXRlIGJldHdlZW4gdG9wIDIgdmFsdWVzXG5gYGAifQ== -->

```r
# Conclusion : Pass. Nothing to differentiate between top 2 values
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI1Jvb2ZNYXRsOiBSb29mIG1hdGVyaWFsXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoUm9vZk1hdGwpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZiksXG4gICAgICAgICAgICBtZWRpYW4gPSBtZWRpYW4ocHNmKSlcbmBgYCJ9 -->

```r
#RoofMatl: Roof material
train %>%
  group_by(RoofMatl) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6OH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFHV0JHa0FDa0RFR1ZpQm1BMkkyU0h5S0FhdzVhU1dwZVlVQTFrQ1lGbUlLTHR6VG1WSVprNHFuSnVmV3hDY2tRN2orcWJtSmhVbDVrRzVyTDZwSllrNVVBNUxVSDRPak0wZWtsaWs1bDVVQnVPR3B3Um5KR2FuSW5QejBuUFFITVNhbkpOWURITVAzSlZwaWNrbCtVVkExajhnUnZJbjZ5eW9mMkdZRzhtL2ZDQjFEaXljZktIQjg1YzdtSnFGczdxeXNqdEliT0VYalhQdGRWQTQvbHkwY0xxRGc0YmErVXYzdHBjNHFNNXplZmk5WksyRGdXekQ2cnFYU2c3RzJvcXpYNW5NeFRESDhQbFpSdFhDSXB6bUtEWnF1TVUyTXpub243YTA5bHhYNEdDOEljNmo5TDhQeEp2TS85Rjh4cFdTV0pLb2wxYVVtSnVLSGhCNVFERllRTEJBQlRtQzh2UFRmQk5MY3VDaGxWK2FWd0xsTUNlV3dhS0lMVGMxSlJNWVE2aEdjaGJsbCt2QmpBV0ZJbE1Ea1BqLy8vOFBTTWlpS0diUEx5akp6TThES21VU2hnWXFzc01aaTlBRUJFcnpRRWFuNkNabmxPWmw2NXFZZzN3SGpSVUdxSDJNMEppRHNWa2dkckxBUW9VVjV2elV2UFRNUEZoS1ljMUpURXFGK1pnUDZBZXdGL1FLaWpMaFh1Y0NpaGJybGVRakVpSlhjbjRPVEFTU2JQNEJBRFpxdFg5UEF3QUEifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["RoofMatl"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"ClyTile","2":"1","3":"2.504422","4":"2.504422"},{"1":"CompShg","2":"1434","3":"21.212265","4":"17.905472"},{"1":"Membran","2":"1","3":"6.175839","4":"6.175839"},{"1":"Metal","2":"1","3":"8.390435","4":"8.390435"},{"1":"Roll","2":"1","3":"12.075804","4":"12.075804"},{"1":"Tar&Grv","2":"11","3":"10.809119","4":"8.752260"},{"1":"WdShake","2":"5","3":"16.115245","4":"15.896921"},{"1":"WdShngl","2":"6","3":"19.168482","4":"19.688939"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[8]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI0NvbmNsdXNpb24gOiBBZ2FpbiBtb3N0IG9mIHRoZSB2YWx1ZXMgYmVsb25nIHRvIG9uZSBjYXRlZ29yeSBvbmx5IFxuYGBgIn0= -->

```r
#Conclusion : Again most of the values belong to one category only 
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI0V4dGVyaW9yMXN0OiBFeHRlcmlvciBjb3ZlcmluZyBvbiBob3VzZVxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEV4dGVyaW9yMXN0KSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
#Exterior1st: Exterior covering on house
train %>%
  group_by(Exterior1st) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6MTV9LCJyZGYiOiJINHNJQUFBQUFBQUFCZ3R5aVREaWl1QmlZR0JnWW1CbVlXUmdZZ1l5V1ppQUJDTURDd01uaUs1Z1lHQVdCb2tDYVY0Z3pRK1dCR2tBQ2tERUdWaUJtQTJJMllHWUE0aEJHa0dHY2dNeER4Q0Q5UEZCOUtJWXpwYVRXcGFhVXd4a0NZQmxJYUxzanNWSndSbDU2UWh1UVFhUUQrTTZGV1U3NStmbUluSGRFcE5UWVNZNk8rWGtKMmZESkoxVGMvTktuRkpnWEk4VXAvekVJampYTXplNHBEUTVHY2IxVFMxSnpBbUd5d2JrVkpibjU4TzRyTUVsK1hsd1c4RDY4bUVxd3pMektwRTBocWNvQktjZ25CK2VFcHlSQ2VTaWVwMDFPU2V4R09aemVIaWtKU2FYNUJjQldmK2dvUVlLYlJHa0VEZUNzbTJCK0I2VWZRZUljNkR5a2d5UU9Ed0h4Rkt3VUhmUWJiVm9sdUZ0ZFZDSk50Sklablp5a0prZGRTdzQrNHlERVplbFY4TFpVQWZqd3VNeVFPVGdXTGZDNzhMRElBZmorQ01CcXpyZEhFelplcmROOXBWeU1MM2YwLzV0V3FtRGtTanpTb1g2bHc2R0dSTE9mbHY0SFl5bVMzOW9hZHJuWUg1b2dzUEgyc1VPZWlGdHR6Nkh4RGtZUEk4ckU0cFhnOXV2TFhDbEpuaHhFS2I5eXNtVE4wc2NnTnR2ZndZRXpqb1lGQmxxTEZneEEyNi9RWFAwWXJrSlN4d01ST2NVM05TUWdkdXYvK2FvOUpJVnpnNW1ERXR6SG1uZGRkQjVxaFhNbkNUa29QL3c5TFkxUFg2UUlHZitqeGJLWENtSkpZbDZhVVdKdWFub2taSUhGSU5GQ2d0VWtOdTFvaVMxS0RPL3lMQzRCQjU1K2FWNU1BNXpZaGtzcnRseVUxTXlFL1BRVE9Vc3lpL1hnNWtNaWxTbUJpRHgvLy8vajVDSVJsSE1ubDlRa3BtZkIxVEtKQXpOV2NodVp5eENFeEFvelFNWm5hS2JuRkdhbDYxcllnSE5lcUNFd1FDMWp4R2FrR0JzRm9pZExMQ0FZWVU1UHpVdlBST2V5Rmx6RXBOU2M2QWNQcUFmd0Y3UUt5aktoSHVkQ3loYXJGZVNEOHczTUpIay9CeVlDQ1FWL3dNQTVURlZSMlFFQUFBPSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Exterior1st"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"AsbShng","2":"20","3":"14.760197","4":"13.532871"},{"1":"AsphShn","2":"1","3":"10.178117","4":"10.178117"},{"1":"BrkComm","2":"2","3":"7.151713","4":"7.151713"},{"1":"BrkFace","2":"50","3":"18.039937","4":"18.138238"},{"1":"CBlock","2":"1","3":"19.444444","4":"19.444444"},{"1":"CemntBd","2":"61","3":"34.989511","4":"31.800000"},{"1":"HdBoard","2":"222","3":"19.374089","4":"16.446063"},{"1":"ImStucc","2":"1","3":"21.025600","4":"21.025600"},{"1":"MetalSd","2":"220","3":"21.873238","4":"16.513117"},{"1":"Plywood","2":"108","3":"18.082087","4":"16.084418"},{"1":"Stone","2":"2","3":"17.406620","4":"17.406620"},{"1":"Stucco","2":"25","3":"18.590270","4":"15.962441"},{"1":"VinylSd","2":"515","3":"23.760014","4":"22.002524"},{"1":"Wd Sdng","2":"206","3":"15.165091","4":"14.447589"},{"1":"WdShing","2":"26","3":"16.903785","4":"15.941007"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[15]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEV4dGVyaW9yMXN0LCB5ID0gcHNmLCBmaWxsID0gIEV4dGVyaW9yMXN0KSkgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKSArXG4gIGNvb3JkX2ZsaXAoKVxuYGBgIn0= -->

```r
ggplot(train, aes(x = Exterior1st, y = psf, fill =  Exterior1st)) +
  geom_boxplot() +
  theme(legend.position = "none") +
  coord_flip()
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI0NvbmNsdXNpb24gOiBJbnRlcmVzdGlnbiBmZWF0dXJlXG5gYGAifQ== -->

```r
#Conclusion : Interestign feature
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI0V4dGVyaW9yMm5kOiBFeHRlcmlvciBjb3ZlcmluZyBvbiBob3VzZSAoaWYgbW9yZSB0aGFuIG9uZSBtYXRlcmlhbClcbnRyYWluICU+JVxuICBncm91cF9ieShFeHRlcmlvcjJuZCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
#Exterior2nd: Exterior covering on house (if more than one material)
train %>%
  group_by(Exterior2nd) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6MTZ9LCJyZGYiOiJINHNJQUFBQUFBQUFCZ3R5aVREaWl1QmlZR0JnWW1CbVlXUmdZZ1l5V1ppQUJDTURDd01uaUs1Z1lHQVdCb2tDYVY0Z0xRQ1dCR2tBQ2tERUdWaUJtQTJJMllHWUE0aEJHa0dHY2dNeER4Q0Q5UEVCTVQ5RVA0b0ZiRG1wWmFrNXhWQ1RCYUNpN0k3RlNjRVplZWtJYmtFR2tBL2pPaFZsS3pqbkluUGRFcE5UWVNZNk8rWGtKMmZESkoxelUvTktuRkpnWEk4VXAvekVJampYTXplNHBEUTVHY2IxVFMxSnpBbUd5Ykw2bDJTa0ZzSGtBbklxeS9QejRYTEJKZmw1Y0N2Qmh1VERWSVpsNWxVaVRHRVBUMUVJVGtINEJjUUZlUTAxSEZpVGN4S0xZY0VBRDV5MHhPU1MvQ0lnNng4MEdFR3lJdENnQndXM0pEUTZiSUQ0UERUWXIwSEYrcUJSSXdYay9nRFNSNEZZRFJvVkFnNjZQQmtyZnYxTWROQ2NLblIyK3RwckRoNVcyV0hQM25BNkdENlJ6M2o4NTY2RGNlRnhHU0J5Y0x5K0pzRnRvcmFEY2MvY0dSMzExZzVXUDlObVoxaGVjVENUaWN2Nm1pcnZZR001ZjRQTDdYTU91ai9ZVGsvTWlYVFEzcUhTZW5iM2NnY2pGc09qMjVzT09KaFg4VmQvdWJ2UlFWOTZTZkI1OXRrT1p2NVRZaEorMzRhN1EydHl5UWVqaVVrT1dwWFA1d0dSUXdDVDNZUCtIU29PaHMrMit6TnJpc0hkNGFENlhhM3YxbFlIZy9TOEpwYllSQWZUVFhxYk15TnVPQmkwZzZTTDRPN1FTMjZiMDcxK2tvTW1BeGc0Nkc5aDNtczEvNCtENmZ2bmVVZURIQngwVjV4VGZQcWgxY0hBUW5EN1pOOUZrR2hnL284Vzhsd3BpU1dKZW1sRmlibXA2QkdWQnhTRFJSUUxWSkRidGFJa3RTZ3p2OGdvRDU1QWt2Tkw4MHFnSE9iRU1sajhzK1dtcG1RbTVxR1p5bG1VWDY0SE14a1UwVXdOUU9MLy8vOGZJSkdQb3BnOXY2QWtNejhQcUpSSkdCckh5RzVuTEVJVEVDak5BeG1kb3B1Y1VacVhyV3RxQUUwb2pKQWdBdHZIQ05VRFk3TkE3R1NCQlF3cnpQbXBlZW1aOElUUG1wT1lsSm9ENWZBQi9RRDJnbDVCVVNiYzYxeEEwV0s5a254Z3hvS0pKT2Zud0VRZ0tmc2ZBQnNLYWxlSkJBQUEifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Exterior2nd"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"AsbShng","2":"20","3":"14.52424","4":"13.28800"},{"1":"AsphShn","2":"3","3":"12.79116","4":"13.23810"},{"1":"Brk Cmn","2":"7","3":"48.45640","4":"64.03509"},{"1":"BrkFace","2":"25","3":"17.89110","4":"17.90123"},{"1":"CBlock","2":"1","3":"19.44444","4":"19.44444"},{"1":"CmentBd","2":"60","3":"35.68495","4":"32.29660"},{"1":"HdBoard","2":"207","3":"19.54928","4":"16.40403"},{"1":"ImStucc","2":"10","3":"26.97422","4":"21.69603"},{"1":"MetalSd","2":"214","3":"22.11082","4":"16.52778"},{"1":"Other","2":"1","3":"28.22509","4":"28.22509"},{"1":"Plywood","2":"142","3":"14.98443","4":"15.19439"},{"1":"Stone","2":"5","3":"13.85965","4":"12.50000"},{"1":"Stucco","2":"26","3":"18.01638","4":"15.85159"},{"1":"VinylSd","2":"504","3":"23.47680","4":"21.93713"},{"1":"Wd Sdng","2":"197","3":"15.55399","4":"14.82970"},{"1":"Wd Shng","2":"38","3":"22.31086","4":"16.21902"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[16]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEV4dGVyaW9yMXN0LCBFeHRlcmlvcjJuZCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSkgJT4lXG4gIGFycmFuZ2UoZGVzYyhjb3VudCkpXG5gYGAifQ== -->

```r
train %>%
  group_by(Exterior1st, Exterior2nd) %>%
  summarise(count = n()) %>%
  arrange(desc(count))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbImdyb3VwZWRfZGYiLCJ0YmxfZGYiLCJ0YmwiLCJkYXRhLmZyYW1lIl0sIm5jb2wiOjMsIm5yb3ciOjY3fSwicmRmIjoiSDRzSUFBQUFBQUFBQnNWVXpXN1RRQkJlcitPaytiT0RpZ1RIdkVBanRSSW5Uc1JRd1FHQnNFUjd4TFczalJWN043STMvYm54U2p4QUQ3d0R6OEt4WVd6UE9Cc3JTQVVoY2ZpOE96ODdzelB6clQrOVBqOFpuQThZWTV6WkhZdHhHN1lkRGgrTGRWaS9YRzhac3c5aEF4WjdES3NQS05mUzJBTzRnREpBdHp5SnVsRVZnREVQZFM2aWc3NWp3OVpIM1FoOXJEcFhFNHZzZEk1aWVlakwwWmZnNEYyNmVON0VBY1lqREJFanhQZzNjUGZBcTdIVHJHNHFya1Zhd0c1U1dXdHQ3MVZ4RVN6azFWWmNMVUFtY1o0dmZaVmxobmdhUm9JaSt2TlVSVXN5K2lLVGVoNlQrRGFlcXpCdnhIZFpvTmRSUk9KN29jTTBhS3dmMDdzYnBVaDBBcTFrazZVNnA4anpjeUx2aklObjhUU0l0OWMvaTRORkF1SnU2VTZVaGdWVjN2VGpNb3kweW1IM1lMREhOZGpqNFFTSVBVUHN1Tlgwc0Y1cFVyWWhtMU9kNEVvK0k1UzlWaDVpYkEvemNNdzF4aGlPa1pQalBUMGpQamQ4aWVsZHRtVTgzY2RrdWNXMlREZFpodXpoRzR3M2VUUmZwbjRtSDhlWFRQd3RYNXdQZWlIeWYwK2VhVlZhVmJsTmxlL2xDME8rV0Q5aC9RSDREdmdHK0FKNENYZ09lQVo0Q25pQ0dHR2ZEM0F1amdGN0QvZ2Z3UHIvMk51MVFSenFjSGFaaDVsb1Awb0pPbnFVTmlxSGIyNjF5Qk9WSHhlNnJUcVJ6WWdqdFphNkZhK2ZxNXNaeGF5ZXoxZjRiRGFiKzNwa084NDl0ZEtKa3VES0QzRUM1cTJ0dktXWXJHVVpPajZLRm11NVBIcHh6T3BuVkpiTzJQYTM0QnQ3dTg3Wm9aWTRSQ1FocjVLR29VNGFYb2dVQlJkcXFFcVlyZkpFVWdjR29DMW1Xc0VMSUUya1V0TFVmSHo0Qlh3cGh0SXVCd0FBIn0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Exterior1st"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["Exterior2nd"],"name":[2],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"VinylSd","2":"VinylSd","3":"502"},{"1":"MetalSd","2":"MetalSd","3":"212"},{"1":"HdBoard","2":"HdBoard","3":"193"},{"1":"Wd Sdng","2":"Wd Sdng","3":"177"},{"1":"Plywood","2":"Plywood","3":"96"},{"1":"CemntBd","2":"CmentBd","3":"59"},{"1":"BrkFace","2":"BrkFace","3":"24"},{"1":"HdBoard","2":"Plywood","3":"23"},{"1":"Stucco","2":"Stucco","3":"20"},{"1":"AsbShng","2":"AsbShng","3":"17"},{"1":"WdShing","2":"Wd Shng","3":"17"},{"1":"BrkFace","2":"Wd Sdng","3":"12"},{"1":"Wd Sdng","2":"Wd Shng","3":"9"},{"1":"Wd Sdng","2":"Plywood","3":"8"},{"1":"BrkFace","2":"Plywood","3":"6"},{"1":"Plywood","2":"Brk Cmn","3":"5"},{"1":"VinylSd","2":"Wd Shng","3":"5"},{"1":"WdShing","2":"Plywood","3":"5"},{"1":"BrkFace","2":"HdBoard","3":"3"},{"1":"MetalSd","2":"HdBoard","3":"3"},{"1":"Plywood","2":"ImStucc","3":"3"},{"1":"Stucco","2":"Wd Shng","3":"3"},{"1":"Wd Sdng","2":"ImStucc","3":"3"},{"1":"AsbShng","2":"Plywood","3":"2"},{"1":"BrkComm","2":"Brk Cmn","3":"2"},{"1":"BrkFace","2":"Stone","3":"2"},{"1":"HdBoard","2":"ImStucc","3":"2"},{"1":"MetalSd","2":"Wd Sdng","3":"2"},{"1":"Plywood","2":"HdBoard","3":"2"},{"1":"Plywood","2":"Wd Sdng","3":"2"},{"1":"VinylSd","2":"Plywood","3":"2"},{"1":"Wd Sdng","2":"HdBoard","3":"2"},{"1":"Wd Sdng","2":"VinylSd","3":"2"},{"1":"WdShing","2":"HdBoard","3":"2"},{"1":"AsbShng","2":"Stucco","3":"1"},{"1":"AsphShn","2":"AsphShn","3":"1"},{"1":"BrkFace","2":"AsbShng","3":"1"},{"1":"BrkFace","2":"Stucco","3":"1"},{"1":"BrkFace","2":"Wd Shng","3":"1"},{"1":"CBlock","2":"CBlock","3":"1"},{"1":"CemntBd","2":"Wd Sdng","3":"1"},{"1":"CemntBd","2":"Wd Shng","3":"1"},{"1":"HdBoard","2":"AsphShn","3":"1"},{"1":"HdBoard","2":"MetalSd","3":"1"},{"1":"HdBoard","2":"Wd Sdng","3":"1"},{"1":"HdBoard","2":"Wd Shng","3":"1"},{"1":"ImStucc","2":"ImStucc","3":"1"},{"1":"MetalSd","2":"AsphShn","3":"1"},{"1":"MetalSd","2":"Stucco","3":"1"},{"1":"MetalSd","2":"Wd Shng","3":"1"},{"1":"Stone","2":"HdBoard","3":"1"},{"1":"Stone","2":"Stone","3":"1"},{"1":"Stucco","2":"CmentBd","3":"1"},{"1":"Stucco","2":"Stone","3":"1"},{"1":"VinylSd","2":"AsbShng","3":"1"},{"1":"VinylSd","2":"HdBoard","3":"1"},{"1":"VinylSd","2":"ImStucc","3":"1"},{"1":"VinylSd","2":"Other","3":"1"},{"1":"VinylSd","2":"Stucco","3":"1"},{"1":"VinylSd","2":"Wd Sdng","3":"1"},{"1":"Wd Sdng","2":"AsbShng","3":"1"},{"1":"Wd Sdng","2":"BrkFace","3":"1"},{"1":"Wd Sdng","2":"MetalSd","3":"1"},{"1":"Wd Sdng","2":"Stone","3":"1"},{"1":"Wd Sdng","2":"Stucco","3":"1"},{"1":"WdShing","2":"Stucco","3":"1"},{"1":"WdShing","2":"Wd Sdng","3":"1"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[67]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogRXh0ZXJpb3IgMm5kIGlzIGVxdWFsIHRvIDFzdCBpZiBib3RoIGV4dGVyaW9yIGFyZSBzYW1lLlxuYGBgIn0= -->

```r
# Conclusion : Exterior 2nd is equal to 1st if both exterior are same.
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBNYXNWbnJUeXBlOiBNYXNvbnJ5IHZlbmVlciB0eXBlXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoTWFzVm5yVHlwZSkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
# MasVnrType: Masonry veneer type
train %>%
  group_by(MasVnrType) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFxV0JHa0FDb0RFR3hnWTBEV3g1YVNXcGVZVUExa0NZQjFRVWFlaWJPZmNQQ2lQSGNoelMweE9oWEpaL1BMellHelc0QklRaDRHQjh6OFFvSm5ObXB5VFdBd3pHbTVoV21KeVNYNFJrUFVQaUdITzVBY3EyQXQwWlFLUURYSWxCeER6Z2VRY05IWUZKVmpJUFhBdy8zcXllVXFobW9OUnQvYnRpWVhoRGpaMzVrbFhNS1U0V0p6Y2R5aWhxZ0t1WHFmNDVwR0k1M1lPeG52bHJoMzhIT2Rna0g0bDdPVEJCdzVXazYyMWRMUDNPMWpxM1d0OXVoUWFETXovMFZ6SGxaSllrcWlYVnBTWW00cnVtVHlnR013ekxERGx2b25GWVhsRklaVUY4QUJKemkvTks0RnltQlBMMG1IZXprMU55VXpNUXpPVXN5aS9YQTltTUNnc21FQ2VCNGJrYjBqNG9DaG16eThveWN6UEF5cGxFb1lHRzdMVEdZdlFCQVJLODBCR3ArZ21aNVRtWmV1YUdvRWNERTBTREZEN0dLRUd3ZGdzRUR0WllPRUNUeENwZWVtWmlGalBTVXhLellGeStJQitBSHRCcjZBb0UrNTFMcUJvc1Y1SmZra2lUQjFYY240T1RBUVMrZjhBcDJ6UElOUUNBQUE9In0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["MasVnrType"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"BrkCmn","2":"15","3":"12.36391","4":"14.22627"},{"1":"BrkFace","2":"445","3":"23.96011","4":"19.73875"},{"1":"None","2":"864","3":"18.54364","4":"16.40558"},{"1":"Stone","2":"128","3":"28.86179","4":"26.57512"},{"1":"NA","2":"8","3":"24.78807","4":"25.18308"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[5]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IE1hc1ZuclR5cGUsIHkgPSBwc2YsIGZpbGwgPSAgTWFzVm5yVHlwZSkpICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIilcbmBgYCJ9 -->

```r
ggplot(train, aes(x = MasVnrType, y = psf, fill =  MasVnrType)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBOZWVkIHRvIHJlcGxhY2UgbnVsbCB2YWx1ZXMgd2l0aCBub25lXG5gYGAifQ== -->

```r
# Need to replace null values with none
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI01hc1ZuckFyZWE6IE1hc29ucnkgdmVuZWVyIGFyZWEgaW4gc3F1YXJlIGZlZXRcbnRyYWluICU+JVxuICBnZ3Bsb3QoYWVzKHggPSBNYXNWbnJBcmVhKSkgK1xuICBnZW9tX2hpc3RvZ3JhbShiaW53aWR0aCA9IDUwKVxuYGBgIn0= -->

```r
#MasVnrArea: Masonry veneer area in square feet
train %>%
  ggplot(aes(x = MasVnrArea)) +
  geom_histogram(binwidth = 50)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzEsIlJlbW92ZWQgOCByb3dzIGNvbnRhaW5pbmcgbm9uLWZpbml0ZSB2YWx1ZXMgKHN0YXRfYmluKS4iXV0sImhlaWdodCI6NDMyLjYzMjksInNpemVfYmVoYXZpb3IiOjAsIndpZHRoIjo3MDB9 -->

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArwAAAGwCAMAAAB8TkaXAAAA0lBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZrY6AAA6ADo6AGY6OgA6Ojo6OmY6ZmY6ZpA6kLY6kNtZWVlmAABmOgBmOjpmZgBmZjpmZmZmZpBmkJBmkLZmkNtmtttmtv+QOgCQZjqQZmaQkDqQkLaQtpCQtraQttuQ2/+2ZgC2Zjq2kDq2kGa2tma2tpC2tra2ttu225C229u22/+2/7a2///bkDrbkJDbtmbbtpDbtrbb25Db27bb29vb2//b/7bb////tmb/25D/27b/29v//7b//9v///8cYTCmAAAACXBIWXMAAA7DAAAOwwHHb6hkAAAM9ElEQVR4nO3dD3/TxgGHcdk0NiPQeYaxji5ut1HENmjLosFKusip7ff/lnZ3Ovmv4pwdnXw/8nw/HxxjwnERD8pZskW2AERlp54AcCzihSzihSzihSzihSzihSzihSzihay24uUfATpHvJBFvJBFvJBFvJBFvJBFvJBFvJBFvJBFvJBFvJBFvJBFvJBFvJBFvJBFvJDVSbx/2NbSH4qHjXghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghi3ghKyjeMqtcLGZj+3FQPdZ7EzgO8SKG8D3vbGyanT72wZam3HKtXuJF58LjLfqXpll7Y8wnI3ObD8LGIV7EEBzvdGhzLQb1zy4WvueAcYgXMQTHm7tQ83Oz5B3Vywe/H3br4X2/l3gRQ2i8s/HI3Z5dm4JHfrm7tuglXnQuNN71J2dmh0u8OL3QeHO7y/XMgndj2XDnOMSLGALjrVYNnimXJ2w4vcB4q1j9B7PD5VAZTi8w3np163I1T9g4SYHTC4x3uUDI3Vli+winh3FivDAHsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXsogXssLinY0zY2DulVnWe7NYvxMwDvEihrB4p499p6UJ1v5Y3QkZh3gRQ1i8Zf/SfZxPRuY2H6zuBI1DvIghLN7CVzodXtif9S+Xd4LGIV7E0BDd7MVT1+R8smwzPzdL3lG9fDD74eWdPeOsEC9i2Inu6urzuP/zlfFpWLc5G59dm4JHfpVrbpd33BjWvj+EeBHDdnTVcQXPJrti9rPN8TaNs4F4EcNOdDfv3w17r99bP260axe8LBuQkIbo5t9/c737qFvw8oQNCQk62lClavazHCpDQpqj++3K+bX+uavUPGHjJAUS0hTd7Ll/wrZaFeTmZ3bvuyjqs8IFp4dxYk3R5VnvVdMztkPHWSJexNB0kmK8vks9fpwV4kUMjfGulgv3GWeFeBFD06GyCXteKGiKbjo8+9DGOEvEixgalw3ZztGGY8ZZIV7E0HiG7U9e85m20HFWiBcx8B42yCJeyGqKzp8cXjs9fNw4S8SLGHjCBllNT9j+a08Nv3vZe8XpYaRsT3RF76KVcYgXceyJrnrn2v3HIV7EsTde1rxI2e3Rzf+RsedFyvYebWDNi5TtOT38zc/3G2eFeBEDZ9ggi3ghqzm6Ty/Pz5/9cP9xPOJFDE3RzSdZ1htuX+3p8HGWiBcxNEVXZF99WCxuntvrQt5nnCXiRQx73sM2HXKcFynb8+5hzrAhbXuu2zAdEi9S1nzFHLfYLbJBwy8eMM4S8SKG5re+Z09fv3uRHXL5BuJF5xqju3FX2vvqkIs3EC86d0t086urAw7y3j5OhXgRA6eHIWvP63kPeO8w8eIEGk8Pv7XHyA56FxDxonvNp4dttvO3HCpD0vacpOAMG9LG6WHIanxhTvXmtZI3YCJpTdGVWfbs9buXvAETaWuM7tMTd4bth/uOUyNexMAZNsjiDBtkES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9khcU7n2RZNjJ3ZmP7X2oPFu6/hu+9CRyHeBFDULzziem0sM1OH/tgS/NIuVYv8aJzQfFOhxfmtuhfLkrzw5pP7H44H4SNQ7yI4YA1r93RFj7XVc4h4xAvYjgg3tykmp9Xi99q+eD3w3YZTLzoXHi8pYl2Nj67NhWP/HJ3bdFLvOhccLxltlzgmh0u8eL0QuMt3ZGyilnwbiwb7hyHeBFDYLzFWrt2wcsTNpxeWLxFduE+Vs2aHS6HynB6gcd56/2uy9U8YeMkBU4vKN7CHQxzp4Nz8/HCP8bpYZwUL8yBLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFLOKFrETiJW8cjnghi3ghi3ghi3ghK9V4qRl3Il7IkomXmrGNeCGLeCGLeCGLeCGLeCFLN15qfvBOE28ULX0lkEG8kPUFxUvNDw3xQhbxQhbxQhbxQtaXHO+Olr5WJIJ4IYt4IYt4IYt4IYt4Iethx3v3ZyBhDyreu7W0NdAJ4t3Q0tZAJ4h3Q0tbA50g3g0tbQ104uh4yyzrvQkc59RJ3sPdG+KI34J2HBtvacot1+r9UuM9wt1f/pHbHFuOjHc+GZnbfBA2zgkKOqG7v/zjtjm2HRnvdHhhbov+ZdA4JyjohKJ8+QF/J0dMJGDUlB0b72O7YiireDOrxTkBQY6Mrlruri16iRedI17IamPZcI9xgON18oQNiKGTQ2VADJ2cpABiODq64oDTw0AMnbwwB4iBeCGLeCGLeCGLeCGLeCGLeCGLeCGLeCGrtXiBjrQeb1jhXf5h96Mz1Qc8U+JtpjPVBzxT4m2mM9UHPFOdLx3YQryQRbyQRbyQRbyQRbyQ1V28W9dETc9sbE/f2DdEL6ea5pynv3NXHNidZXLTrWYabcN2Fu/2243TU11IZbE21TTnPBu7y2XszjK56fqZRtuwXcW7c6GH9NTX/1lONc05m52WnejuLJObrp9pvA3bVbw7l9hJT+E35nKqSc65zEYuht1ZpjbdeqbxNmxn8W5f3Cw9+blZmY3WpprqnKt4d2aZ4HSryUTbsF3Fu3NZyeTMxmfXZkOPVlNNdc7ub313lglO18003oYl3k1mc6dcgyMW7/KubLwJfk9rZJZjKX8fdtSWDU6MDcsTtk1muyb7DKgm8oRtsRlvhA3LobJatUXN5k732JNXihwq2/hnFmPDcpJiyW1M87wi4aP+lVLlJEV9tCHWhu3u9HCR2rnLHXmWZXYnsZpqmnP234x3Z5ncdP1MY21YXpgDWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcTbmvzp367dnfl/XoyaPsG/pWvr7rr5JK0zZIkj3tbk/hyofe9WY7zmM+rHi+bPmA5v+Z1oQrytyXtPqtdJ5Y+GzQlOh2d+33zLHjbv/zGlVzSmjnhbk/f/2q8uU/DnW+JdNjsdNr4ccDYefPR7bwQg3tbk/Z/8K1d/cvF+fJJlvVdmVzt/O8yypx8Wq9VCbhKdT85+eZ71vrVND4qs/8GuNy6qN3wtH7r5zo+xNhxqxNuavP/vsXuR9dkvNt6i+g8URtUrAquXAPo03Yf5pP6E+eTRMHOPmD137nbO/iGzBq4vNrMaDjXibU3ev8xNgrPxaGrinY3tvnRqMq2K/ei6q9Is7X0T7+DaNGnfWFA1aX+bX1H4h/Ls96bpt2Y/vRrulF9iYoi3NXn1/ljzY1qtea/ef/8ks/H2vn7/a/U5Lk23h/W3tuzqni97/Rf90tisIdaGO80XlyTibY2J1+x1zarh2u9C3ff5s+vqO361XHVR1jtXG6K9re7569FVS4PqIT+EG2Q1HGrE25rcvsXw7H+m32rZkD179eNn933+83fL7gqzBKiXtVvxltkq1a147T+L1XDwiLc1Jt5F0fv74zcu3tId85rVtf326blLdjYeLA8obMZbLx7qQxHXfhFc2RoOFvG2JncrgnN3a+M1T8dunrtDBgOz4r3xx3jz/r+qQ7nb8S6P/do79S/2vrXP9cwDq+FO9wUmh3hbY+O1hxAW9bLBf8f3h8qyqk2zFKj2sNvxFvXpCXsqw68k/LrBZL82HGrE2xobr/ueX327N7vJ7NFf7Pp2/s+hvVt9Vn1cbDvetZfqFNnIx+tOUmRf2/Mbq+FQI17IIl7IIl7IIl7IIl7IIl7IIl7IIl7IIl7IIl7IIl7IIl7IIl7I+j/JBoblOyJQyAAAAABJRU5ErkJggg==" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdncGxvdChhZXMoeCA9IE1hc1ZuckFyZWEsIHkgPSBwc2YpKSArXG4gIGdlb21faml0dGVyKGNvbG9yID0gXCJyZWRcIiwgYWxwaGEgPSAwLjMpICtcbiAgZ2VvbV9zbW9vdGgobWV0aG9kID0gXCJsbVwiKVxuYGBgIn0= -->

```r
train %>%
  ggplot(aes(x = MasVnrArea, y = psf)) +
  geom_jitter(color = "red", alpha = 0.3) +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzEsIlJlbW92ZWQgOCByb3dzIGNvbnRhaW5pbmcgbm9uLWZpbml0ZSB2YWx1ZXMgKHN0YXRfc21vb3RoKS4iXSxbMSwiUmVtb3ZlZCA4IHJvd3MgY29udGFpbmluZyBtaXNzaW5nIHZhbHVlcyAoZ2VvbV9wb2ludCkuIl1dLCJoZWlnaHQiOjQzMi42MzI5LCJzaXplX2JlaGF2aW9yIjowLCJ3aWR0aCI6NzAwfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogbW9zdCBvZiB0aGUgdmFsdWUgYXJlIDBcbmBgYCJ9 -->

```r
# Conclusion : most of the value are 0
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBFeHRlclF1YWw6IEV2YWx1YXRlcyB0aGUgcXVhbGl0eSBvZiB0aGUgbWF0ZXJpYWwgb24gdGhlIGV4dGVyaW9yIFxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEV4dGVyUXVhbCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
# ExterQual: Evaluates the quality of the material on the exterior 
train %>%
  group_by(ExterQual) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRJRFpRRWFRQUtRUGdvR3RoeVVzdFNjNHFCTEFHd0xFU1V5YlVDeG5KTGhMSGNVMkNzRUVjMFUxaVRjeEtMWVliQWpVNUxUQzdKTHdLeS9nRXh6REVtUU13SFZQUUM2SjR1Q0p1QnhjSE8yTUx0dmxLTGc5cTB1by8vZCsxd3NOcHZkVmluVGNYQmNQRU0rOVZodlhCMXRwNHFBaE9tN0hkUXZoMFY5N3hsdllONTBFeXBaZFlISFBTOW05NXVOWjBIY1JiemZ6U1hjS1VrbGlUcXBSVWw1cWFpT3p3UEtJYnVlMDdYaXBMVW9zRFN4Qnk0OS9KTDgwcWdIT2JFc25TWUQzTlRVeklUODlETTVDektMOWVEbVF2eU5sTURrUGovLy84ZlNGQ2dLR2JQTHlqSnpNOERLbVVDUlJzcm1zc1ppOUFFQkVyelFFYW42Q1pubE9abDY1cWFnYndIaldNR3FIMk0wS0JHWW9Qc1pJRUZDeXZNK2FsNTZabDVxVEJQNWlRbXBjSjh6QWYwQTlnTGVnVkZtWEN2Y3dGRmkvVks4a3ZnSWNPVm5KOERFNEhFOHo4QS9Xa1AwcVVDQUFBPSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["ExterQual"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Ex","2":"52","3":"30.20008","4":"29.285707"},{"1":"Fa","2":"14","3":"11.29394","4":"9.928424"},{"1":"Gd","2":"488","3":"26.74699","4":"23.322649"},{"1":"TA","2":"906","3":"17.63904","4":"15.647483"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[4]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEV4dGVyUXVhbCwgeSA9IHBzZiwgZmlsbCA9ICBFeHRlclF1YWwpKSArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpXG5gYGAifQ== -->

```r
ggplot(train, aes(x = ExterQual, y = psf, fill =  ExterQual)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogRXhjZWxsZW50IGZlYXR1cmUuIENsZWFyIGRpc3RpbmN0aW9uIGJldHdlZW4gdG9wIDIgdmFsdWVzIC0gR29vZCBhbmQgQXZlcmFnZVxuYGBgIn0= -->

```r
# Conclusion : Excellent feature. Clear distinction between top 2 values - Good and Average
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBFeHRlckNvbmQ6IEV2YWx1YXRlcyB0aGUgcHJlc2VudCBjb25kaXRpb24gb2YgdGhlIG1hdGVyaWFsIG9uIHRoZSBleHRlcmlvclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEV4dGVyQ29uZCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
# ExterCond: Evaluates the present condition of the material on the exterior
train %>%
  group_by(ExterCond) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFxV0JHa0FDa0RFUVdJb210aHlVc3RTYzRxQkxBR3dMRVNVeWJVQ3huSkxoTEhjVTJDc2dId1lLOFFSelR6VzVKekVZcGh4Y0V2U0VwTkw4b3VBckg5QURITWF5RWt5UUR3SjRreFdrREY4SURrSHd6T0MxY3BwWFE2YS85Tml6akVjZERDcVVvNDNTdjdxb0ROVFhpb3dvczNCdFBkMXhVWFhNTGg2ZzZPaElPQ2dmcmcyMFhyT2VnZURQL0hYQTRLWHdOVWJTV1EwdkxzN0FlSlU1djlvcnVOS1NTeEoxRXNyU3N4TlJmZE1IbEFNNWhrV3FDQ25hMFZKYXBGemZsNEszTXY1cFhrbFVBNXpZbGs2ek5lNXFTbVppWGxvWm5JVzVaZnJ3Y3dGQlFWVEE1RDQvLy8vYjBqd29DaG16eThveWN6UEF5cGxFb2FHR3JMTEdZdlFCQVJLODBCR3ArZ21aNVRtWmV1YVdvQzhCMDBGREZEN0dLRUd3ZGdzRUR0WllNRUNTd05zcVhucG1YbXBNRS9tSkNhbDVrQTVmRUEvZ0wyZ1YxQ1VDZmM2RjFDMFdLOGt2eVFScG80ck9UOEhKZ0tKKzM4QUZuV3h4OGNDQUFBPSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["ExterCond"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Ex","2":"3","3":"17.79714","4":"16.77083"},{"1":"Fa","2":"28","3":"12.99883","4":"11.88182"},{"1":"Gd","2":"146","3":"18.47710","4":"16.98584"},{"1":"Po","2":"1","3":"14.29907","4":"14.29907"},{"1":"TA","2":"1282","3":"21.55437","4":"18.09534"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[5]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEV4dGVyQ29uZCwgeSA9IHBzZiwgZmlsbCA9ICBFeHRlckNvbmQpKSArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpXG5gYGAifQ== -->

```r
ggplot(train, aes(x = ExterCond, y = psf, fill =  ExterCond)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTm9wZS5cbmBgYCJ9 -->

```r
# Conclusion : Nope.
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBGb3VuZGF0aW9uOiBUeXBlIG9mIGZvdW5kYXRpb25cbnRyYWluICU+JVxuICBncm91cF9ieShGb3VuZGF0aW9uKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
# Foundation: Type of foundation
train %>%
  group_by(Foundation) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6Nn0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFhV0JHa0FDa0RFR1ZnaDRpZ2EyWEpTeTFKemlvRXNBYkFzVk5TcEtEc2tNd2ZHYzNiS3lVL09odkpZQTV6ejg1S2hISmJnbk1Ra21FUndTWDVlS2t3aVBEOC9CYzB1MXVTY3hHS1lWWEFIcENVbWwrUVhBVm4vZ0JqbTlFbEFsMWNCY1R1UUxRRVZBM21ERDhSMjBKL21iV3ZsME9SZ09QZEpCTWVsVXc1V3pFWDFuZTJ5RHBvNnBsRStaL1k2R1BFZTM5Z3g3NENEM3ZvcStRdHpWZUQ2OUNhR0NMTXMzK0dnMTdXNkwrZURtb1Baby9pL2NoRzVEdXJTSzZvN1B6QTU2THZ4MVJ1clJUaG9jL0FiN0lrSmhqaWYrVCthaTdsU0Vrc1M5ZEtLRW5OVDBUMllCeFNEZVpBRnB0d3R2elFQcUNVelB3OGVEa0NSRWlpSE9iRXNIUllVdWFrcG1ZbDVhSVp5RnVXWDY4RU1Cb1VQVXdPUStQLy8veTlJbUtFb1pzOHZBRmtFVk1va0RJMXhaS2N6RnFFSkNKVG1nWXhPMFUzT0tNM0wxalV6QURrWW1uUVlvUFl4UXNNZnhtYUIyTWtDQ3hkV21QTlQ4OUl6NFFtQUZaZ3dVbUVwaUEvb0I3QVg5QXFLTXVGZTV3S0tGdXVWNUpja3d0UnhKZWZud0VRZ0NlSWZBQ2NGQjJuOEFnQUEifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Foundation"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"BrkTil","2":"146","3":"15.79354","4":"15.28384"},{"1":"CBlock","2":"634","3":"17.61677","4":"15.27084"},{"1":"PConc","2":"647","3":"26.01347","4":"22.88428"},{"1":"Slab","2":"24","3":"12.58634","4":"11.55402"},{"1":"Stone","2":"6","3":"18.05383","4":"15.63683"},{"1":"Wood","2":"3","3":"15.34273","4":"13.51574"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[6]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEZvdW5kYXRpb24sIHkgPSBwc2YsIGZpbGwgPSAgRm91bmRhdGlvbikpICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIilcbmBgYCJ9 -->

```r
ggplot(train, aes(x = Foundation, y = psf, fill =  Foundation)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTmljZSBPbmUhIENsZWFyIGRpc3RpbmN0aW9uIGJldHdlZW4gdG9wIDIgdmFsdWVzXG5gYGAifQ== -->

```r
# Conclusion : Nice One! Clear distinction between top 2 values
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210UXVhbDogRXZhbHVhdGVzIHRoZSBoZWlnaHQgb2YgdGhlIGJhc2VtZW50XG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoQnNtdFF1YWwpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZiksXG4gICAgICAgICAgICBtZWRpYW4gPSBtZWRpYW4ocHNmKSlcbmBgYCJ9 -->

```r
# BsmtQual: Evaluates the height of the basement
train %>%
  group_by(BsmtQual) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFxV0JHa0FDb0RFR3hnWTBEV3g1YVNXcGVZVUExa0NZQjBRVVNiWENoakxMUkhHY2srQnNVSWNnU1RuZnlCQU00MDFPU2V4R0dZWTNJcTB4T1NTL0NJZzZ4OFF3eHhXQ2NUS1FMT3lnTGdUeUZZRllqNlFuSU50NGFKamlqLzlISFFuU3diZm1iVER3V0pmbjVyeXh4SUhnenY2UGs4MWNodzBEUDcvNUx6cUQxZHZzM3JWdlQ0dmZRZmRIenRVOWY5TE81am10Q2NjMjJybm9MZktudmUrbVpXRDJ0UE9BT1pIeFJDbk12OUhjeDFYU21KSm9sNWFVV0p1S3JwbjhvQmlNTSt3UUFVNW5JcHpTd0pMRTNQZ1BzNHZ6U3VCY3BnVHk5SmhuczVOVGNsTXpFTXprck1vdjF3UFppd29KSmhBVVFJTXg5K1EwRUZSeko1ZlVKS1pud2RVeWlRTURUUmtoek1Xb1FrSWxPYUJqRTdSVGM0b3pjdldOVE1DK1E2YUJCaWc5akZDRFlLeFdTQjJzc0JDQlpZQTJGTHowalB6VW1HZXpFbE1Tb1g1bUEvb0I3QVg5QXFLTXVGZTV3S0tGdXVWNUpmQVE0WXJPVDhISmdLSituOEF4SVhaQzhRQ0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BsmtQual"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Ex","2":"121","3":"29.44389","4":"28.67058"},{"1":"Fa","2":"35","3":"14.78730","4":"14.98578"},{"1":"Gd","2":"618","3":"24.74436","4":"21.42394"},{"1":"TA","2":"649","3":"16.86010","4":"15.33251"},{"1":"NA","2":"37","3":"12.09570","4":"11.44831"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[5]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEJzbXRRdWFsLCB5ID0gcHNmLCBmaWxsID0gIEJzbXRRdWFsKSkgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKVxuYGBgIn0= -->

```r
ggplot(train, aes(x = BsmtQual, y = psf, fill =  BsmtQual)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogQWdhaW4gc3VwZXJiIHBpY3R1cmUuIE5pY2UgZGlzdGluY3Rpb24gYmV0d2VlbiB0b3AgMyB2YWx1ZXMgXG5gYGAifQ== -->

```r
# Conclusion : Again superb picture. Nice distinction between top 3 values 
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210Q29uZDogRXZhbHVhdGVzIHRoZSBnZW5lcmFsIGNvbmRpdGlvbiBvZiB0aGUgYmFzZW1lbnRcbnRyYWluICU+JVxuICBncm91cF9ieShCc210Q29uZCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
# BsmtCond: Evaluates the general condition of the basement
train %>%
  group_by(BsmtCond) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFxV0JHa0FDb0RFR3hnWTBEV3g1YVNXcGVZVUExa0NZQjBRVVNhM1JCakxQUVhHQ3NpSHNVSWNnU1RuZnlCQU00MDFPU2V4R0dZWTNJcTB4T1NTL0NJZzZ4OFF3eHltQzhTT0VNZXh5Z05wVlNEbUE4azU2R29taE5vNUxuSXdPNXplT2JORXlrRmFycWU2SSt5S2cybjExY05iK3A0NWFCajgvOGw1MVIrdVhydGhwdlBSaWJFT0ppOTI2WFV2ZWdsWGJ5UWFDZ0lPYWs4N0E1Z2ZGVU9jeXZ3ZnpYVmNLWWtsaVhwcFJZbTVxZWlleVFPS3dUekRBaFhrY0NyT0xYSE96MHVCK3ppL05LOEV5bUZPTEV1SGVUbzNOU1V6TVEvTlNNNmkvSEk5bUxHZ2tHQUNSUWt3SEg5RFFnZEZNWHQrUVVsbWZoNVFLWk13Tk5DUUhjNVloQ1lnVUpvSE1qcEZOem1qTkM5YjE4d0U1RHRvRW1DQTJzY0lOUWpHWm9IWXlRSUxGVmdDWUV2TlM4L01TNFY1TWljeEtUVUh5dUVEK2dIc0JiMkNva3k0MTdtQW9zVjZKZmtsaVRCMVhNbjVPVEFSU05UL0F3Q0FyQTljeEFJQUFBPT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BsmtCond"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Fa","2":"45","3":"14.580813","4":"13.751169"},{"1":"Gd","2":"65","3":"22.763299","4":"20.909091"},{"1":"Po","2":"2","3":"6.779833","4":"6.779833"},{"1":"TA","2":"1311","3":"21.483731","4":"18.083333"},{"1":"NA","2":"37","3":"12.095703","4":"11.448313"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[5]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTm90IG9mIG15IGxpa2luZyAuLkxlYXZlIGl0XG5gYGAifQ== -->

```r
# Conclusion : Not of my liking ..Leave it
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210RXhwb3N1cmU6IFJlZmVycyB0byB3YWxrb3V0IG9yIGdhcmRlbiBsZXZlbCB3YWxsc1xudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEJzbXRFeHBvc3VyZSkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
# BsmtExposure: Refers to walkout or garden level walls
train %>%
  group_by(BsmtExposure) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFxV0JHa0FDb0RFR3hnWTBEV3g1YVNXcGVZVUExa0NZQjBRVVNiSE1oakxQUVhHOHMyRHNmenlnU1RuZnlCQU00MDFPU2V4R0dZWTNJcTB4T1NTL0NJZzZ4OFF3eHgyRjRqYmdCZ296cndUU0tzQk1SOUl6c0hjVk02TFliTzZnNW5MK2ROVFhQWTZtRERvdmpyZGV0ZkI1UEdlakgwYUt4dzAzRTBQZmREZkIxZHYvR0xISGM5elZ4Mk1uWTJZUlBtZU9SZzVTdngxbXVybVlOaklKSzIrUXNkQlhYcEZkZWNISm9oVG1mK2p1WTRySmJFa1VTK3RLREUzRmQwemVVQXhtR2RZb0lJOFRzVzVKYTRWQmZuRnBVV3BjRi9ubCthVlFEbk1pV1hwTUkvbnBxWmtKdWFoR2N0WmxGK3VCek1hRkJwTW9HZ0JodVZ2U0FpaEtHYlBMeWpKek04REttVVNoZ1ljc3VNWmk5QUVCRXJ6UUVhbjZDWm5sT1psNjVxWmdud0lUUVlNVVBzWW9RYkIyQ3dRTzFsZ0lRTkxCR3lwZWVtWmVYQlA1aVFtcGVaQU9YeEFQNEM5b0ZkUWxBbjNPaGRRdEZpdkpMOGtFYWFPS3prL0J5WUNpZjUvQURJcm1ITElBZ0FBIn0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BsmtExposure"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Av","2":"221","3":"23.20749","4":"19.90907"},{"1":"Gd","2":"134","3":"22.26880","4":"19.26248"},{"1":"Mn","2":"114","3":"20.00070","4":"18.25429"},{"1":"No","2":"953","3":"20.88959","4":"17.50394"},{"1":"NA","2":"38","3":"12.13908","4":"11.55402"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[5]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEJzbXRFeHBvc3VyZSwgeSA9IHBzZiwgZmlsbCA9ICBCc210RXhwb3N1cmUpKSArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpXG5gYGAifQ== -->

```r
ggplot(train, aes(x = BsmtExposure, y = psf, fill =  BsmtExposure)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzdGlvbiA6IE5vIGNsZWFyIGRpc3RpbmN0aW9uXG5gYGAifQ== -->

```r
# Conclustion : No clear distinction
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210RmluVHlwZTE6IFJhdGluZyBvZiBiYXNlbWVudCBmaW5pc2hlZCBhcmVhXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoQnNtdEZpblR5cGUxKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
# BsmtFinType1: Rating of basement finished area
train %>%
  group_by(BsmtFinType1) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6N30sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelE2V0JHa0FDa0RFR1ZpQm1LMkJnUUZkTTF0T2FsbHFUakdRSlFEV0NSRmxkdlFKaERHZEVFeDNCTk9uSE00TVNrMkdNVVB6MG9BVTUzOGdRTE9ITlRrbnNSaG1EZHp5dE1Ua2t2d2lJT3NmRU1PY2ZnZUlwd0FWTFFMU1hrRGNDbVN2QTlLcVFNd0hVdU5nWW5uWnF0eWp6TUhnb1lEWXRPdlJEbFlIVW5hOVhGVGhZSFNkWDFYdmI3MkQzc0dhSHhxdVBRNG1ZY242S3IrVkhEUU0vdi9rdk9vUDEyOXcvb09CN3VNdERycVhaS2E5MXpOMk1ML2c2RE1yT3NMQklEZjVTK0o5Q3dkZC9vQ3ZRT1JncFA2cjY4ZlcvdzVxVHpzRG1COFZRN3pFL0IvTkYxd3BpU1dKZW1sRmlibXA2SjdPQTRyQlBNMENGZVJ4S3M0dGNjdk1DNmtzU0RXRWgwNSthVjRKTEJRVHk5SmhBWlNibXBLWm1JZG1MR2RSZnJrZXpHaFFxREdCSWhZWTVqOGhJWW1pbUQyL29DUXpQdytvbEVrWW1nNlFIYzlZaENZZ1VKb0hNanBGTnptak5DOWIxOHdjNUVOb2dtS0Eyc2NJalNrWW13VmlKd3NzWkZoaHprL05TOC9NUzRWNU1pY3hLVFVIeXVFRCtnSHNCYjJDb2t5NDE3bUFvc1Y2SmZrbGlUQjFYTW41T1RBUlNETDVCd0JHRXQ3UUVnTUFBQT09In0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BsmtFinType1"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"ALQ","2":"220","3":"20.22588","4":"16.81226"},{"1":"BLQ","2":"148","3":"16.87915","4":"14.91037"},{"1":"GLQ","2":"418","3":"26.75154","4":"23.81350"},{"1":"LwQ","2":"74","3":"18.84007","4":"16.42731"},{"1":"Rec","2":"133","3":"15.37791","4":"14.52991"},{"1":"Unf","2":"430","3":"20.33745","4":"18.15617"},{"1":"NA","2":"37","3":"12.09570","4":"11.44831"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[7]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEJzbXRGaW5UeXBlMSwgeSA9IHBzZiwgZmlsbCA9ICBCc210RmluVHlwZTEpKSArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpXG5gYGAifQ== -->

```r
ggplot(train, aes(x = BsmtFinType1, y = psf, fill =  BsmtFinType1)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTm90IGJhZFxuYGBgIn0= -->

```r
# Conclusion : Not bad
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210RmluU0YxOiBUeXBlIDEgZmluaXNoZWQgc3F1YXJlIGZlZXRcbmdncGxvdCh0cmFpbiwgYWVzKHggPSBCc210RmluU0YxKSkgK1xuICBnZW9tX2hpc3RvZ3JhbShhbHBoYSA9IDAuNSwgZmlsbCA9IFwicmVkXCIpIFxuYGBgIn0= -->

```r
# BsmtFinSF1: Type 1 finished square feet
ggplot(train, aes(x = BsmtFinSF1)) +
  geom_histogram(alpha = 0.5, fill = "red") 
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dLCJoZWlnaHQiOjQzMi42MzI5LCJzaXplX2JlaGF2aW9yIjowLCJ3aWR0aCI6NzAwfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdncGxvdChhZXMoeCA9IEJzbXRGaW5TRjEsIHkgPSBwc2YpKSArXG4gIGdlb21faml0dGVyKGNvbG9yID0gXCJyZWRcIiwgYWxwaGEgPSAwLjMpICtcbiAgZ2VvbV9zbW9vdGgobWV0aG9kID0gXCJsbVwiKVxuYGBgIn0= -->

```r
train %>%
  ggplot(aes(x = BsmtFinSF1, y = psf)) +
  geom_jitter(color = "red", alpha = 0.3) +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzdGlvbiA6IE5vdCBnb29kIGZlYXR1cmVcbmBgYCJ9 -->

```r
# Conclustion : Not good feature
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogQnNtdEZpblR5cGUyOiBSYXRpbmcgb2YgYmFzZW1lbnQgZmluaXNoZWQgYXJlYSAoaWYgbXVsdGlwbGUgdHlwZXMpXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoQnNtdEZpblR5cGUyKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
# Conclusion : BsmtFinType2: Rating of basement finished area (if multiple types)
train %>%
  group_by(BsmtFinType2) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6N30sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelE2V0JHa0FDa0RFR1ZpQm1LMkJnUUZkTTF0T2FsbHFUakdRSlFEV0NSRmxkdlFKaERHZEVFeDNCTk9uSE00TVNrMkdNVVB6MG9BVTUzOGdRTE9ITlRrbnNSaG1EZHp5dE1Ua2t2d2lJT3NmRU1PY0R2S0tJaER6QWJFZUVKc0JqWG9CcE5XZ1l1d09SaHRuQ3Q1YXdlR2cvL04xNlZaZkJ3ZXJHbitCcDBvUkRvYm1ua3UvN0N4ek1ERGN6YjMyOVFjSDAxUHFIdUpYbkJ3MHZxby8vV3c4QzY3Zk1NUDdsdEMzVmdlRDVKOGZiaWtHTzVpc1ZsVHhmbjNIUWYvT3ovaGZFMUljZEcwV0NHM29sbmN3YW0xNE8vWExLZ2QxNlJYVm5SK1lJRjVpL28vbUM2NlV4SkpFdmJTaXhOeFVkRS9uQWNWZ25tYUJDdkk0RmVlV3VHWG1oVlFXcEJyQlF5ZS9OSzhFRm9xSlplbXdBTXBOVGNsTXpFTXpsck1vdjF3UFpqUW8xSmhBRVFzTTg1K1FrRVJSeko1ZlVKS1pud2RVeWlRTVRRZklqbWNzUWhNUUtNMERHWjJpbTV4Um1wZXRhMjRJOGlFMFFURkE3V09FeGhTTXpRS3hrd1VXTXF3dzU2Zm1wV2ZtcGNJOG1aT1lsSm9ENWZBQi9RRDJnbDVCVVNiYzYxeEEwV0s5a3Z5U1JKZzZydVQ4SEpnSUpKbjhBd0NaSXRJREVnTUFBQT09In0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BsmtFinType2"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"ALQ","2":"19","3":"18.69374","4":"17.40741"},{"1":"BLQ","2":"33","3":"15.98812","4":"16.39053"},{"1":"GLQ","2":"14","3":"26.48558","4":"20.66847"},{"1":"LwQ","2":"46","3":"17.21597","4":"15.93159"},{"1":"Rec","2":"54","3":"16.19426","4":"14.61841"},{"1":"Unf","2":"1256","3":"21.78966","4":"18.52150"},{"1":"NA","2":"38","3":"12.47882","4":"11.55402"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[7]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTm90IHNvIGdvb2RcbmBgYCJ9 -->

```r
# Conclusion : Not so good
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210RmluU0YyOiBUeXBlIDIgZmluaXNoZWQgc3F1YXJlIGZlZXRcbnRyYWluICU+JVxuICBnZ3Bsb3QoYWVzKHggPSBCc210RmluU0YyLCB5ID0gcHNmKSkgK1xuICBnZW9tX2ppdHRlcihjb2xvciA9IFwicmVkXCIsIGFscGhhID0gMC4zKSArXG4gIGdlb21fc21vb3RoKG1ldGhvZCA9IFwibG1cIilcbmBgYCJ9 -->

```r
# BsmtFinSF2: Type 2 finished square feet
train %>%
  ggplot(aes(x = BsmtFinSF2, y = psf)) +
  geom_jitter(color = "red", alpha = 0.3) +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIG11dGF0ZShic210MkZsYWcgPSBpZmVsc2UoQnNtdEZpblNGMiA9PSAwLCBcIk5cIiwgXCJZXCIpKSAlPiVcbiAgZ2dwbG90KGFlcyh4ID0gYnNtdDJGbGFnLCB5ID0gcHNmLCBmaWxsID0gYnNtdDJGbGFnKSkgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKVxuYGBgIn0= -->

```r
train %>%
  mutate(bsmt2Flag = ifelse(BsmtFinSF2 == 0, "N", "Y")) %>%
  ggplot(aes(x = bsmt2Flag, y = psf, fill = bsmt2Flag)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogbW9zdCBvZiB2YWx1ZXMgYXJlIDAuIGFuZCBubyBjby1yZWxhdGlvbiBmb3Igbm9uIHplcm8gdmFsdWVzXG5gYGAifQ== -->

```r
# Conclusion : most of values are 0. and no co-relation for non zero values
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210VW5mU0Y6IFVuZmluaXNoZWQgc3F1YXJlIGZlZXQgb2YgYmFzZW1lbnQgYXJlYVxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEJzbXRVbmZTRikpICtcbiAgZ2VvbV9oaXN0b2dyYW0oYWxwaGEgPSAwLjUsIGZpbGwgPSBcInJlZFwiKSBcbmBgYCJ9 -->

```r
# BsmtUnfSF: Unfinished square feet of basement area
ggplot(train, aes(x = BsmtUnfSF)) +
  geom_histogram(alpha = 0.5, fill = "red") 
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dLCJoZWlnaHQiOjQzMi42MzI5LCJzaXplX2JlaGF2aW9yIjowLCJ3aWR0aCI6NzAwfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdncGxvdChhZXMoeCA9IEJzbXRVbmZTRiwgeSA9IHBzZikpICtcbiAgZ2VvbV9wb2ludChjb2xvciA9IFwicmVkXCIsIGFscGhhID0gMC4zKSArXG4gIGdlb21fc21vb3RoKG1ldGhvZCA9IFwibG1cIilcbmBgYCJ9 -->

```r
train %>%
  ggplot(aes(x = BsmtUnfSF, y = psf)) +
  geom_point(color = "red", alpha = 0.3) +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBUb3RhbEJzbXRTRjogVG90YWwgc3F1YXJlIGZlZXQgb2YgYmFzZW1lbnQgYXJlYVxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IFRvdGFsQnNtdFNGKSkgK1xuICBnZW9tX2hpc3RvZ3JhbShhbHBoYSA9IDAuNSwgZmlsbCA9IFwicmVkXCIpICBcbmBgYCJ9 -->

```r
# TotalBsmtSF: Total square feet of basement area
ggplot(train, aes(x = TotalBsmtSF)) +
  geom_histogram(alpha = 0.5, fill = "red")  
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dLCJoZWlnaHQiOjQzMi42MzI5LCJzaXplX2JlaGF2aW9yIjowLCJ3aWR0aCI6NzAwfQ== -->

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArwAAAGwCAMAAAB8TkaXAAAAwFBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZrY6AAA6ADo6AGY6OgA6Ojo6OmY6ZmY6ZpA6ZrY6kNtmAABmOgBmOjpmZjpmZmZmZpBmkLZmkNtmtttmtv+QOgCQZgCQZjqQZmaQtraQttuQ2/+2ZgC2Zjq2kDq2kGa2tpC2tra2ttu229u22/+2/7a2///bkDrbkGbbtmbbtpDbtrbb25Db27bb29vb2//b/9vb////f3//tmb/25D/27b/29v//7b//9v///+e4fX+AAAACXBIWXMAAA7DAAAOwwHHb6hkAAANn0lEQVR4nO3dgXbTRgJG4XFKYkqBxoEt2xgKMV1oabSkS7pZOdh+/7faGUmWHUuZaqyRrJ/c7xwcpcSDjs5FjCRLNStAlDn0CgD7Il7IIl7IIl7IIl7IIl7IIl7IIl7Iah7v7PjGvqbGjC5W2wuh4wCRNI4uNS7e1Abrfm0WQscBYmka3WLi4l1OT+3y7GSzEDoOEE3T6JLj1zbe+fjcLR9dlguh4wDRNIxu/vjCzXntF/tNauNdL2RjON2tIlCvWXRuluDizWe59rVcCBsHiKhZdIkNl3gxMI2iyyYJ908bGo8DxNQousTkzjlgw4CEXaTgVBkGJPAKGxcpMByhl4eT9VXhhMvDOLBY0REveke8kEW8kEW8kKUW7/8qevqDMTzEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1nEC1n68dboaV1wYMQLWcQLWQ2jS4wZXbiFtLIQNE5rxItSs+iSo8tV6lp1L3cXgsZpj3hRahTdYnK6Wi2nJ/aXXVjNthaCxomAeFFqHp2Ldz4+X2X74XIhfJx2iBel5tEldpIwf+wmCqmNd72QjeF0tH67iBelptHZ47PTVTHLta/lQug4bREvSiHThuMb4sWABERnU62fNgSO0wrxohQQnT1I44ANA9IoujxVu5/lVBkGpFl0s+ObvFcuUmA4GkY3M8a4ve/mOnHC5WEcGB/MgSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihaya6BYvnl66r8vp0WWbcTpBvChVoru+/jI5+v3auhoTL4ZsN7rFxGwc3+w9TleIF6VKdLcfP4xHbz86vzVvl3jRv5rolr/8FFDt/eN0gnhR4mwDZNVH9/U681fbceIjXpTqolucFQdsnG3AkNVFNzOjV6FHbMSL3tVdpJiMLmKM0wniRak23oDpgmecThAvSnWnyqbseaGgLrr5+PhTjHG6QLwo1U4bDGcbIKD2Cts/CuWVtuXUpnzqllJj8klFuXDvOJ0gXpQaRZfNghNzYpO1C+7XZiFknAiIF6VG0c3H5/Y1ObpcTt3ud3ayKheCxomAeFGqi664OLx7edjuaMuKywXfOF0gXpQCDthmttnHbqKQbi1kYzh9rOyKeLGl7oDtT3dp+MPL0as7l4dTe8SWz3Lta7ngGacTxIuSJ7pkdL71Xbo+XiNeDIQnusVk6zagNDtTVj9t+Jtx9teoVOJ9sLzxbtpM8rO8PR+wES987o9u+evmBszE5DOInk+VES98vGcb1nPe+fi0WOr3IgXxwsdzefin39f/Jclbdq0m66vCSQ+Xh4kXPoO+AZN44UO8kFUf3dXLH3549q79OC0RL3zqonMfgByNg572RLzoX110iXn0abW6PTOnNb8ZME5rxAsfzz1s8/GhH7RHvPDx3D0cdBcx8aJ3nuc2zA/+fF7ihU/9E3OyyW5230+bcVojXvjU3/punr798MKEPL5hUPHS88NQG91t9qS9RyEPbyBe9O6e6JbX12EPmCZe9O6bvDxMvA+D5/O8AY+WJl4cQO3l4ffuHNmdu4D2Gqc14oVP/eVhl+3yveypMuJ9GDwXKXSvsBHvw/BNXh4m3oeh9oM5+c1r6cH/D5jEC5+66FJjnr398HJzA+ae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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBIZWF0aW5nOiBUeXBlIG9mIGhlYXRpbmdcbnRyYWluICU+JVxuICBncm91cF9ieShIZWF0aW5nKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
# Heating: Type of heating
train %>%
  group_by(Heating) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6Nn0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFhV0JHa0FDa0RFR1ZnaDRpZ2EyWEpTeTFKemlvRXNBYkFzUkpUVkxTYy92d2pLWVhGUExIWkVZb2ZEMlVXSlpUQzJmMGtHWER3OE1TY0h6UnJXNUp6RVlwZ3RjTHZURXBOTGdOWXdNUHdEWWlSWHMwNEIwa0pBekE3MUFjajFmQ0I1QjlXSHdSK0R4Qlk3bU5yL0Q3MnZzY3RCWjE3N3hwSXJFZzdLakRNdXUvQW5PUmpGcWt6eVZKbmtvTFpZVU9oZkRTZUdQc092NVlhdXo4SWN0R1prbkoxNzdKYURrdm5SZWU0MkJ4RDZPaklsMjRRZlFKelAvQi9OeFZ3cGlTV0plbWxGaWJtcDZCN01BNHJCUE1nQ0ZXVDNTRTBzeWN4TGh3ZENmbWxlQ1pURG5GZ0dFMmZMVFUzSlRNeERNNUd6S0w5Y0QyWXFLSENZR29ERS8vLy9mMEVDREVVeGUzNUJTV1orSGxBcGt6QTBwcEhkelZpRUppQlFtZ2N5T2tVM09hTTBMMXZYM0J6a09XaVNZWURheHdpTkVCaWJCV0luQ3l4UVdHSE9UODFMejh4TGhYa3lKekVwTlFmSzRRUDZBZXdGdllLaVRMalh1WUNpeFhvbCtTV0pNSFZjeWZrNU1CRklhdmdIQU5jNEZVTDBBZ0FBIn0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Heating"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Floor","2":"1","3":"10.940094","4":"10.94009"},{"1":"GasA","2":"1428","3":"21.249990","4":"17.95885"},{"1":"GasW","2":"18","3":"14.309629","4":"13.29767"},{"1":"Grav","2":"7","3":"9.503119","4":"9.10893"},{"1":"OthW","2":"2","3":"18.363839","4":"18.36384"},{"1":"Wall","2":"4","3":"11.318490","4":"11.26643"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[6]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzdGlvbiA6IE1vc3Qgb2YgdGhlIHZhbHVlcyBiZWxvbmcgdG8gb25lIGNhdGVnb3J5XG5gYGAifQ== -->

```r
# Conclustion : Most of the values belong to one category
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBIZWF0aW5nUUM6IEhlYXRpbmcgcXVhbGl0eSBhbmQgY29uZGl0aW9uXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoSGVhdGluZ1FDKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
# HeatingQC: Heating quality and condition
train %>%
  group_by(HeatingQC) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFxV0JHa0FDa0RFUVdJb210aHlVc3RTYzRxQkxBR3dMRVNVeWJVQ3huSkxoTEhjVTJDc2dId1lLOFFSelR6VzVKekVZcGh4Y0V2U0VwTkw4b3VBckg5QURIVWEwMU1nYlFqRUh5SE9aRndEcFBsQWNnNFdmbmUrcEJnc2NOQVRlK213YzdtNWcxR0YvK0hhUnpjY0ROUEF3TUZ3Z2MyQ0MrdFk0T3BOMTM0M2ZoNm42S0Q1Z0tlQ1dZN1J3U0Q1U2YwWjY5dHc5YnJiUGp3d0RmMEhjU3J6ZnpUWGNhVWtsaVRxcFJVbDVxYWlleVlQS0FiekRBdFVrTk1qTmJFa015ODkwQm51NWZ6U3ZCSW9oem14TEIzbTY5elVsTXpFUERRek9Zdnl5L1ZnNW9LQ2dxa0JTUHovLy84M0pIaFFGTFBuRjVSazV1Y0JsVElKUXlNVTJlV01SV2dDQXFWNUlLTlRkSk16U3ZPeWRjMHRRTjZEcGdJR3FIMk1VSU5nYkJhSW5TeXdZSUdsQWJiVXZQVE12RlNZSjNNU2sxSnpvQncrb0IvQVh0QXJLTXFFZTUwTEtGcXNWNUpma2doVHg1V2Nud01UZ2NUOVB3RG1PbHlleHdJQUFBPT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["HeatingQC"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Ex","2":"741","3":"24.30806","4":"21.67955"},{"1":"Fa","2":"49","3":"15.04475","4":"12.93760"},{"1":"Gd","2":"241","3":"18.46997","4":"16.39021"},{"1":"Po","2":"1","3":"17.40000","4":"17.40000"},{"1":"TA","2":"428","3":"17.62593","4":"14.85731"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[5]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEhlYXRpbmdRQywgeSA9IHBzZiwgZmlsbCA9ICBIZWF0aW5nUUMpKSArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpXG5gYGAifQ== -->

```r
ggplot(train, aes(x = HeatingQC, y = psf, fill =  HeatingQC)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogR29vZC4gTm90IGdyZWF0LlxuYGBgIn0= -->

```r
# Conclusion : Good. Not great.
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDZW50cmFsQWlyOiBDZW50cmFsIGFpciBjb25kaXRpb25pbmdcbnRyYWluICU+JVxuICBncm91cF9ieShDZW50cmFsQWlyKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
# CentralAir: Central air conditioning
train %>%
  group_by(CentralAir) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6Mn0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVJ6VXJFTUJCTy81UXR1Q3o0REFvcVcyVkI4Q0pXMUt1Z0tPeWVKTGJaTlpoTmxqUzdldlFkOUFFOGVoSVBQb0t2NHRHVEp5K3RrellwYkE3TnpIejVPdk45bWN2VDRTQWV4Z2doSHdXaGgvd0EwdENIdzBNaDZ1ajRpRkN3cmxHSWF6VlJYOVp4aWJqQ3lJS3dBckplZld0K1A3Zkp5T0ZIR2NPRnBiZE54amhUUWtKV3dtZkgzUUQ3R21KWDErbjJ6dHZQNzk5bnV2KzZlYmhMejFwODYrcmkrLzNyT1IyTWp1akh4a3N6THFpY0NYR09GVTdHRWsrSks0Z0RaZ1dGbG41Q3VKS1lIVlBaNmhaenJrd1I0TVhFU3ArU25HTHVOTzFJOFpEWXhyV2ZKemlxcWlvYmowdmtWVEZUVkhDZyt2ckZJMGU2SngyZ04rZTZkZDdQN3ViOHZuK3dwd1diOVNBeno2eXF6Y05tWm1qZkpiTHlDWjlRVHF4SmhtOEpNMFVYUE5RV2twbWtyZlVZMENKUlFtSExpelBCTE5Jc3NQd0hiS0lKUG1BQ0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["CentralAir"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"N","2":"95","3":"13.08527","4":"12.66469"},{"1":"Y","2":"1365","3":"21.62558","4":"18.34862"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[2]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IENlbnRyYWxBaXIsIHkgPSBwc2YsIGZpbGwgPSAgQ2VudHJhbEFpcikpICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIilcbmBgYCJ9 -->

```r
ggplot(train, aes(x = CentralAir, y = psf, fill =  CentralAir)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTmljZSBkaXN0aW5jdGlvbiBiZXR3ZWVuIGJvdGggY2F0ZWdvcnkgYnV0IHZlcnkgbGVzcyB2YWx1ZXMuXG5gYGAifQ== -->

```r
# Conclusion : Nice distinction between both category but very less values.
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBFbGVjdHJpY2FsOiBFbGVjdHJpY2FsIHN5c3RlbVxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEVsZWN0cmljYWwpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZiksXG4gICAgICAgICAgICBtZWRpYW4gPSBtZWRpYW4ocHNmKSlcbmBgYCJ9 -->

```r
# Electrical: Electrical system
train %>%
  group_by(Electrical) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6Nn0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NhVjRnelFhV0JHa0FDa0RFR1ZnYkdCalFOYkxscEphbDVoUURXUUpnWFJCUlZyZlM0bFJIWkk0Yk1pY0F5bUgyemF5QWlRYzdGV1VYQVJtYy80RUF6UkxXNUp6RVlwZ2RjSnZURXBOTDhrRmEvZ0V4ek0xeFFDd05kVFBRL2F4bVVIL3dnZVFkZERMT1Bmdlhjc3BCNit4TVp5MnRTdzQ2NFJkYWJ1OW9kWkI5ckJVMnowTFJ3WFRQaVJkZlhoOXhNRFRadWZ6NXVRbHdmZHJ0bWNJcm55bzRhTWlFL1B2ejdhbUQ5dlBkMG1sOU5YQjlSbGsrVjZORVp5SDBnWnpQL0IvTnhWd3BpU1dKZW1sRmlibXA2QjdNQTRyQlBNZ0NVKzZhazVwY1VwU1puSmdERDRmODByd1NXT0FsbHFYRGdpSTNOU1V6TVEvTlVNNmkvSEk5bU1HZzhHRUN4Ujh3ZEg5QndneEZNWHQrUVVsbWZoNVFLUk1vR2JDaU9aMnhDRTFBb0RRUFpIU0tibkpHYVY2MnJvVVJ5TUhRc0dhQTJzY0lqUk1ZbXdWaUp3c3NYRmhoemsvTlM4L01TNFY1TWljeEtSWG1ZejZnSDhCZTBDc295b1I3blFzb1dxeFhrbDhDRHhtdTVQd2NtQWdrUWZ3REFJZHZpQUgxQWdBQSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Electrical"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"FuseA","2":"94","3":"14.204704","4":"13.764474"},{"1":"FuseF","2":"27","3":"13.401560","4":"12.055336"},{"1":"FuseP","2":"3","3":"14.171513","4":"13.952599"},{"1":"Mix","2":"1","3":"7.471841","4":"7.471841"},{"1":"SBrkr","2":"1334","3":"21.737441","4":"18.415235"},{"1":"NA","2":"1","3":"17.205958","4":"17.205958"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[6]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IEVsZWN0cmljYWwsIHkgPSBwc2YsIGZpbGwgPSAgRWxlY3RyaWNhbCkpICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIilcbmBgYCJ9 -->

```r
ggplot(train, aes(x = Electrical, y = psf, fill =  Electrical)) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogU29tZSBwZW5hbHR5IGlmIG5vdCBzdGFuZGFyZCBicmVha2Vyc1xuYGBgIn0= -->

```r
# Conclusion : Some penalty if not standard breakers
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIHNlbGVjdChMb3RBcmVhLCBjb250YWlucyhcIlNGXCIpLCBwc2YpICU+JVxuICBoZWFkKDEwKVxuYGBgIn0= -->

```r
train %>%
  select(LotArea, contains("SF"), psf) %>%
  head(10)
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbImRhdGEudGFibGUiLCJkYXRhLmZyYW1lIl0sIm5jb2wiOjExLCJucm93IjoxMH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJvMVRUV2dUUVJqOWRqZHBUYUtsb09DaHJTZ3FGaVdScE1ZMmg4cG9ROEJTMUppMlJqMXRzeHNidXRtTnV4dXF0K0twQjZrOWlZcDQ4MVlRUlBEdlVudndKQjY4Nk1HZm14UUZrU0tlSlBGTk10c3NxNGdETDkvM3ZYMzdKaTh6T1pzdHBxTEZLQkhKcElRa2toVzBJUmtmRW9Vb3d1c1ZJbVU3bWhpd0RZQjREd1Q3RjRnT2JhQ2VJaHArQk93bE9xQVJEUzRSN1Z3bjZ2L1YwY3RyOEhnRHI4K1kzMkcrQWJ3bkNwOEhmNUZhU3lsMDlQOWN1MzI5cDc4SjczN2dJWHg1L1FLT29ZNjI5MU9lb0Y3djZKVWlRbjVEdlFYOUQvUlgwZU85THZpRUNtMjk4dW52ZXVXRlQzOVA2QnVvYVo5K1dtU2FFZjREcUVjRjl4Yjk5OEQzLzkvbDAwc0hmZndxTUFnMGdhL0FoWUIrVk16OEhad1RUUUs3Z0F6d1Nqd0xBVDFjejBaV0hqd2V6eXl6MUhyckFSdjZ3TmRIRnMrdkZlc2J0MWx5Y1VmZnlUdXJiTjlZMzhDNHM4aU9YWDYrdEZMTnNxR3h1eS92cDYreGRPWXAxak4yK0hYZW1Gb2VEbHlvc0tsV2RRZE5ML0ZMMVNhN0p5ejN1SzJyWW95ZWNLcHVybUlXY3NrL21KUmdJcHlaTXN1Rm5DQmlrNWFyR3B6ZHBMWWtIVGRuMkowNVpXcitlZXVFTlordnEwYkwyTnZwbkdWcFdiMDAxekUrWGRQTk01WmRtdDJrbEpwVER1WXFHYXJqNWZMSXFLYTZhcUpzSTNKQUhyR3QrWVQzVS9CemtoZjRBVGFiUDFFYUFYRzNWWE1ybGdtcHpQK0s0Y0F1a2gwZ2V1c210OWJpcGRtNk9SY2ZPU0x1Z2VTN0Y1TGd2RDdXM2xOdUNxK3c4T3JTelVzVlUvZFNHdXFNYm9paEJ4bGFFUkkxdTJLNlhtYXdUc0xsaCtFeEpjdndtRlk0YXZ3RzdZbExZM2tFQUFBPSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["LotArea"],"name":[1],"type":["int"],"align":["right"]},{"label":["BsmtFinSF1"],"name":[2],"type":["int"],"align":["right"]},{"label":["BsmtFinSF2"],"name":[3],"type":["int"],"align":["right"]},{"label":["BsmtUnfSF"],"name":[4],"type":["int"],"align":["right"]},{"label":["TotalBsmtSF"],"name":[5],"type":["int"],"align":["right"]},{"label":["1stFlrSF"],"name":[6],"type":["int"],"align":["right"]},{"label":["2ndFlrSF"],"name":[7],"type":["int"],"align":["right"]},{"label":["LowQualFinSF"],"name":[8],"type":["int"],"align":["right"]},{"label":["WoodDeckSF"],"name":[9],"type":["int"],"align":["right"]},{"label":["OpenPorchSF"],"name":[10],"type":["int"],"align":["right"]},{"label":["psf"],"name":[11],"type":["dbl"],"align":["right"]}],"data":[{"1":"8450","2":"706","3":"0","4":"150","5":"856","6":"856","7":"854","8":"0","9":"0","10":"61","11":"24.67456"},{"1":"9600","2":"978","3":"0","4":"284","5":"1262","6":"1262","7":"0","8":"0","9":"298","10":"0","11":"18.90625"},{"1":"11250","2":"486","3":"0","4":"434","5":"920","6":"920","7":"866","8":"0","9":"0","10":"42","11":"19.86667"},{"1":"9550","2":"216","3":"0","4":"540","5":"756","6":"961","7":"756","8":"0","9":"0","10":"35","11":"14.65969"},{"1":"14260","2":"655","3":"0","4":"490","5":"1145","6":"1145","7":"1053","8":"0","9":"192","10":"84","11":"17.53156"},{"1":"14115","2":"732","3":"0","4":"64","5":"796","6":"796","7":"566","8":"0","9":"40","10":"30","11":"10.13107"},{"1":"10084","2":"1369","3":"0","4":"317","5":"1686","6":"1694","7":"0","8":"0","9":"255","10":"57","11":"30.44427"},{"1":"10382","2":"859","3":"32","4":"216","5":"1107","6":"1107","7":"983","8":"0","9":"235","10":"204","11":"19.26411"},{"1":"6120","2":"0","3":"0","4":"952","5":"952","6":"1022","7":"752","8":"0","9":"90","10":"0","11":"21.22549"},{"1":"7420","2":"851","3":"0","4":"140","5":"991","6":"1077","7":"0","8":"0","9":"0","10":"4","11":"15.90296"}],"options":{"columns":{"min":{},"max":[10],"total":[11]},"rows":{"min":[10],"max":[10],"total":[10]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyAxc3RGbHJTRjogRmlyc3QgRmxvb3Igc3F1YXJlIGZlZXRcbmdncGxvdCh0cmFpbiwgYWVzKHggPSBgMXN0RmxyU0ZgKSkgK1xuICBnZW9tX2hpc3RvZ3JhbShhbHBoYSA9IDAuNSwgZmlsbCA9IFwicmVkXCIpICBcbmBgYCJ9 -->

```r
# 1stFlrSF: First Floor square feet
ggplot(train, aes(x = `1stFlrSF`)) +
  geom_histogram(alpha = 0.5, fill = "red")  
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dLCJoZWlnaHQiOjQzMi42MzI5LCJzaXplX2JlaGF2aW9yIjowLCJ3aWR0aCI6NzAwfQ== -->

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArwAAAGwCAMAAAB8TkaXAAAAwFBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZrY6AAA6ADo6AGY6OgA6Ojo6OmY6ZmY6ZpA6ZrY6kNtmAABmADpmOgBmOjpmZjpmZmZmZpBmkLZmtttmtv+QOgCQOjqQZgCQZjqQZmaQkGaQtraQttuQ2/+2ZgC2Zjq2kDq2kGa2tpC2tra2ttu229u22/+2///bkDrbkGbbtmbbtpDbtrbb25Db27bb29vb2//b////f3//tmb/25D/27b/29v//7b//9v///8R/jP7AAAACXBIWXMAAA7DAAAOwwHHb6hkAAANl0lEQVR4nO3dj3fT1hmHcYWSmLa0SwasLN7aAaaDFbSlI01kiP3//1eVZFv5YeWiK7+vrr7O8zmHoJNTdH1vnhpZskW2BERlqR8A0BfxQhbxQhbxQhbxQhbxQlbHePMsO3hTbRRbG0Ai3eLNH31cFlWr1ZfbG0AqneK9OjleLhfTo/JXubGc3diI2g9gqXt0Vbzzyemyfh5uNuL3AxjpHl1eHiTMn1QHCkUZ72Yjfj+Aka7Rla/Pjpfro9zya7NR76Pi9giBe8QcNhxetMcbtx/ASER0ZaocNmBEIqIrX6Txgg0j0im6Varl8yynyjAi3aKbHV6ser33IgXxYnAdo5tlWVY9+15fJ85vXx4mXgzOKjrixeCIF7KIF7KIF7KIF7KIF7LU4r3cMtDAGB/ihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSzihSz9eFsM9FiQGPFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCFvFCVrfoFtMsy46rrSLLDt7c2ojZz+6IF41O0S2mZad5dlQmW25Uv643YvZjgHjR6BTdfHJafs0ffVxMq6ff2dGy2YjajwHiRSMiuvKJtqm42eixn50QLxoR0c3KZp9UBwrFjY0e+9kJ8aLRPbqifMW2OsotvzYb9T4qTo/vLuJFo3N0xeb12na8UfvZEfGi0TW6oj5TxmEDRqRjdPnqLC8v2DAi3aLLs9P6d06VYUQ6nuc9Xm9xkQLj0Sm6vD6fUF8OzjdXhXMuDyMx3pgDWcQLWXsZLz0/DMQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWaOOt2+pxPswEC9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9kES9ktUR39fxp/e+kLKbX/15Kn/3sjngRshXd+fmnk0e/nZfOJsSLMbsb3dVJdu3wovd+TBAvQrai+/z+3eTg1fvKf7q3S7wYXkt0i19+iqj2/v3sjngRwtkGyGqP7st57Y9d97Mj4kVIW3RXz9Yv2DjbgDFri26WHbyMfcVGvBhc20WKk5v/Lmv//eyOeBHSGm/E4UJgP7sjXoS0nSqb8swLBW3RzSeHHyz2szPiRUjrYUPG2QYIaL3C9re1iCttxIvBcYUNsogXstqiW18c5vIwxo0XbJDV9oLt9+rS8LsXBy+5PIwxC0SXH5ya7Kc/4kVIILqrEz4GhDELxssxL8bs/ugWv/IBTIxa8GwDx7wYs8Dl4Z9+220/uyNehHCFDbKIF7Laozt78f33P7zefT87Il6EtEW3mGbZwSTqbk/Ei+G1RZdnjz8sl5+fZce77WdnxIuQwGfY5hPO82LMAp8e5gobxi1w34Y59+fFqLXfMac+2M2zo932szPiRUj7R9+zp6/ePc9ibt9AvBhca3Sf6zvtPY65eQPxYnD3RLc4P4+7wfTY46XnPfRQLg8T7x4KvJ834rPDxIsEWi8Pv63OkUV9Coh4Mbz2y8NVtou3+3SqjHj3UOAixV5dYSPePfRQLg8T7x5qfWPO6sNrxT59AJOc91BbdEWW/fDq3Yu9+gAm8e6h1ujOvquvsMV8lIJ4MbgHfIWNeNU94CtsxKuOeIlXFvESryziJV5ZxEu8soiXeGURL/HKIl7ilUW8xCuLeIlXFvESryziJV5ZxEu8soiXeGURb5jHtGCEeMM8pgUjxBvmMS0YId4wj2nBCPGGeUwLRog3zGNaMEK8YR7TghHiDfOYFox0jm7+bX3vpyJb3+2/2YjcT4zU5V4S76h1jW5947KiDLb6db0RuZ8oqcu9JN5R6xhd+TxbxbuYVv9O0OzoeiNyP3FSl3tJvKPWLboiOy6qeOeT6vZl+aOPzUbcfiKlLveSeEetc3SreJ+8WW02G9H7iZG63EviHbW4eFdHueXXZqPeR8XjwaUu95J4R80i3qj9xEhd7iXxjhqHDWEe04KRyHh5wYbxiIuXU2UYkbh4uUiBEYmMd5lvrgrnXB5GYrwxJ8xjWjBCvGEe04IR4g3zmBaMEG+Yx7RghHjDPKYFI8Qb5jEtGCHeMI9pwQjxhnlMC0aIN8xjWjBCvGEe04IR4g3zmBaMEG+Yx7RghHjDPKYFI8Qb5jEtGCHeMI9pwQjxhnlMC0aIN8xjWjBCvGEe04IR4g3zmBaMEG+Yx7RghHjDPKYFI8Qb5jEtGCHeMI9pwQjxhnlMC0aIN8xjWjBCvGEe04IR4g3zmBaMEG+Yx7RghHjDPKYFI8Qb5jEtGCHeMI9pwQjxhnlMC0aIN8xjWjBCvGEe04IR4g3zmBaMEG+Yx7RghHjDPKYFI8Qb5jEtGCHeMI9pwQjxhnlMC0aIN8xjWjBCvGEe04KR8cSbOtN2BksDL8QbZrA08EK8YQZLAy/EG2awNPBCvGEGSwMvxBtmsDTwQrxhBksDL8QbZrA08EK8YQZLAy/EG2awNPBCvGEGSwMvxBtmsDTwQrxhBksDL8QbZrA08EK8YQZLAy/EG81gtWCCeKMZrBZMEG80g9WCCeKNZrBaMEG80QxWCyaIN5rBasEE8UYzWC2YIN5oBqsFE8QbzWC1YIJ4oxmsFkwQbzSD1YIJ4o1msFowQbzRDFYLJog3msFqwQTxRjNYLZgg3mgGqwUTxBvNYLVggnijGawWTBBvNIPVggnijWawWjBBvNEMVgsmiDeawWrBBPFGM1gtmCDeaAarBRPEG81gtWCCeC0YLCDiEa8FgwVEPOK1YLCAiEe8FgwWEPGI14LBAiIe8fowWFJ8DfH6MFhSfA3x+jBYUnxNonhTt+XOaFkRQrw+jJYVIcTrw2hZEUK8PoyWFSHE68NoWRFCvD6MlhUhxOvDaFkRQrw+jJYVIcTrw2hZEUK8PoyWFSHE68NoWRFCvIMxWmk0iDclo8V/qIg3JaPFf6h6x1tk2cGb3vtJXc1I9F181PrGW5TlFjfqJd4+ei4+VnrGu5gel19nR932k7oRJf1+Hq1r3HdXMnrGO5+cll/zRx877WfwAvZdtzXu96MdXu+H3jfeJ9URQ7GKN6v02w/QX8/oVoe7Nw56iReDI17Isjhs2GE/QH+DvGADPAxyqgzwkOgiBbC73tHlO10eBnY3nts9AZGIF7KIF7KIF7KIF7KIF7KIF7KIF7KIF7LM4gUGYh+v0X4YnMEHfwAPdxUZXP4BPNxVZPCH+wCAvogXsogXsogXsogXsogXskzivXO70wHMv/14a+DtDS+LaZZlx4kGv/7kYIrBS7PDi3SDb7GI9+4nif1dndR3jGgG3t7wspiWe8+zoySD1zfKuGfMQX4IRVbFm2jwbQbxbt3DwV35/3kVbzPw9oab5m4rKQa/OjmuZt025iA/hKuTKt5Eg7cwiHfr7jneiuy4vtFUM/D2hvcjOHiTbPAq3kSD54f/LONNt+x3WcR7975lA1jFuxl4e8N5+FnbmAMNnpd/PacZvByjOuZNt+x3GcS7dcfIAdQL1Qy8veE8evmKLdHgRf1qMcng1cFBFW+yZd9CvD0G37xeS/IjXEwPL5IMnpfh7l28D+2woajPlKX7y7M64E4weD3C3h02pDhcT/iCLV+d5U33sqUcJ8Xg+fpzDEkGbyd5qmwdb5JzNnl2Wv+e7jxdkeY8XW22b6fKUpyiLlJdpJhPjjcPIcGp+qadVNcJZvt2kWLrdqcDWB9fNQNvbzhZ/+VZjTH84GU81d/b7WMO8kNYXR5ONPgW3pgDWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcQLWcTr6erk9M53vizr9+SuVG9SqC9ZrZw9L7/39PXy9n8y4MNVQ7yOrp5ld+L9b/Wp53vifbv+7l+WxNsN8fo5m2R3453Vb6K//u6NeOeTg+pJ9/918MXdP4gWxOtl8Y/s8b8i4t2813I+OSLebojXy9VfX16sG1y8LZ+Dn35Y3bDk6G68i+lRnj36cKtX4u2CeD2tG5yt30Z5X7zfTLLqt+zH1xe3/yCCiNfTqsGrk+rY4H/Vx4fWhw0r9TvL62rrN7gvfs62zjbcOBeBLcTraRPvwY/v/6i/0R7v5pTC4vdfvlsFS7xdEK+novnYQ3nU8PKi/QXbrXO9y8WvGS/YOiJeT5sGP/28fhq9P97VsUX9repuesTbAfF6utHgl7NnB29Cz7yz9YfAiLcz4vW0anA+OSqPeD9XN0etC22Pt1gdWHyectjQFfF6unWqrIoybz1Vtjpg2NzV4/FH4u2GeD1tLlL8e5Jl3/x9Wb/b4fDivhdsn55X/9nLiyXxdkO8kEW8kEW8kEW8kEW8kEW8kEW8kEW8kEW8kEW8kEW8kEW8kEW8kPUn98ILS96u6yMAAAAASUVORK5CYII=" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdncGxvdChhZXMoeCA9IGAxc3RGbHJTRmAsIHkgPSBwc2YpKSArXG4gIGdlb21fcG9pbnQoY29sb3IgPSBcInJlZFwiLCBhbHBoYSA9IDAuMykgK1xuICBnZW9tX3Ntb290aChtZXRob2QgPSBcImxtXCIpXG5gYGAifQ== -->

```r
train %>%
  ggplot(aes(x = `1stFlrSF`, y = psf)) +
  geom_point(color = "red", alpha = 0.3) +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyAybmRGbHJTRjogU2Vjb25kIGZsb29yIHNxdWFyZSBmZWV0XG5nZ3Bsb3QodHJhaW4sIGFlcyh4ID0gYDJuZEZsclNGYCkpICtcbiAgZ2VvbV9oaXN0b2dyYW0oYWxwaGEgPSAwLjUsIGZpbGwgPSBcInJlZFwiKSAgXG5gYGAifQ== -->

```r
# 2ndFlrSF: Second floor square feet
ggplot(train, aes(x = `2ndFlrSF`)) +
  geom_histogram(alpha = 0.5, fill = "red")  
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dLCJoZWlnaHQiOjQzMi42MzI5LCJzaXplX2JlaGF2aW9yIjowLCJ3aWR0aCI6NzAwfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGZpbHRlcihgMm5kRmxyU0ZgID4gMCkgJT4lXG4gIGdncGxvdChhZXMoeCA9IGAxc3RGbHJTRmAsIHkgPSBwc2YpKSArXG4gIGdlb21fcG9pbnQoY29sb3IgPSBcInJlZFwiLCBhbHBoYSA9IDAuMykgK1xuICBnZW9tX3Ntb290aChtZXRob2QgPSBcImxtXCIpXG5gYGAifQ== -->

```r
train %>%
  filter(`2ndFlrSF` > 0) %>%
  ggplot(aes(x = `1stFlrSF`, y = psf)) +
  geom_point(color = "red", alpha = 0.3) +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogbG9va3MgdmVyeSB1bnVzYWwuIE5lZ2F0aXZlIGNvLXJlbGF0aW9uIGZvciAybmQgZmxvb3I/XG5gYGAifQ== -->

```r
# Conclusion : looks very unusal. Negative co-relation for 2nd floor?
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBMb3dRdWFsRmluU0Y6IExvdyBxdWFsaXR5IGZpbmlzaGVkIHNxdWFyZSBmZWV0IChhbGwgZmxvb3JzKVxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IExvd1F1YWxGaW5TRikpICtcbiAgZ2VvbV9oaXN0b2dyYW0oYWxwaGEgPSAwLjUsIGZpbGwgPSBcInJlZFwiKSAgXG5gYGAifQ== -->

```r
# LowQualFinSF: Low quality finished square feet (all floors)
ggplot(train, aes(x = LowQualFinSF)) +
  geom_histogram(alpha = 0.5, fill = "red")  
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dLCJoZWlnaHQiOjQzMi42MzI5LCJzaXplX2JlaGF2aW9yIjowLCJ3aWR0aCI6NzAwfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTW9zdCBvZiB2YWx1ZXMgYXJlIDAuIElnbm9yZS5cbmBgYCJ9 -->

```r
# Conclusion : Most of values are 0. Ignore.
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBHckxpdkFyZWE6IEFib3ZlIGdyYWRlIChncm91bmQpIGxpdmluZyBhcmVhIHNxdWFyZSBmZWV0XG5nZ3Bsb3QodHJhaW4sIGFlcyh4ID0gR3JMaXZBcmVhKSkgK1xuICBnZW9tX2hpc3RvZ3JhbShhbHBoYSA9IDAuNSwgZmlsbCA9IFwicmVkXCIpICBcbmBgYCJ9 -->

```r
# GrLivArea: Above grade (ground) living area square feet
ggplot(train, aes(x = GrLivArea)) +
  geom_histogram(alpha = 0.5, fill = "red")  
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dLCJoZWlnaHQiOjQzMi42MzI5LCJzaXplX2JlaGF2aW9yIjowLCJ3aWR0aCI6NzAwfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdncGxvdChhZXMoeCA9IEdyTGl2QXJlYSwgeSA9IHBzZikpICtcbiAgZ2VvbV9wb2ludChjb2xvciA9IFwicmVkXCIsIGFscGhhID0gMC4zKSArXG4gIGdlb21fc21vb3RoKG1ldGhvZCA9IFwibG1cIilcbmBgYCJ9 -->

```r
train %>%
  ggplot(aes(x = GrLivArea, y = psf)) +
  geom_point(color = "red", alpha = 0.3) +
  geom_smooth(method = "lm")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogSW1wb3J0YW50IGZlYXR1cmVcbmBgYCJ9 -->

```r
# Conclusion : Important feature
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210RnVsbEJhdGg6IEJhc2VtZW50IGZ1bGwgYmF0aHJvb21zXG5nZ3Bsb3QodHJhaW4sIGFlcyh4ID0gYXMuZmFjdG9yKEJzbXRGdWxsQmF0aCksIHkgPSBwc2YsIGZpbGwgPSAgYXMuZmFjdG9yKEJzbXRGdWxsQmF0aCkpKSArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpXG5gYGAifQ== -->

```r
# BsmtFullBath: Basement full bathrooms
ggplot(train, aes(x = as.factor(BsmtFullBath), y = psf, fill =  as.factor(BsmtFullBath))) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEJzbXRGdWxsQmF0aCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
train %>%
  group_by(BsmtFullBath) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NNUytVWmdBckFHa0NTaUxFbVNPQVFqNUFOajlVbmc4azdtQ1NmS0k4dDNDT2c1bkRnMUloZFdrSDdVbU9udUk2blE0R2s3NjE3RjJvRDFkbjZGMmFja0xqbUlQUitnZlhRMDVNY1ZEanZOK3ZPZnMyUWgyS3cxaVRjeEtMaTRFTUFTUkJycFRFa2tTOXRLTEUzRlIwNVhsQU1aaHlGcWdnajFOeGJvbGJhVTZPVTJKSkJ0emMvTks4RWlpSE9iRXNIY3BreTAxTnlVek1Rek9Xc3lpL1hBOW1OQ2dZbUJxQXhQLy8vLzhBcVg5b2l0bnpDMG95OC9PQVNwbEFJY3FLNW5qR0lqUUJnZEk4a05FcHVza1pwWG5adXBiR0lCOUNnNVlCYWg4alV0UkEyU0E3bWY5RHpXS0ZPVDgxTHowekx4WG15WnpFcE5RY0tJY1A2QWV3Ri9RS2lqTGhYdWNDaWhicmxlU1hKTUxVY1NYbjU4QkV3SjVqK0FjQUxTYVRVa0FDQUFBPSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BsmtFullBath"],"name":[1],"type":["int"],"align":["right"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"0","2":"856","3":"20.38978","4":"17.29476"},{"1":"1","2":"588","3":"22.25342","4":"18.68702"},{"1":"2","2":"15","3":"13.78565","4":"11.01928"},{"1":"3","2":"1","3":"16.57407","4":"16.57407"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[4]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCc210SGFsZkJhdGg6IEJhc2VtZW50IGhhbGYgYmF0aHJvb21zXG50cmFpbiAlPiVcbiAgZ3JvdXBfYnkoQnNtdEhhbGZCYXRoKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
# BsmtHalfBath: Basement half bathrooms
train %>%
  group_by(BsmtHalfBath) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6M30sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NNUzhRZzFRd2dCV0FOTUhGV0pPQWRBQlVqQThrNW1DcWJYemd4TTlBQjJPcE80SUxoSDBkN0xzTXA4UjFkc0hsRGIrV0c3bytDM1BRbnpvbk1PUEhDNFE4aWdOWWszTVNpNHVCREFFa1FhNlV4SkpFdmJTaXhOeFVkT1Y1UURHWWNoYW9JSTlUY1c2SlIySk9tbE5pU1FiYzNQelN2QklvaHpteExCM0taTXROVGNsTXpFTXpsck1vdjF3UFpqVEl5MHdOUU9MLy8vOS9nZFEvTk1YcytRVWxtZmw1UUtWTW9KQmpSWE04WXhHYWdFQnBIc2pvRk4za2pOSzhiRjFMRTVBUG9VSE1BTFdQRVJyME1EWUx4RTdtLzFDeldHSE9UODFMejh4TGhYa3lKekVwTlFmSzRRUDZBZXdGdllLaVRMalh1WUNpeFhvbCtTV0pNSFZjeWZrNU1CR3c1eGorQVFEaXlWTFVLQUlBQUE9PSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BsmtHalfBath"],"name":[1],"type":["int"],"align":["right"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"0","2":"1378","3":"21.16876","4":"17.95885"},{"1":"1","2":"80","3":"19.10492","4":"15.79221"},{"1":"2","2":"2","3":"31.53982","4":"31.53982"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[3]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogcGFzc1xuYGBgIn0= -->

```r
# Conclusion : pass
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBGdWxsQmF0aDogRnVsbCBiYXRocm9vbXMgYWJvdmUgZ3JhZGVcbnRyYWluICU+JVxuICBncm91cF9ieShGdWxsQmF0aCkgJT4lXG4gIHN1bW1hcmlzZShjb3VudCA9IG4oKSxcbiAgICAgICAgICAgIGF2ZyA9IG1lYW4ocHNmKSxcbiAgICAgICAgICAgIG1lZGlhbiA9IG1lZGlhbihwc2YpKVxuYGBgIn0= -->

```r
# FullBath: Full bathrooms above grade
train %>%
  group_by(FullBath) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6NH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NNUytVWmdBckFHa0NTaUtKQXpVd2RVR0VHQlNCbUE4azdxQi9QYnFsczFYTHdYRHU1azM5Z1pJTzV1LyszbDJ6dmNyQi9QYXpWd3czYnNQVnFYSGU3OWVjZmR0QmI4R1R0T00zM3p1WUN1MzBYU3o1ejhHY1BkWjcxZG8zYUE1alRjNUpMQzRHTWdTUUJMbFNFa3NTOWRLS0VuTlQwWlhuQWNWZ3lsbWdnaHh1cFRrNVRva2xHWEF6ODB2elNxQWM1c1N5ZENpVExUYzFKVE14RDgxSXpxTDhjajJZc2FBZ1lHb0FFdi8vLy84RHBQNmhLV2JQTHlqSnpNOERLbVVDaFNZcm1zTVppOUFFQkVyelFFYW42Q1pubE9abDYxcWFnbndIRFhZR3FIMk1TTkVDWllQc1pQNFBOWXNWNXZ6VXZQVE12RlNZSjNNU2sxSnpvQncrb0IvQVh0QXJLTXFFZTUwTEtGcXNWNUpma2doVHg1V2Nud01UQVh1TzRSOEE2MTRiNUR3Q0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["FullBath"],"name":[1],"type":["int"],"align":["right"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"0","2":"9","3":"15.92062","4":"11.01928"},{"1":"1","2":"650","3":"17.61602","4":"15.31424"},{"1":"2","2":"768","3":"23.93356","4":"21.07314"},{"1":"3","2":"33","3":"23.85899","4":"23.02877"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[4]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihGdWxsQmF0aCksIHkgPSBwc2YsIGZpbGwgPSAgYXMuZmFjdG9yKEZ1bGxCYXRoKSkpICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIilcbmBgYCJ9 -->

```r
ggplot(train, aes(x = as.factor(FullBath), y = psf, fill =  as.factor(FullBath))) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogTmljZSBvbmUuIEJ1dCBkbyB3ZSBoYXZlIHRvdGFsIG51bWJlciBvZiBiYXRoP1xuYGBgIn0= -->

```r
# Conclusion : Nice one. But do we have total number of bath?
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBIYWxmQmF0aDogSGFsZiBiYXRocyBhYm92ZSBncmFkZVxudHJhaW4gJT4lXG4gIGdyb3VwX2J5KEhhbGZCYXRoKSAlPiVcbiAgc3VtbWFyaXNlKGNvdW50ID0gbigpLFxuICAgICAgICAgICAgYXZnID0gbWVhbihwc2YpLFxuICAgICAgICAgICAgbWVkaWFuID0gbWVkaWFuKHBzZikpXG5gYGAifQ== -->

```r
# HalfBath: Half baths above grade
train %>%
  group_by(HalfBath) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6M30sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NNUzhRZzFRd2dCV0FOTUhGbUNjQ3VlSkFOZzhRODRIRUhJdzE5M0VmOFNoMnNFZ1hZSjYrOEw2RDRZVDRmYjVmK3VIeUJyUCtYWlpacE9aZ3N2YmNxMGZuOWpqb0NUWktBQkdhQTFpVGN4S0xpNEVNQVNSQnJwVEVra1M5dEtMRTNGUjA1WGxBTVpoeUZxZ2doMGRpVHBwVFlra0czTXo4MHJ3U0tJYzVzU3dkeW1UTFRVM0pUTXhETTVLektMOWNEMllzeUx0TURVRGkvLy8vZjRIVVB6VEY3UGtGSlpuNWVVQ2xUS0JRWTBWek9HTVJtb0JBYVI3STZCVGQ1SXpTdkd4ZFMzT1E3NkRCeXdDMWp4RWE3REEyQzhSTzV2OVFzMWhoemsvTlM4L01TNFY1TWljeEtUVUh5dUVEK2dIc0JiMkNva3k0MTdtQW9zVjZKZmtsaVRCMVhNbjVPVEFSc09jWS9nRUE0YTk5S2lRQ0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["HalfBath"],"name":[1],"type":["int"],"align":["right"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"0","2":"913","3":"19.16306","4":"16.60545"},{"1":"1","2":"535","3":"24.40259","4":"20.67894"},{"1":"2","2":"12","3":"17.56396","4":"15.03419"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[3]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihIYWxmQmF0aCksIHkgPSBwc2YsIGZpbGwgPSAgYXMuZmFjdG9yKEhhbGZCYXRoKSkpICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIilcbmBgYCJ9 -->

```r
ggplot(train, aes(x = as.factor(HalfBath), y = psf, fill =  as.factor(HalfBath))) +
  geom_boxplot() +
  theme(legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBCZWRyb29tOiBCZWRyb29tcyBhYm92ZSBncmFkZSAoZG9lcyBOT1QgaW5jbHVkZSBiYXNlbWVudCBiZWRyb29tcylcbnRyYWluICU+JVxuICBncm91cF9ieShCZWRyb29tQWJ2R3IpICU+JVxuICBzdW1tYXJpc2UoY291bnQgPSBuKCksXG4gICAgICAgICAgICBhdmcgPSBtZWFuKHBzZiksXG4gICAgICAgICAgICBtZWRpYW4gPSBtZWRpYW4ocHNmKSlcbmBgYCJ9 -->

```r
# Bedroom: Bedrooms above grade (does NOT include basement bedrooms)
train %>%
  group_by(BedroomAbvGr) %>%
  summarise(count = n(),
            avg = mean(psf),
            median = median(psf))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibmNvbCI6NCwibnJvdyI6OH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERpaXVCaVlHQmdZbUJtWVdSZ1lnWXlXWmlBQkNNREN3TW5pSzVnWUdBV0Jva0NNUzhRY3pCQUFDTllFMUFTS3NjS3hHeFFlWmc2RU44SXFEUU5xRXdGeUw0S3hLSkF6QTdWendkUzUyRENvQlBXS3RUcVlLdTlMZjdnbW4wT0ZsblBiWFRNQWgyTXQydEpsKzYvNzJEczBMOTU5b1pkRGdaLzlZdFN0VFk1R0dUdXNMTDZYT2RnRlBYamRxZnBJYmc1bXRvWElpVW1IM2F3ZTFmS2szQXB4c0Z3bDhmaVJHVWJCOE9ieTF6WUNqSWNES3RjNzUwbzZuYlFlL0l4ejEvc3FZT2hidTMzTU1kOUNITlFQTTZhbkpOWVhBeGtDQ0FKY3FVa2xpVHFwUlVsNXFhaUs4OERpc0dVczBBRmVaeFNVNHJ5ODNNZGs4cmNpK0RtNXBmbWxVQTV6SWxsNlZBbVcyNXFTbVppSHBxeG5FWDU1WG93bzBIQnl0UUFKUDcvLy84RFNQMURVOHllWDFDU21aOEhWTW9rREkwUlpNY3pGcUVKQ0pUbWdZeE8wVTNPS00zTDFyVzBCUGtRR2pVTVVQc1lrYUtVRVJMVklEdVovMFBOWW9VNVB6VXZQVE12RmViSm5NU2sxQndvaHcvb0I3QVg5QXFLTXVGZTV3S0tGdXVWNUpja3d0UnhKZWZud0VUQW5tUDRCd0FjL2xROW9BSUFBQT09In0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["BedroomAbvGr"],"name":[1],"type":["int"],"align":["right"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]},{"label":["avg"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"0","2":"6","3":"20.00068","4":"12.58557"},{"1":"1","2":"50","3":"29.17075","4":"30.93147"},{"1":"2","2":"358","3":"24.41759","4":"17.72767"},{"1":"3","2":"804","3":"19.71549","4":"17.85019"},{"1":"4","2":"213","3":"19.25219","4":"17.47763"},{"1":"5","2":"21","3":"16.98901","4":"15.44715"},{"1":"6","2":"7","3":"16.41297","4":"17.17770"},{"1":"8","2":"1","3":"18.35536","4":"18.35536"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[8]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucDEgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihCZWRyb29tQWJ2R3IpLCB5ID0gcHNmLCBmaWxsID0gIGFzLmZhY3RvcihCZWRyb29tQWJ2R3IpKSkgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKSArXG4gIGxhYnMoeCA9IFwiXCIsIHkgPSBcIlByaXplIFBlciBTcUZ0LlwiKVxucDIgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihCZWRyb29tQWJ2R3IpLCBmaWxsID0gIGFzLmZhY3RvcihCZWRyb29tQWJ2R3IpKSkgK1xuICBnZW9tX2JhcigpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpK1xuICBsYWJzKHggPSBcIlwiKVxucDMgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihCZWRyb29tQWJ2R3IpLCB5ID1wc2YsICBmaWxsID0gIGFzLmZhY3RvcihCZWRyb29tQWJ2R3IpKSkgK1xuICBnZW9tX2JhcihzdGF0ID0gXCJzdW1tYXJ5XCIsIGZ1bi55ID0gXCJtZWFuXCIpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpK1xuICBsYWJzKHggPSBcIkJlZHJvb21BYnZHclwiKVxubGF5b3V0IDwtIG1hdHJpeChjKDEsMSwxLDIsMiwyLDMsMywzKSwzLDMsYnlyb3c9VFJVRSlcbm11bHRpcGxvdChwMSwgcDIsIHAzLCBsYXlvdXQ9bGF5b3V0KVxuYGBgIn0= -->

```r
p1 <- ggplot(train, aes(x = as.factor(BedroomAbvGr), y = psf, fill =  as.factor(BedroomAbvGr))) +
  geom_boxplot() +
  theme(legend.position = "none") +
  labs(x = "", y = "Prize Per SqFt.")
p2 <- ggplot(train, aes(x = as.factor(BedroomAbvGr), fill =  as.factor(BedroomAbvGr))) +
  geom_bar() +
  theme(legend.position = "none")+
  labs(x = "")
p3 <- ggplot(train, aes(x = as.factor(BedroomAbvGr), y =psf,  fill =  as.factor(BedroomAbvGr))) +
  geom_bar(stat = "summary", fun.y = "mean") +
  theme(legend.position = "none")+
  labs(x = "BedroomAbvGr")
layout <- matrix(c(1,1,1,2,2,2,3,3,3),3,3,byrow=TRUE)
multiplot(p1, p2, p3, layout=layout)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucDEgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihLaXRjaGVuQWJ2R3IpLCB5ID0gcHNmLCBmaWxsID0gIGFzLmZhY3RvcihLaXRjaGVuQWJ2R3IpKSkgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKSArXG4gIGxhYnMoeCA9IFwiXCIsIHkgPSBcIlByaXplIFBlciBTcUZ0LlwiKVxucDIgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihLaXRjaGVuQWJ2R3IpLCBmaWxsID0gIGFzLmZhY3RvcihLaXRjaGVuQWJ2R3IpKSkgK1xuICBnZW9tX2JhcigpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpK1xuICBsYWJzKHggPSBcIlwiKVxucDMgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihLaXRjaGVuQWJ2R3IpLCB5ID1wc2YsICBmaWxsID0gIGFzLmZhY3RvcihLaXRjaGVuQWJ2R3IpKSkgK1xuICBnZW9tX2JhcihzdGF0ID0gXCJzdW1tYXJ5XCIsIGZ1bi55ID0gXCJtZWFuXCIpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpK1xuICBsYWJzKHggPSBcIktpdGNoZW5BYnZHclwiLCB5ID0gXCJNZWFuXCIpXG5sYXlvdXQgPC0gbWF0cml4KGMoMSwxLDEsMiwyLDIsMywzLDMpLDMsMyxieXJvdz1UUlVFKVxubXVsdGlwbG90KHAxLCBwMiwgcDMsIGxheW91dD1sYXlvdXQpXG5gYGAifQ== -->

```r
p1 <- ggplot(train, aes(x = as.factor(KitchenAbvGr), y = psf, fill =  as.factor(KitchenAbvGr))) +
  geom_boxplot() +
  theme(legend.position = "none") +
  labs(x = "", y = "Prize Per SqFt.")
p2 <- ggplot(train, aes(x = as.factor(KitchenAbvGr), fill =  as.factor(KitchenAbvGr))) +
  geom_bar() +
  theme(legend.position = "none")+
  labs(x = "")
p3 <- ggplot(train, aes(x = as.factor(KitchenAbvGr), y =psf,  fill =  as.factor(KitchenAbvGr))) +
  geom_bar(stat = "summary", fun.y = "mean") +
  theme(legend.position = "none")+
  labs(x = "KitchenAbvGr", y = "Mean")
layout <- matrix(c(1,1,1,2,2,2,3,3,3),3,3,byrow=TRUE)
multiplot(p1, p2, p3, layout=layout)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uIDogQWx0aG91Z2ggbWVhbiBpcyBkaWZmZXJlbnQsIG1lZGlhbiBpcyBub3RcbmBgYCJ9 -->

```r
# Conclusion : Although mean is different, median is not
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucDEgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IEtpdGNoZW5RdWFsLCB5ID0gcHNmLCBmaWxsID0gIEtpdGNoZW5RdWFsKSkgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKSArXG4gIGxhYnMoeCA9IFwiXCIsIHkgPSBcIlByaXplIFBlciBTcUZ0LlwiKVxucDIgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IEtpdGNoZW5RdWFsLCBmaWxsID0gIEtpdGNoZW5RdWFsKSkgK1xuICBnZW9tX2JhcigpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpK1xuICBsYWJzKHggPSBcIlwiKVxucDMgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IEtpdGNoZW5RdWFsLCB5ID1wc2YsICBmaWxsID0gIEtpdGNoZW5RdWFsKSkgK1xuICBnZW9tX2JhcihzdGF0ID0gXCJzdW1tYXJ5XCIsIGZ1bi55ID0gXCJtZWFuXCIpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpK1xuICBsYWJzKHggPSBcIktpdGNoZW5RdWFsXCIsIHkgPSBcIk1lYW5cIilcbmxheW91dCA8LSBtYXRyaXgoYygxLDEsMSwxLDIsMiwzLDMpLDIsNCxieXJvdz1UUlVFKVxubXVsdGlwbG90KHAxLCBwMiwgcDMsIGxheW91dD1sYXlvdXQpXG5gYGAifQ== -->

```r
p1 <- ggplot(train, aes(x = KitchenQual, y = psf, fill =  KitchenQual)) +
  geom_boxplot() +
  theme(legend.position = "none") +
  labs(x = "", y = "Prize Per SqFt.")
p2 <- ggplot(train, aes(x = KitchenQual, fill =  KitchenQual)) +
  geom_bar() +
  theme(legend.position = "none")+
  labs(x = "")
p3 <- ggplot(train, aes(x = KitchenQual, y =psf,  fill =  KitchenQual)) +
  geom_bar(stat = "summary", fun.y = "mean") +
  theme(legend.position = "none")+
  labs(x = "KitchenQual", y = "Mean")
layout <- matrix(c(1,1,1,1,2,2,3,3),2,4,byrow=TRUE)
multiplot(p1, p2, p3, layout=layout)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucDEgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihUb3RSbXNBYnZHcmQpLCB5ID0gcHNmLCBmaWxsID0gIGFzLmZhY3RvcihUb3RSbXNBYnZHcmQpKSkgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKSArXG4gIGxhYnMoeCA9IFwiXCIsIHkgPSBcIlByaXplIFBlciBTcUZ0LlwiKVxucDIgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihUb3RSbXNBYnZHcmQpLCBmaWxsID0gIGFzLmZhY3RvcihUb3RSbXNBYnZHcmQpKSkgK1xuICBnZW9tX2JhcigpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpK1xuICBsYWJzKHggPSBcIlwiKVxucDMgPC0gZ2dwbG90KHRyYWluLCBhZXMoeCA9IGFzLmZhY3RvcihUb3RSbXNBYnZHcmQpLCB5ID1wc2YsICBmaWxsID0gIGFzLmZhY3RvcihUb3RSbXNBYnZHcmQpKSkgK1xuICBnZW9tX2JhcihzdGF0ID0gXCJzdW1tYXJ5XCIsIGZ1bi55ID0gXCJtZWFuXCIpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpK1xuICBsYWJzKHggPSBcIlRvdFJtc0FidkdyZFwiLCB5ID0gXCJNZWFuXCIpXG5sYXlvdXQgPC0gbWF0cml4KGMoMSwxLDEsMSwyLDIsMywzKSwyLDQsYnlyb3c9VFJVRSlcbm11bHRpcGxvdChwMSwgcDIsIHAzLCBsYXlvdXQ9bGF5b3V0KVxuYGBgIn0= -->

```r
p1 <- ggplot(train, aes(x = as.factor(TotRmsAbvGrd), y = psf, fill =  as.factor(TotRmsAbvGrd))) +
  geom_boxplot() +
  theme(legend.position = "none") +
  labs(x = "", y = "Prize Per SqFt.")
p2 <- ggplot(train, aes(x = as.factor(TotRmsAbvGrd), fill =  as.factor(TotRmsAbvGrd))) +
  geom_bar() +
  theme(legend.position = "none")+
  labs(x = "")
p3 <- ggplot(train, aes(x = as.factor(TotRmsAbvGrd), y =psf,  fill =  as.factor(TotRmsAbvGrd))) +
  geom_bar(stat = "summary", fun.y = "mean") +
  theme(legend.position = "none")+
  labs(x = "TotRmsAbvGrd", y = "Mean")
layout <- matrix(c(1,1,1,1,2,2,3,3),2,4,byrow=TRUE)
multiplot(p1, p2, p3, layout=layout)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZmFjdG9yQ2hhcnQgPC0gZnVuY3Rpb24gKGRmLCB2YWwxLCB2YWwyKSB7XG4gIHAxIDwtIGdncGxvdChkZiwgYWVzKHggPSBhcy5mYWN0b3IoZGZbW3ZhbDFdXSksIHkgPSBkZltbdmFsMl1dLCBmaWxsID0gIGFzLmZhY3RvcihkZltbdmFsMV1dKSkpICtcbiAgICBnZW9tX2JveHBsb3QoKSArXG4gICAgdGhlbWUobGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpICtcbiAgICBsYWJzKHggPSB2YWwxLCB5ID0gdmFsMilcbiAgXG4gIHAyIDwtIGdncGxvdChkZiwgYWVzKHggPSBhcy5mYWN0b3IoZGZbW3ZhbDFdXSksIGZpbGwgPSAgYXMuZmFjdG9yKGRmW1t2YWwxXV0pKSkgK1xuICAgIGdlb21fYmFyKCkgK1xuICAgIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiKStcbiAgICBsYWJzKHggPSB2YWwxKVxuICBcbiAgcDMgPC0gZ2dwbG90KGRmLCBhZXMoeCA9IGFzLmZhY3RvcihkZltbdmFsMV1dKSwgeSA9IGRmW1t2YWwyXV0sICBmaWxsID0gIGFzLmZhY3RvcihkZltbdmFsMV1dKSkpICtcbiAgICBnZW9tX2JhcihzdGF0ID0gXCJzdW1tYXJ5XCIsIGZ1bi55ID0gXCJtZWFuXCIpICtcbiAgICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIikrXG4gICAgbGFicyh4ID0gdmFsMSwgeSA9IFwiTWVhblwiKVxuICBcbiAgbGF5b3V0IDwtIG1hdHJpeChjKDEsMSwxLDEsMiwyLDMsMyksMiw0LGJ5cm93PVRSVUUpXG4gIG11bHRpcGxvdChwMSwgcDIsIHAzLCBsYXlvdXQ9bGF5b3V0KSAgXG59XG5gYGAifQ== -->

```r
factorChart <- function (df, val1, val2) {
  p1 <- ggplot(df, aes(x = as.factor(df[[val1]]), y = df[[val2]], fill =  as.factor(df[[val1]]))) +
    geom_boxplot() +
    theme(legend.position = "none") +
    labs(x = val1, y = val2)
  
  p2 <- ggplot(df, aes(x = as.factor(df[[val1]]), fill =  as.factor(df[[val1]]))) +
    geom_bar() +
    theme(legend.position = "none")+
    labs(x = val1)
  
  p3 <- ggplot(df, aes(x = as.factor(df[[val1]]), y = df[[val2]],  fill =  as.factor(df[[val1]]))) +
    geom_bar(stat = "summary", fun.y = "mean") +
    theme(legend.position = "none")+
    labs(x = val1, y = "Mean")
  
  layout <- matrix(c(1,1,1,1,2,2,3,3),2,4,byrow=TRUE)
  multiplot(p1, p2, p3, layout=layout)  
}
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZmFjdG9yQ2hhcnQodHJhaW4sIFwiVG90Um1zQWJ2R3JkXCIsIFwicHNmXCIpXG5gYGAifQ== -->

```r
factorChart(train, "TotRmsAbvGrd", "psf")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->






Add a new chunk by clicking the *Insert Chunk* button on the toolbar or by pressing *Ctrl+Alt+I*.

When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the *Preview* button or press *Ctrl+Shift+K* to preview the HTML file).

<!-- rnb-text-end -->
