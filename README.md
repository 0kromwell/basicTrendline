# basicTrendline: an R package for adding trendline of basic regression models to plot

[![cran version](http://www.r-pkg.org/badges/version/basicTrendline)](http://cran.rstudio.com/web/packages/basicTrendline) 
[![rstudio mirror downloads](http://cranlogs.r-pkg.org/badges/grand-total/basicTrendline)](https://github.com/metacran/cranlogs.app)
[![rstudio mirror downloads](http://cranlogs.r-pkg.org/badges/basicTrendline)](https://github.com/metacran/cranlogs.app)
[![HitCount](http://hits.dwyl.io/PhDMeiwp/basicTrendline.svg)](http://hits.dwyl.io/PhDMeiwp/basicTrendline)

## Installing "basicTrendline" package in R

1\. **version 1.0.1** from R (Open R software and run:)

	### version 1.0.1
	
	install.packages("basicTrendline")
	library(basicTrendline)

2\. **version 1.0.2** (Recommend !!!) from Github (change the expression of formula of "exp3P" from y=a\*exp(b\*x)+c to y=a\*e<sup>b\*x</sup>+c )

You can install directly **from GitHub** if you have the devtools package installed:

    ### version 1.0.2
	
	install.packages("devtools")
	library(devtools)   
	install_github("PhDMeiwp/basicTrendline@master", force = TRUE)
	library(basicTrendline)


## Using "basicTrendline" package
	
Then upload your dataset including x and y data, for example

    x<-c(1,30,90,180,360)
    y<-c(4,8,10,11,11)

 **[case 1：] plot and add trendline as default:** 

	library(basicTrendline)

	trendline(x,y,model="exp3P", summary=TRUE, eDigit=3, ePos="bottom",linecolor="red")  


version 1.0.2 of "basicTrendline" package, figure for exp3P:

 <img src="docs/images/exp3P2.png" width="490"/>
	
version 1.0.1 of "basicTrendline" package, figure for exp3P:

 <img src="docs/images/exp.png" width="490"/>

**[case 2:] plot and add trendline separately:** 


	plot(x,y,yaxt="n",xlab = "your own xaxis name (mg)", ylab = "ylab (‰)")
	axis(2,las=2)  # Change the y-axis text direction

	library(basicTrendline)
	#set plot=FALSE in the following codes
	trendline(x,y, plot=FALSE, model="power3P", summary=TRUE, eDigit=3, ePos="bottom",linecolor="black") 

<img src="docs/images/power.png" width="490"/>
	
**[case 3:] chanage other models, using the same function "trendline()"** 

	library(basicTrendline)

	# change model to "log2P"
	trendline(x,y, model="log2P", summary=TRUE, eDigit=3, ePos="bottom",linecolor="black") 

<img src="docs/images/log2P.png" width="490"/>

“model” can be one of c('lin2P','line3P','log2P','exp3P','power3P')
	
- "line2P"    # y=a\*x+b

- "line3P"    # y=a\*x^2+b\*x+c

- "log2P"     # y=a\*ln(x)+b

- "exp3P"     # y=a\*exp(b\*x)+c

- "power3P"   # y=a*x^b+c)



**[case 4:] draw different regression lines for the same dataset:**

	x1<-1:5
	y1<-c(2,14,18,19,20)

	plot(x1,y1,main="Different regression lines in one plot")
	
	library(basicTrendline)

	trendline(x1,y1,model="line2P",plot=FALSE,ePos="none",linecolor="red")
	trendline(x1,y1,model="log2P",plot=FALSE,ePos="none",linecolor="blue",lty=2)
	trendline(x1,y1,model="exp3P",plot=FALSE,ePos="none",linecolor="black",lty=3)

	legend("bottomright",c("line2P","log2P","exp3P"), lty=c(1,2,3),col=c("red","blue","black"))

<img src="docs/images/Multilines.png" width="490"/>


**[case 5:] draw trendlines by the same model (e.g. "exp3P") with different datasets:**

import some datasets:

	x1<- c(1,30,90,180,360)
	x2<- c(1,45,90,180,360)
	x3<- c(1,30,60,120,240)

	y1<-c(10,14,18,19,20)    
	y2<- c(8,11,13,15,17) 
	y3<-c(9,13,16,16,16)   

Plot (or points) and add trendlines:

	plot(x1,y1,,pch=1, xlim = c(0,400),ylim = c(6,22),main="Same regression lines with different datasets",xlab = "Time (days)", ylab = "your ylab (‰)")

	points(x2,y2,pch=2)  # different type for points
	points(x3,y3,pch=3)

	library(basicTrendline)

	# different linecolor and lty (lineType) for each trendline
	trendline(x1,y1,model="exp3P",linecolor="red",lty=1,plot=FALSE,ePos="none",summary = TRUE)->output1
	trendline(x2,y2,model="exp3P",linecolor="blue",lty = 2,plot=FALSE,ePos="none",summary = TRUE)->output2
	trendline(x3,y3,model="exp3P",linecolor="green",lty = 3,plot=FALSE,ePos="none",summary = TRUE)->output3
	
	# add legend
	legend("bottomright",c("x1y1","x2y2","x3y3"),pch=c(1,2,3), lty=c(1,2,3),col=c("red","blue","green"))

	## return the results of each trendline as follow:
	output1
	output2
	output3

<img src="docs/images/case5.png" width="490"/>


## Highlights

<font color=red>The "basicTrendline" package in R software could output **a better regression result (higher R<sup>2</sup> and lower p-value)** for 'power3P' model（y = ax^b +c） **than those in OriginPro** software.</font> Please see the example below:

>formula as y=a*x^b +c

x<- c(1,30,60,90,180,360)

y<- c(2,14,16,18,19,20)  # increase convex-function

>in OriginPro software:

c=-7344.578

a=7347.183

b=43224.4

<font color=red>**adjR<sup>2</sup>= 0.97129       # lower adjR<sup>2</sup> value**</font>

p-value of model=2.24891e-4

>in the 'basicTrendline' R package:

c=34.671

a=-32.703

b=-0.13999

<font color=red>**adjR<sup>2</sup>= 0.99346 >  0.97129   # higher (or better ) adjR<sup>2</sup> value**</font>

p-value of model= 2.44924-5 < 2.24891e-4

## Graphics

<img src="docs/images/line2P.png" width="490"/>
<img src="docs/images/line3P.png" width="490"/>
<img src="docs/images/log.png" width="490"/>
<img src="docs/images/log0.5.png" width="490"/>
<img src="docs/images/exp.png" width="490"/>
<img src="docs/images/power.png" width="490"/>


To see examples on how to use "basicTrendline" in R software, you can run the following R code if you have the "basicTrendline" package installed:

    library(basicTrendline)
    ?trendline()


## Contributions

R codes contributed by


- adding-regression-line-equation-and-r2-on-graph-1: http://blog.sciencenet.cn/blog-267448-1021594.html
- adding-regression-line-equation-and-r2-on-graph-2: https://stackoverflow.com/questions/7549694/adding-regression-line-equation-and-r2-on-graph
- What is non-linear regression?: https://datascienceplus.com/first-steps-with-non-linear-regression-in-r/
- adding regression line for nonlinear regression: http://blog.sciencenet.cn/blog-651374-1014133.html
- R codes for 'print.summary.nls of exp3P and power3P' cite from https://github.com/SurajGupta/r-source/blob/master/src/library/stats/R/nls.R
- and so on...

## Contact

- If you have any question or comment to this package, tell me at [here](http://meiweiping.cn/en/basicTrendline-an-R-package-for-adding-trendline-of-basic-regression-models-to-plot/).

- Bugs and feature requests can be filed to https://github.com/PhDMeiwp/basicTrendline/issues. BTW, [Pull requests](https://github.com/PhDMeiwp/basicTrendline/pulls) are also welcome.

## Appendix

The **PDF file** of this R package is available at https://cran.r-project.org/web/packages/basicTrendline/index.html 

>> 点击进入 [basicTrendline函数包中文介绍入口](http://meiweiping.cn/%E7%94%A8%E4%BA%8E%E5%B8%B8%E8%A7%84%E7%BA%BF%E6%80%A7%E9%9D%9E%E7%BA%BF%E6%80%A7%E6%8B%9F%E5%90%88%E7%9A%84R%E5%87%BD%E6%95%B0%E5%8C%85%EF%BC%88basicTrendline%EF%BC%89%E4%BB%8B%E7%BB%8D/)