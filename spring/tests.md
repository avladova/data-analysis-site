---
layout: page
title: Tests \ Тесты — Весна
permalink: /spring/tests/
---

[← Back \ Назад]({{ "/spring/" | relative_url }})

> On the old site this block was mislabeled "Autumn term" though the content is statistics (spring semester). Moved here by meaning \ На старом сайте этот блок был ошибочно подписан «Autumn term», хотя по содержанию — статистика. Перенесено сюда по смыслу.

## Statistics \ Статистика

1. In order to estimate the average intelligence quotient (IQ) of the students of a large university, the mean IQ of a number of randomly chosen students is calculated. Using the central limit theorem, under the assumption that the distribution of the mean IQ is close to a normal one, estimate the minimal number of chosen students needed to obtain a result differing from the real average IQ by not more than 1 with a probability not less than 0.95, if it is known from previous studies that the standard deviation of IQ doesn't exceed 10.

2. For a sample of size 180 drawn from a normal population the unbiased point estimate of the population variance 0.5768 is found. Find a confidence interval (CI) for the population variance at confidence level 0.97.

3. A data set is given (176 values). Under the assumption that this data set is a sample drawn from a normal population compute a confidence interval (CI) for the population mean at confidence level 0.97.

4. Using Excel and/or R(RStudio), clear a given data set out of non-numeric values and omissions and compute the following statistical characteristics of the sample: size of the sample, interquartile range, sample standard deviation, lower boundary of normal range, total number of outlying cases. In addition clear the sample out of outlying cases and compute: size of the cleared sample, 0.84-quantile, kurtosis (unbiased estimate).

5. For a sample of size = 42 sample moments are calculated: expected value = 0.82, variance = 3.32. Using the method of moments find estimates of the parameters of a normal distribution.

Русскоязычный дубль (как на исходном сайте):

1. Используя Excel и/или R(RStudio), проведите очистку набора от нечисловых значений и пропусков и вычислите статистические характеристики очищенной выборки: количество нечисловых значений и пропусков в исходной выборке, медиана, стандартное отклонение (несмещенное), нижняя граница нормы, верхняя граница нормы.

2. Дополнительно очистите выборку от выбросов и вычислите следующие статистические характеристики выборки, очищенной от нечисловых значений, пропусков и выбросов: объем выборки, очищенной от нечисловых значений, пропусков и выбросов, квантиль уровня 0.62, эксцесс (несмещенная оценка).

3. Методом моментов найдите оценки параметров равномерного распределения. Для однопараметрических распределений используйте первый начальный момент ν1. Для двухпараметрических распределений дополнительно используйте второй центральный момент μ2.

4. По извлеченной из нормальной генеральной совокупности случайной выборке объёма 152 найдена точечная несмещенная оценка дисперсии 1.3889. Постройте доверительный интервал (ДИ) для дисперсии на уровне доверия 0.96.

5. Для оценки средней суммы чека в заведении общепита вычисляют среднее арифметическое некоторого количества случайно выбранных чеков. Используя центральную предельную теорему, оцените минимальное количество выбранных чеков, необходимое для того, чтобы с вероятностью не менее 0.9 полученное значение отличалось от истинной средней суммы чека не более чем на 50 руб., если среднеквадратичное отклонение суммы чека не превышает 200 руб.

To read the sequences, please try to use `scan("clipboard", what = character())` or `scan("clipboard", what = numeric())` or read from Excel file with library(readxl) `read_excel("path")`.

## End Semester Test 2 \ Контрольная работа № 2

1. Test the null hypothesis H0: Var(X)=Var(Y) at significance level α=0.06 against the alternative H1: Var(X)≠Var(Y), computing the P-value. *(даны две выборки X, Y по ~180 значений)*

2. Using Excel or R(RStudio), clear the sample out of omissions, denoted as "NA". After that test the hypothesis about discrete uniform distribution of respondents' answers at significance level 0.09, applying goodness-of-fit (Pearson's chi-squared) test.

3. A two-dimensional sample (X,Y) is given. Delete all rows, in which at least one value is missing (omissions are denoted by "NA"). Test the hypothesis about insignificance of correlation coefficient ρ (i.e. H0: ρ=0 against the alternative H1: ρ≠0). To complete the task please check additional presentation at the page Statistics.

4. Two samples are drawn from two normal populations X and Y. Test the null hypothesis H0: E(X)=E(Y) (without the assumption of equality of variances) at significance level α=0.09 against the alternative H1: E(X)≠E(Y), computing the P-value.

5. According to the results of a sociological study, respondents' answers to a survey questions are represented as a sample. Using Excel or R(RStudio), clear the sample out of omissions, denoted as "NA", and answer: number of different variants of respondents' answers occurring in the cleared sample; number of respondents who gave answer "Post-Graduate"; the proportion of respondents who gave answer "Post-Graduate"; the boundaries of a 0.92-confidence interval for the population proportion of answers "Post-Graduate".

---

## Problems with the final stat test \ Замеченные проблемы с экзаменом по статистике

Test lasts 60 minutes. To enter Windows use login: studmoodle and password: moodle38. To enter [campus.fa.ru](https://campus.fa.ru/) use your regular login and password. Open RStudio and Excel before you start the test. Name your file as "GROUP_LastName_FirstName". You are given 60 minutes for the test. You can check your results with the Check button. Going back is not allowed.
