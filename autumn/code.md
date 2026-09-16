---
layout: page
title: R code & Excel functions \ Код — Осень
permalink: /autumn/code/
---

[← Back \ Назад]({{ "/autumn/" | relative_url }})

Discrete and continuous distributions with R code and files of solutions \ Дискретные и непрерывные распределения с кодом на R и файлами решений на R и Excel.

## Basic discrete distributions \ Базовые дискретные распределения

### Bayes classifier \ Классификатор Байеса

```r
library(e1071)
data(Titanic)
m <- naiveBayes(Survived ~ .,
             data = Titanic)
predict(m, as.data.frame(Titanic))
```

### Empirical distribution \ Эмпирические законы распределения

```r
x<-pbinom(1:7, size=20,1/2)
n <- length(x)
x <- sort(x); vals <- unique(x)
rval <- approxfun(vals,
  cumsum(tabulate(match(x, vals)))/n,
  method = "constant", yleft = 0, yright = 1,
  f = 0, ties = "ordered")
plot(rval,ylab='F(x)')
```

## Basic continuous distributions \ Базовые непрерывные распределения

### Integrate if pdf is known distribution

```r
integrand <-function(x){dunif(x, min = 0, max = 3)}
integrate(integrand, lower = 2, upper = 3)
integrate(integrand, lower = 0, upper = 1)
```

### Дискретные случайные величины

```r
#Равномерное распределение - кубик
s<-1:6
p<-c(1/6,1/6,1/6,1/6,1/6,1/6)
sum(p) #проверка
plot(s,p,col="red",type="h")
Ms=sum(s*p)
Ds=sum(s^2*p)-Ms^2 #1 формула
DDs=sum((s-Ms)^2*p) #2 формула
```

### Uniform distribution pdf&cdf \ Плотность и кумулята равномерного закона

```r
curve(dunif(x, min = 1, max = 2), from = -1, to = 3,
  xlab='x', ylab='f(x)', main='PDF for Unif(1,2)')
curve(punif(x, min = 1, max = 2), from = -1, to = 3,
  xlab='x', ylab='F(x)', main='CDF for Unif(1,2)')
```

### Distribution functions \ Функции распределения

```r
library(mosaic)
plotDist('norm', mean=1, sd=1, col="red",kind="density", under=TRUE)
plotDist('norm', kind='cdf')
plotDist('exp', kind='histogram')
plotDist('binom', 25, .25)
```

### Standardizing to standard normal \ Приведение к стандартному нормальному распределению

```r
library(mosaic)
plotDist("norm")
integrand <- function(x) {dnorm(x, mean=0, sd=1)}
integrate(integrand, lower =(52.5-45)/sqrt(18), upper = Inf)
```

### Correlation matrix \ Корреляционная матрица

```r
library(corrplot)
cormat<-cor(as.matrix(dataset_name))
corrplot(cormat, method = 'number', order='FPC')

# or / или
library(corrgram)
corrgram(dataset_name, font.labels=6,
  lower.panel=panel.ellipse, upper.panel=panel.cor, diag.panel=panel.density)
```

### Non-linear relationship \ Нелинейная связь

```r
library(devtools); devtools::install_github("r-lib/remotes")
install_github("ProcessMiner/nlcor", force=TRUE); library(nlcor)
a<-c(1,2,3,4,5,6,7,8,9,10,11,12,13); b<-c(1,1,2,3,4,5,7,5,4,3,2,1,1)
plot(a,b, lwd = 10)
cor(a,b); ab <- nlcor(a, b, plt = T); ab$cor.estimate
print(ab$cor.plot)
```

### Portfolio of 2 stocks \ Портфель двух активов

```r
risk <- function(x1,x2,s1=0.05,s2=0.14,ro=0.36)
  {(s1^2*x1^2+s2^2*x2^2+2*ro*s1*s2*x1*x2)}
gb_risk<- function(x) risk(x[1],x[2])
constraint.mat<-rbind(c(-1,-1), # matrix of constraint coefficients
  c(1,0), c(0,1), c(0.16,0.23))
b<-c(-1,0,0,0.1)
constrOptim(c(0.4,0.4),gb_risk,NULL,constraint.mat,b)
```

### Basic Statistic Functions \ Основные статистики

```r
a<-1:30
summary(a) #stats at a glance
mean(a)
median(a)
var(a) #variance
sd(a) #standard deviation
min(a); max(a)
quantile(a)
IQR(a) #an interquartile range
boxplot(a) #the box and whiskers plot
```

### Combinatorial Formulas \ Комбинаторика

```r
# computing the number of combinations
n=16
k=14
C1=factorial(n)/(factorial(k)*factorial(n-k))
#or
C2=choose(n,k)
#Excel: ФАКТР(n)/ФАКТР(k)*ФАКТР(n-k)

#permutations
library(combinat)
permn(x=c("A","B","C"))
permn(x=2:5)
```

### Symbolic calculus \ Символьные вычисления

```r
library(rSymPy) #old version
.jinit()
sympy("var('x')"); sympy("var('y')"); sympy("var('C')")
sympy("integrate(0.5*x + C*y,(y,0,2),(x,0,1))")

library(Ryacas) #new version
f3y <- ysym("0.75*(2-2*x^2)")
integrate(f3y, "x")
```

### Exponential distribution pdf&cdf \ Плотность и кумулята экспоненциального закона

```r
x<-0:10
rate=5 #rate = lambda = 1/E(x)
plot(x,dexp(x,rate),type='l')
plot(x,pexp(x,rate),type='l')
```

### Double integral \ Двойной интеграл

```r
library(rSymPy)
.jinit()
sympy("var('x')"); sympy("var('y')"); sympy("var('C')")
sympy("integrate(0.5*x + C*y,(y,0,2),(x,0,1))")
```

## Distribution reference (R & Excel) \ Справочник по распределениям

| Distribution | R | Excel |
|---|---|---|
| **Bernoulli** — single trial, success/failure. Ex: coin flip | pmf: `dbinom(x, size=1, prob)` cmf: `pbinom(q, size=1, prob)` | `Binom.Dist(number_success, 1, prob, 0/1)` |
| **Binomial** — successes in n trials. Ex: heads in coin flips | pmf: `dbinom(x, size, prob)` cmf: `pbinom(q, size, prob)` | `Binom.Dist(...)`, `Binom.Inv(trials, probability_s, alpha)` |
| **Geometric** — failures before first success | pmf: `dgeom(x, prob)` cmf: `pgeom(x, prob)` | — |
| **Hypergeometric** — selection without replacement. Ex: lotto | pmf: `dhyper(x, m, n, k)` cmf: `phyper(q, m, n, k)` | `HYPGEOM.DIST(...)` |
| **Uniform** — equally likely over interval. Ex: train waiting time | pdf: `dunif(x, min, max)` | — |
| **Exponential** — time until event | pdf: `dexp(x, rate)` cdf: `pexp(x, rate)` | — |
| **Normal** — central tendency. Ex: height, weight | pdf: `dnorm(x, mean, sd)` cdf: `pnorm(p, mean, sd)` | `Norm.Dist(x, mean, sd, cumulative)`, `Norm.Inv(p, mean, sd)` |
| **Log-Normal** — Ex: income, stock prices | `dlnorm(x, mean, sd)` | — |
| **Student's t** — small samples/unknown variance | pdf: `dt(x, mean, sd)` cdf: `pt(prob, mean, sd)` | `T.DIST(...)`, `T.INV(...)` |
| **Negative Binomial** — failures until r successes | pmf: `dnbinom(x, size, prob)` | `NEGBINOM.DIST(...)` |
| **Poisson** — events per time period. Ex: calls per hour | pmf: `dpois(x, lambda)` | `POISSON.DIST(...)` |
| **Pareto** — rare impactful events. Ex: wealth, disasters | `library(actuar)`; `dpareto(x, shape, scale)` | — |

- Биномиальная случайная величина определяет вероятность m успехов в n испытаниях (выборка с возвращением).
- Гипергеометрическое распределение — выборка без возвращения.
- Геометрическая случайная величина — вероятность m испытаний до первого успеха; дискретный вариант экспоненциального распределения.
- Отрицательное биномиальное распределение — обобщение геометрического: k неудач до r успехов.

## How to solve \ Файлы решений

- [Dice & Events space](https://drive.google.com/file/d/1GmxWIH0jtpjgTBhjR91GssE_QbpEaN36/view?usp=sharing)
- [Factorial, Permutation, Combination in Excel](https://drive.google.com/file/d/1Rbc4EdfCFersiujDqkcavzNO7AlOMw-O/view?usp=sharing)
- [Workshop 7 Mean & Variance](https://drive.google.com/file/d/13Y1ajWEPk7IgXl1-CoVpojqfF6HXCjaL/view?usp=sharing)
- [Workshop 8 pdf & cdf](https://drive.google.com/file/d/1xk7ZcZVrNWv658PuXy16OD46ku-PNjl6/view?usp=sharing)
- [Workshop 9 Bernoulli & Binomial](https://drive.google.com/file/d/1_NvYbaqXLJ8JZ6wH6kxiEwwAgpj1dyej/view?usp=sharing)
- [Test 1 IFF19-1](https://drive.google.com/file/d/1mB-nUhYhqTmP0fnRz87AwMN8Nxv4HvTD/view?usp=sharing)
- [Midterm 1 — an example](https://drive.google.com/drive/folders/1QpkCKazLReFkb1eP1ptubb4Kyb-MJUot?usp=sharing)
- [Workshop 10 Geom & Poisson](https://drive.google.com/file/d/1FgJbD9fR4XQgGaOU_tjeBpvtZiTJ44Wa/view?usp=sharing)

*Shared by Владислав Бычков МБНиА24-1*
