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
## % Thu Feb 11 15:52:19 2016
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
rm(list=keep(OBJECT.))  # remove all elements in ls() except OBJECT.
```



# Change `.pdf` image files to `.png`

## One single `.pdf`


```r
library("animation")
ani.options(outdir = getwd())

pdf("bm.pdf")
plot(1:10)
dev.off()

im.convert("bm.pdf", output = "bm.jpeg")
im.convert("bm.pdf", output = "bm.png")
```

## Several `.pdf` files




```r
# read all files with .pdf extension
files <- list.files(pattern = "\\.(pdf|PDF)$")
newfiles<-sub(pattern=".pdf",replacement=".png",files)
# convert pdf to png
library(animation)
for(i in 1:length(files)){
  im.convert(files[i],output=newfiles[i],clean=FALSE)
}
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

