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
## % Thu Feb 11 12:14:33 2016
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



+--------+---------+--------+---------+
| 0.4684 | 0.3165  | 0.3534 | 0.3392  |
+--------+---------+--------+---------+
| 0.8103 | 0.8394  | 0.418  | 0.03921 |
+--------+---------+--------+---------+
| 0.4175 | 0.02549 | 0.8655 | 0.1014  |
+--------+---------+--------+---------+

Table: make it table with pander

# Extract Rnw Sweave Rmd Knitr files to *.R


```r
library(knitr)

purl("File.Rmd",output="File.R")

# In RSweave

Stangle("File.Rnw",output="File.R")
```

# Working with data frames in R

## Drop unused factor levels


```r
library(gdata)
drop.levels(x, reorder=TRUE, ...)
```

#  Remove all elements in R except a few specified


```r
library(gdata) # function keep()
```

```
## gdata: read.xls support for 'XLS' (Excel 97-2004) files ENABLED.
```

```
## 
```

```
## gdata: read.xls support for 'XLSX' (Excel 2007+) files ENABLED.
```

```
## 
## Attaching package: 'gdata'
```

```
## The following object is masked from 'package:stats':
## 
##     nobs
```

```
## The following object is masked from 'package:utils':
## 
##     object.size
```

```r
rm(list=keep(OBJECT.))  # remove all elements in ls() except OBJECT.
```

```
## Warning in keep(OBJECT.): you tried to keep "OBJECT." which doesn't exist
## in workspace - nothing was removed
```

-----------------------------------------------------

**Contact**

Alameda de Mazarredo, 14

E-48009 Bilbao, Basque Country - Spain

Tel: +34 946 567 842 (Ext. 277)

Fax: +34 946 567 843

**email:** dlee[at]bcamath.org

**Github** [idaejin](https://github.com/idaejin/)

**BCAM webpage** [dlee](http://www.bcamath.org/en/people/dlee)

<img src="http://www.bcamath.org/public_images/logo_bcam.jpg" style="width: 150px;" align="right">

