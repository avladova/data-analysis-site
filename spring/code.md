---
layout: page
title: R scripts \ Код — Весна
permalink: /spring/code/
---

[← Back \ Назад]({{ "/spring/" | relative_url }})

## Normality check \ Проверки нормальности

```r
#1
shapiro.test(X) # Тест Шапиро
# Pvalue<alfa=0.05 гипотезу о нормальности отвергаем

#2
library(ggpubr)
ggdensity(X, main = "Density plot of X", xlab = "X")
ggqqplot(X)

#3
library(nortest) # Библиотека для pearson.test и lillie.test
pearson.test(X$V1) # Пирсон
lillie.test(X$V1)

#4
library("sm") # Для sm.density
sm.density(X$V1, model = "Normal") # Попадаем в коридор?
```

[Basic Stats & dataset](https://disk.yandex.ru/i/3q16BxQkqM0y2A) · [Pearson Spearman Kendall Correlation](https://drive.google.com/file/d/1RaQ9Wu2HszEWwDWW4iNwrUXfc7lKKu7n/view?usp=sharing)

## Clean the data \ Очистка данных

```r
#MAC:
x <- as.numeric(read.delim(pipe("pbpaste"), header = F, sep = ","))
#PC:
x <- as.numeric(read.delim("clipboard", header = F, sep = ","))

#delete NAN and string values
y <- na.omit(x)
```

## Hypothesis Tests \ Проверка гипотез

**1. Mean test (normal dist., known variance)**
R: `z.test()` (from BSDA package) · Excel: `Z.TEST(array, μ₀, σ)`, Data Analysis: One-sample z-test

**2. Mean test (normal dist., unknown variance)**
R: `t.test(x, mu = μ₀)` · Excel: `T.TEST(array, μ₀, tails, type=1)`, Data Analysis: One-sample t-test

**3. Equality of two means (independent samples, known variances)**
R: `z.test(x, y, sigma.x=σ₁, sigma.y=σ₂)` · Excel: Two-sample z-test

**4. Equality of two means (independent samples, unknown but equal variances)**
R: `t.test(x, y, var.equal=TRUE)`
Example: `male<-c(26200, 24700, 28400, 21700); female<-c(22600, 23600, 29300, 22300); t.test(male, female, "greater", paired=TRUE)`
Excel: `T.TEST(array1, array2, tails, type=2)`, Data Analysis: Student's t-test (equal variances)

**5. Equality of two means (independent samples, unknown & unequal variances)**
R: `t.test(x, y, var.equal=FALSE)`
Example: Test H0: E(X)=E(Y) without assuming equal variances at α=0.02 against H1: E(X)>E(Y):
`t.test(X, Y, alternative="greater", var.equal=FALSE, conf.level=0.98)`
Excel: `T.TEST(array1, array2, tails, type=3)`, Data Analysis: Welch's t-test (unequal variances)

**6. Equality of means (paired data)**
R: `t.test(x, y, paired=TRUE)` · Excel: `T.TEST(array1, array2, tails, type=1)`, Data Analysis: Paired t-test

**7. Equality of variances (two samples)**
R: `var.test(x, y)`
Example: Test H0: Var(X)=Var(Y) at α=0.05 against H1: Var(X)≠Var(Y): `var.test(x, y, alternative='two.sided')`
Excel: `F.TEST(array1, array2)`, Data Analysis: F-test (Fisher's test)

**8. Equality of proportions**
R: `prop.test(c(x_succ, y_succ), c(n₁, n₂), correct = FALSE)`
Example: `test<-prop.test(c(191,145), c(381,166), alternative = "two.sided", correct = FALSE); -sqrt(test$statistic)` — Z-statistic negative because prop1 < prop2 (191/381 < 145/166)

**9. Significance of correlation**
R: `cor.test(x, y, method="pearson")`
Example: Test H0: ρ=0 against H1: ρ≠0: `cor.test(x, y, alternative = "two.sided")`
Excel: `PEARSON(array1, array2)` + T.DIST for p-value, Data Analysis: Pearson correlation test

## Pareto optimum \ Оптимум по Парето

```r
library(rPref)
df <- data.frame(Object= c("A", "B", "C", "D", "E"),
  Tech = c(5, 6, 3, 6, 4), Art = c(6, 1, 5, 5, 3))
pref <- high(Tech) * high(Art)
front <- psel(df, pref)
plot(df$Tech, df$Art,
  type = "n", xlab = "Technique", ylab = "Artistry",
  main = "Pareto-front", xlim = c(0, 7), ylim = c(0, 7))
points(front$Tech, front$Art, col = "red", pch = 19, cex = 1.5)
others <- df[!df$Object %in% front$Object, ]
points(others$Tech, others$Art, col = "gray", pch = 1, cex = 1.5)
text(df$Tech, df$Art, labels = df$Object, pos = 4, cex = 0.9)
```

## CI for E(x) \ Интервал для матожидания

```r
install.packages("BSDA")
library(BSDA)
data<-c(18.2, 13.7, 15.9, 17.4, 21.8, 16.6, 12.3, 18.8, 16.2)
z.test(x = data,
  sigma.x = 3.8, # стандартное отклонение
  mu = 2.90, # выборочное среднее
  conf.level = 0.9,
  alternative = "two.sided")
```

```r
install.packages("confintr")
library(confintr)
data <- rnorm(25, mean = 2.9, sd = 0.45)
ci_mean(data, type = "bootstrap")
```

## CI for Var(x) \ Интервал для дисперсии

```r
install.packages("DescTools")
library(DescTools)
data <- rnorm(25, mean = 2.9, sd = 0.45)
VarTest(data, conf.level = 0.95)

install.packages("TeachingDemos")
library(TeachingDemos)
sigma.test(x, conf.level = 0.95)
```
