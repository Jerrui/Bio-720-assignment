---
title: "Bio720 assignment11.7"
author: "Jerry"
date: "2018Äê11ÔÂ7ÈÕ"
output: 
  html_document: 
    keep_md: yes
---

**Q2**
y = TRUE : calculate mean expression. y = FALSE : calculate log2 mean expression. 

```r
MyData <- read.csv(file="C:\\Users\\jerry\\Desktop\\eXpress_dm_counts.csv", header=TRUE,row.names = 1, sep=",")
rna_counts = function(x, y = TRUE ){
  if (y == TRUE) {
  a <- mean(MyData[,x])
  } else {
  MyData = MyData + 0.000001
  a <- mean(log2(MyData[,x]))
  }
  return(a)
}
rna_counts('F101_lg_female_hdhorn',FALSE)
```

```
## [1] 8.795177
```
**Q3**

```r
colname_MyData <- colnames(MyData)
elements <- c()
for(i in colname_MyData){
  elements <- c(elements, rna_counts(i))
}
names(elements) <- colname_MyData
elements
```

```
##  F101_lg_female_hdhorn F101_lg_female_thxhorn   F101_lg_female_wings 
##               1978.847               1983.250               1583.904 
##  F105_lg_female_hdhorn F105_lg_female_thxhorn   F105_lg_female_wings 
##               2105.712               1433.749               1869.962 
##  F131_lg_female_hdhorn F131_lg_female_thxhorn   F131_lg_female_wings 
##               2117.847               2307.529               2272.692 
##   F135_sm_female_wings  F135_sm_female_hdhorn F135_sm_female_thxhorn 
##               1728.483               1452.913               1776.309 
##  F136_sm_female_hdhorn F136_sm_female_thxhorn   F136_sm_female_wings 
##               2065.780               1777.769               1988.882 
##  F196_sm_female_hdhorn F196_sm_female_thxhorn   F196_sm_female_wings 
##               1348.898               1025.301               3067.287 
##  F197_sm_female_hdhorn F197_sm_female_thxhorn   F197_sm_female_wings 
##               2639.152               2047.151               2081.889 
##  F218_lg_female_hdhorn F218_lg_female_thxhorn   F218_lg_female_wings 
##               2329.563               1950.561               2074.992 
## M120_sm_male_genitalia    M120_sm_male_hdhorn   M120_sm_male_thxhorn 
##               1832.780               2105.145               2101.163 
##     M120_sm_male_wings M125_lg_male_genitalia    M125_lg_male_hdhorn 
##               2536.920               2088.092               2372.259 
##     M125_lg_male_wings M160_lg_male_genitalia    M160_lg_male_hdhorn 
##               2559.085               1727.538               2111.337 
##   M160_lg_male_thxhorn     M160_lg_male_wings M171_sm_male_genitalia 
##               2087.583               2184.076               2035.093 
##    M171_sm_male_hdhorn   M171_sm_male_thxhorn     M171_sm_male_wings 
##               1598.190               1621.659               1825.344 
## M172_sm_male_genitalia    M172_sm_male_hdhorn   M172_sm_male_thxhorn 
##               2196.101               1713.119               1344.019 
##     M172_sm_male_wings M180_lg_male_genitalia    M180_lg_male_hdhorn 
##               2602.351               1922.634               2670.498 
##   M180_lg_male_thxhorn     M180_lg_male_wings M200_sm_male_genitalia 
##               2003.293               3216.476               2412.038 
##    M200_sm_male_hdhorn   M200_sm_male_thxhorn     M200_sm_male_wings 
##               2032.085               2820.495               2203.813 
## M257_lg_male_genitalia    M257_lg_male_hdhorn   M257_lg_male_thxhorn 
##               2170.258               2361.912               2749.767 
##     M257_lg_male_wings 
##               1325.684
```


**Q4**
For loop is faster on "user" and "elapsed". They were the same on "system"(0).

```r
system.time(sapply(colname_MyData, rna_counts))
```

```
##    user  system elapsed 
##       0       0       0
```

```r
system.time(for(i in colname_MyData){elements <- c(elements, rna_counts(i))})
```

```
##    user  system elapsed 
##    0.03    0.00    0.03
```
**Q5**

```r
sapply(MyData, mean)
```

```
##  F101_lg_female_hdhorn F101_lg_female_thxhorn   F101_lg_female_wings 
##               1978.847               1983.250               1583.904 
##  F105_lg_female_hdhorn F105_lg_female_thxhorn   F105_lg_female_wings 
##               2105.712               1433.749               1869.962 
##  F131_lg_female_hdhorn F131_lg_female_thxhorn   F131_lg_female_wings 
##               2117.847               2307.529               2272.692 
##   F135_sm_female_wings  F135_sm_female_hdhorn F135_sm_female_thxhorn 
##               1728.483               1452.913               1776.309 
##  F136_sm_female_hdhorn F136_sm_female_thxhorn   F136_sm_female_wings 
##               2065.780               1777.769               1988.882 
##  F196_sm_female_hdhorn F196_sm_female_thxhorn   F196_sm_female_wings 
##               1348.898               1025.301               3067.287 
##  F197_sm_female_hdhorn F197_sm_female_thxhorn   F197_sm_female_wings 
##               2639.152               2047.151               2081.889 
##  F218_lg_female_hdhorn F218_lg_female_thxhorn   F218_lg_female_wings 
##               2329.563               1950.561               2074.992 
## M120_sm_male_genitalia    M120_sm_male_hdhorn   M120_sm_male_thxhorn 
##               1832.780               2105.145               2101.163 
##     M120_sm_male_wings M125_lg_male_genitalia    M125_lg_male_hdhorn 
##               2536.920               2088.092               2372.259 
##     M125_lg_male_wings M160_lg_male_genitalia    M160_lg_male_hdhorn 
##               2559.085               1727.538               2111.337 
##   M160_lg_male_thxhorn     M160_lg_male_wings M171_sm_male_genitalia 
##               2087.583               2184.076               2035.093 
##    M171_sm_male_hdhorn   M171_sm_male_thxhorn     M171_sm_male_wings 
##               1598.190               1621.659               1825.344 
## M172_sm_male_genitalia    M172_sm_male_hdhorn   M172_sm_male_thxhorn 
##               2196.101               1713.119               1344.019 
##     M172_sm_male_wings M180_lg_male_genitalia    M180_lg_male_hdhorn 
##               2602.351               1922.634               2670.498 
##   M180_lg_male_thxhorn     M180_lg_male_wings M200_sm_male_genitalia 
##               2003.293               3216.476               2412.038 
##    M200_sm_male_hdhorn   M200_sm_male_thxhorn     M200_sm_male_wings 
##               2032.085               2820.495               2203.813 
## M257_lg_male_genitalia    M257_lg_male_hdhorn   M257_lg_male_thxhorn 
##               2170.258               2361.912               2749.767 
##     M257_lg_male_wings 
##               1325.684
```

**Q6**

```r
rowmean_counts = function(x, y = TRUE ){
  
  if (y == TRUE) {
    a <- rowMeans(MyData[x,])
  } else {
    MyData = MyData + 0.000001
    a <- rowMeans(log2(MyData[x,]))
  }
  return(a)
}
rowmean <- sapply(rownames(MyData), rowmean_counts)
```

**Q7**

```r
male_lg_hdhorn <- MyData[,grep('M.*lg_male_hdhorn', colname_MyData, value = TRUE)]
male_sm_hdhorn <- MyData[,grep('M.*sm_male_hdhorn', colname_MyData, value = TRUE)]
rowmean_counts_male = function(x, y = TRUE, z ){
  if (y == TRUE) {
    a <- rowMeans(z[x,])
  } else {
    z = z + 0.000001
    a <- rowMeans(log2(z[x,]))
  }
  return(a)
}
male_lg_hdhorn_mean <- sapply(rownames(MyData),z = male_lg_hdhorn, rowmean_counts_male)
male_sm_hdhorn_mean <- sapply(rownames(MyData),z = male_sm_hdhorn, rowmean_counts_male)
mean_difference = male_lg_hdhorn_mean - male_sm_hdhorn_mean
male_lg_hdhorn_logmean <- sapply(rownames(MyData),y = FALSE, z = male_lg_hdhorn, rowmean_counts_male) 
male_sm_hdhorn_logmean <- sapply(rownames(MyData),y = FALSE, z = male_sm_hdhorn, rowmean_counts_male)
logmean_difference = male_lg_hdhorn_logmean - male_sm_hdhorn_logmean
```

**Q8**

```r
male_hdhorn <- MyData[,grep('M.*_male_hdhorn', colname_MyData, value = TRUE)]
mean <- sapply(rownames(MyData),z = male_hdhorn, rowmean_counts_male)
logmean <- sapply(rownames(MyData),y = FALSE, z = male_hdhorn, rowmean_counts_male)
plot(mean, mean_difference,xlab = "Mean expression of each gene in male head horns", ylab = "Mean difference between large male and small males (for head horns)", main="Mean expression") 
```

![](222222_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

```r
plot(logmean, logmean_difference,xlab = "LogMean expression of each gene in male head horns", ylab = "LogMean difference between large male and small males (for head horns)", main="LogMean expression")
```

![](222222_files/figure-html/unnamed-chunk-7-2.png)<!-- -->

For the bonus question, I think using "dplyr"  is aslo able to do those operations.
