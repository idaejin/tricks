---
title: "Some Useful Tricks"
author: '@idaejin'
date: ""
output:
  html_document:
    highlight: haddock
    keep_md: yes
    number_sections: yes
    theme: spacelab
    toc: yes
---


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
## % latex table generated in R 3.5.2 by xtable 1.8-3 package
## % Wed Mar 27 19:36:33 2019
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

# create a new vble with .png extension 
newfiles<-sub(pattern=".pdf",replacement=".png",files)
# convert pdf to png
library(animation)
for(i in 1:length(files)){
  im.convert(files[i],output=newfiles[i],clean=FALSE)
}
```

# Convert `.pdf` files to `.eps` using **Inkscape** converter

This requires **Inkscape** (and MacOS)

- A single file

```r
/Applications/Inkscape.app/Contents/Resources/bin/inkscape --export-eps test.eps -w 1024 -h 768 test.pdf
```
or 

```r
/Applications/Inkscape.app/Contents/Resources/bin/inkscape -z -E test.eps test.pdf
```

This is not the most efficient code, but it works :P


```r
# read all files with .pdf extension
pdf.files <- list.files(pattern = "\\.(pdf|PDF)$")
# create a new vble with .eps extension 
eps.files<-sub(pattern=".pdf",replacement=".eps",pdf.files)

# create a pdf2eps.sh bash file and run it from R
sh.file <- file("pdf2eps.sh","w")
writeLines("#!/bin/bash",con=sh.file,sep="\n")
writeLines(paste("/Applications/Inkscape.app/Contents/Resources/bin/inkscape -z -E",eps.files,pdf.files),con=sh.file,sep="\n")
close(sh.file)

# Run bash script from R
system("./pdf2eps.sh")
```

# Save the orientation 3D rgl plot

Found on [stackoverflow.com](http://stackoverflow.com/questions/16362381/save-the-orientation-of-a-rgl-plot3d-plot)


```r
## In an inital session:

library(rgl)
plot3d(iris) 

## Now move the image around to an orientation you like

## Save RGL parameters to a list object
pp <- par3d(no.readonly=TRUE)

## Save the list to a text file
dput(pp, file="irisView.R", control = "all")

## Then, in a later session, to recreate the plot just as you had it:

library(rgl)
pp <- dget("irisView.R")
plot3d(iris)
par3d(pp)
```
# Find points within a rectangle 

source [here](https://stackoverflow.com/questions/34308600/identify-points-within-a-rectangle-in-a-scatterplot)


```r
# function
loc.box <- function(x,y){
  print("choose bottom left corner")
  p1 <- locator(1)
  print("choose top right corner")
  p2 <- locator(1)
  rect(p1$x, p1$y, p2$x, p2$y, border=3, col=rgb(0,1,0,0.1))
  incl <- which(
    x >= p1$x &
    x <= p2$x &
    y >= p1$y &
    y <= p2$y
  )
  return(incl)
}

# data
set.seed(1)
n <- 100
x <- runif(n)
y <- runif(n)

# plot and select
op <- par(ps=9, mar=c(4,4,1,1))
plot(x, y, pch=20, cex=0.3)
text(x, y, labels=seq(x), pos=3)
par(op)
res <- loc.box(x,y)
```

![](index_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

```
## [1] "choose bottom left corner"
## [1] "choose top right corner"
```

```r
res
```

```
## integer(0)
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

