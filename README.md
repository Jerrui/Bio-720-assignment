# Bio-720-assignment
**Q2**
y = TRUE : calculate mean expression. y = FALSE : calculate log2 mean expression. 
```{r}
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
**Q3**
```{r}
colname_MyData <- colnames(MyData)
elements <- c()
for(i in colname_MyData){
  elements <- c(elements, rna_counts(i))
}
names(elements) <- colname_MyData
elements
```


**Q4**
For loop is faster on "user" and "elapsed". They were the same on "system"(0).
```{r}
system.time(sapply(colname_MyData, rna_counts))
system.time(for(i in colname_MyData){elements <- c(elements, rna_counts(i))})
```
**Q5**
```{r}
sapply(MyData, mean)
```

**Q6**
```{r}
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
```{r}
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
```{r}
male_hdhorn <- MyData[,grep('M.*_male_hdhorn', colname_MyData, value = TRUE)]
mean <- sapply(rownames(MyData),z = male_hdhorn, rowmean_counts_male)
logmean <- sapply(rownames(MyData),y = FALSE, z = male_hdhorn, rowmean_counts_male)
plot(mean, mean_difference,xlab = "Mean expression of each gene in male head horns", ylab = "Mean difference between large male and small males (for head horns)", main="Mean expression") 
plot(logmean, logmean_difference,xlab = "LogMean expression of each gene in male head horns", ylab = "LogMean difference between large male and small males (for head horns)", main="LogMean expression")
```

For the bonus question, I think using "dplyr"  is aslo able to do those operations.
