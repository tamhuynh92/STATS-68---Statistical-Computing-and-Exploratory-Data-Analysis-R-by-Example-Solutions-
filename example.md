---
title: "Chapter 4"
output: html_document
---




### Chapter 4: Presentation Graphic
#### Example 4.1 (Home run hitting in baseball history).



```r
setwd("/Users/huynh/Downloads")
hitting.data = read.table("batting.history.txt", header=TRUE, sep ="\t")
attach(hitting.data)
plot(Year, HR)
```

### 4.2 Labeling the Axes and Adding a Title


```r
plot(Year, HR, xlab="Season", ylab="Avg HR Hit Per Team Per Game", main="Home Run Hitting in the MLB Across Seasons")
```

### 4.3 Changing the Plot Type and Plotting Symbol<br>
type = "l": connect the points with lines <br>
type = "n": show no points<br>
type = "b": show both points and connecting lines <br>

xaxt = "n" : no x axes to be draw<br>
yaxt = "n" : no y axes to be draw<br>
pch: plotting symbols<br>
cex: magnifies the symbols to x times their usual size<br>
text: display text on the current graph


```r
plot(Year, HR, type = "l", xlab="Season", ylab="Avg. Home Runs Hit by a Team in a Game", 
                                      main="Home Run Hitting in the MLB Across Seasons")
```

```r
row = rep(1:3, each=7)
col = rep(1:7, times=3)
plot(2, 3, xlim=c(.5,3.5), ylim=c(.5,7.5), type="n", xaxt = "n", yaxt = "n", xlab="", ylab="")
points(row, col, pch=0:20, cex=3)
text(row, col, 0:20, pos=4, offset=2, cex=1.5)
title("Plotting Symbols with the pch Argument")
```

```r
plot(Year, HR, xlab="Season", cex=1.5, pch=19, ylab="Avg. Home Runs Hit by a Team in a Game",
                                            main="Home Run Hitting in the MLB Across Seasons")
```

### 4.4 Overalying Lines and Line Types


```r
plot(Year, HR, xlab="Season", ylab="Avg. Home Runs Hit by a Team in a Game", main="Home Run Hitting in the MLB Across Seasons")
lines(lowess(Year, HR))
```

```r
plot(0, 0, type="n", xlim=c(-2, 2), ylim=c(-2, 2), xaxt="n", yaxt="n", xlab="", ylab="")
y = seq(2, -3, -1)
for(j in 1:6)
    abline(a=y[j], b=1, lty=j, lwd=2)
legend("topleft", legend=c("solid", "dashed", "dotted", "dotdash", "longdash", "twodash"), lty=1:6, lwd=2)
title("Line Styles with the lty Argument")
```

```r
plot(Year, HR, xlab="Season", ylab="Avg. Home Runs Hit by a Team in a Game", main="Home Run Hitting in the MLB Across Seasons")
lines(lowess(Year, HR), lwd=2)
lines(lowess(Year, HR, f=1 / 3), lty="dashed", lwd=2)
lines(lowess(Year, HR, f=1 / 12), lty="dotdash", lwd=2)
legend("topleft", legend=c("f = 2/3", "f = 1/3", "f = 1/12"), lty=c(1, 2, 4), lwd=2, inset=0.05)
```

```r
plot(1:10, c(5, 4, 3, 2, 1, 2, 3, 4, 3, 2), pch=13, cex=2, col=c("red", "blue", "green", "beige", "goldenrod",
                                                             "turquoise", "salmon", "purple", "pink", "seashell"))
```

### 4.6 Changing the Format of Text


```r
plot(0, 0, type="n", xlim=c(-1, 6), ylim=c(-0.5, 4), xaxt="n", yaxt ="n", xlab="", ylab="", 
                                         main="Font Choices Using, font, family and srt Arguments")
text(2.5, 4, "font = 1 (Default)")
text(1, 3, "font = 2 (Bold)", font=2, cex=1.0)
text(1, 2, "font = 3 (Italic)", font=3, cex=1.0)
text(1, 1, "font = 4 (Bold Italic), srt = 20", font=4, cex=1.0, srt=20)
text(4, 3, family="serif", cex=1.0, family="serif")
text(4, 2, family="sans", cex=1.0, family="sans")
text(4, 1, family="mono", cex=1.0, family="mono")
text(2.5, 0, family = "HersheyScript", cex=2.5, family="HersheyScript", col="red")
```

### 4.7 Interacting with the Graph


```r
fit = lowess(Year, HR, f=1 / 12)
Residual = HR - fit$y
plot(Year, Residual)
abline(h=0)
identify(Year, Residual, n=2, labels=Year)
```

### 4.8 Multiple Figures in a Window


```r
par(mfrow=c(2, 1))
plot(Year, HR, xlab="Season", ylab="Avg HR Hit Per Team Per Game", main="Home Run Hitting in the MLB Across Seasons")
lines(fit, lwd=2)
plot(Year, Residual, xlab="Season", main="Residuals from Lowess Fit")
abline(h=0)
```

### 4.9 Overlaying a Curve and Adding a Mathematical Expression


```r
n = 20; p = 0.2
y = 0:20
py = dbinom(y, size=n, prob=p)
plot(y, py, type="h", lwd=3, xlim=c(0, 15), ylab="Prob(y)")
mu = n * p; sigma = sqrt(n * p * (1 - p))
curve(dnorm(x, mu, sigma), add=TRUE, lwd=2, lty=2)
text(10, 0.15, expression(paste(frac(1, sigma*sqrt(2*pi)), " ", e^{frac(-(y-mu)^2, 2*sigma^2)})), cex = 1.5)
title("Binomial probs with n=2, p=0.2, and matching normal curve")
locs = locator(2)
```

### 4.10 Multiple Plots and Varying the Graphical Parameters


```r
snow.yr1 = c(85.9, 71.4, 68.8, 58.8, 34.4)
snow.yr2 = c(150.9, 102.0, 86.2, 80.1, 63.8)
#windows(width=5, height=7)
layout(matrix(c(1, 2), ncol=1), heights=c(6, 4))
par(plt=c(0.20, 0.80, 0, 0.88), xaxt="n")
plot(snow.yr1, snow.yr2, xlim=c(30, 100), ylim=c(30, 155), ylab="2010-11 Snowfall (in)", pch=19, main="Snowfall in Five New York Cities")
abline(a=0, b=1)
text(80, 145, "Syracuse")
tm = par("yaxp")
ticmarks = seq(tm[1], tm[2], length=tm[3]+1) 
axis(4, at=ticmarks, labels=as.character(round(2.54 * ticmarks, -1)))
mtext("2010-11 Snowfall (cm)", side=4, line=3)
par(plt=c(0.20, 0.80, 0.35, 0.95), xaxt="s")
plot(snow.yr1, snow.yr2 - snow.yr1, xlim=c(30, 100),xlab="2009-10 Snowfall (in)", pch=19,
     ylab="Increase (in)")
text(80, 60, "Syracuse")
tm=par("yaxp")
ticmarks=seq(tm[1], tm[2], length=tm[3] + 1)
axis(4, at=ticmarks, labels=as.character(round(2.54 * ticmarks, -1)))
mtext("Increase (cm)", side=4, line=3)
```

### 4.11 Creating a plot using Low-Level Functions


```r
plot.new()
plot.window(xlim=c(-1.5, 1.5), ylim=c(-1.5, 1.5), pty="s")
theta = seq(0, 2*pi, length=100)
lines(cos(theta), sin(theta))
theta=seq(0, 2*pi, length=7)[-7]
points(cos(theta), sin(theta), cex=3, pch=19)
pos = locator(6)
box()
```

### 4.12 Exporting a Graph to a Graphics File


```r
pdf("homerun.pdf")
plot(Year, HR, xlab="Season",ylab="Avg. Home Runs Hit by a Team in a Game", main="Home Run Hitting in the MLB Across Seasons")
lines(lowess(Year, HR))
lines(lowess(Year, HR, f=1 / 3), lty=2)
lines(lowess(Year, HR, f=1 / 6), lty=3)
legend("topleft", legend=c("f = 2/3", "f = 1/3", "f = 1/6"), lty=c(1, 2, 3))
dev.off()
```

### 4.13 The lattice Package


```r
library(lattice)
xyplot(mpg ~ wt, data=mtcars, xlab="Weight", ylab="Mileage", main="Scatterplot of Weight and Mileage for 32 Cars")
```

```r
xyplot(mpg ~ wt | cyl, data=mtcars, pch=19, cex=1.5, xlab="Weight", ylab="Mileage")
```

```r
densityplot(~ wt, groups=cyl, data=mtcars, auto.key=list(space="top"))
```

```r
library(lattice)
cloud(z ~ x + y, data = randu)
```