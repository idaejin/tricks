# Some Useful Tricks
@idaejin  


# Convert a matrix into $\LaTeX$

Create a composition matrix 


```r
x = diag(3)%x%matrix(rep(1,5),nrow=1)
x
```

```
##      [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10] [,11] [,12] [,13]
## [1,]    1    1    1    1    1    0    0    0    0     0     0     0     0
## [2,]    0    0    0    0    0    1    1    1    1     1     0     0     0
## [3,]    0    0    0    0    0    0    0    0    0     0     1     1     1
##      [,14] [,15]
## [1,]     0     0
## [2,]     0     0
## [3,]     1     1
```

```r
library(xtable)
x <- xtable(x,digits=0)
print(x, floating=FALSE, tabular.environment="bmatrix",hline.after=NULL, include.rownames=FALSE, include.colnames=FALSE)
```

```
## % latex table generated in R 3.2.0 by xtable 1.7-4 package
## % Thu Feb  4 19:23:32 2016
## \begin{bmatrix}{rrrrrrrrrrrrrrr}
##   1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
##   0 & 0 & 0 & 0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 \\ 
##   0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 & 1 & 1 & 1 \\ 
##   \end{bmatrix}
```

# `library(pander)`


```r
library(pander)
tab <- matrix(runif(3*4),3,4)
panderOptions("table.style", "grid") # "simple"
pander(tab, caption="make it table with pander")
```



+--------+--------+--------+---------+
| 0.8671 | 0.2867 | 0.8021 | 0.9758  |
+--------+--------+--------+---------+
| 0.3958 | 0.806  | 0.8375 | 0.8152  |
+--------+--------+--------+---------+
| 0.948  | 0.6982 | 0.5507 | 0.04105 |
+--------+--------+--------+---------+

Table: make it table with pander
