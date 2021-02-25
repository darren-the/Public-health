# Life Expectancy - Regression Analysis
Having recently completed a machine learning course at school, I wanted to apply some of the techniques I learnt to my own project. The topic of public health and diseases have always interested me, so I decided to put my skills to the test using [life expectancy data](https://www.kaggle.com/kumarajarshi/life-expectancy-who) from kaggle.

## The Goals:
* Predict life expectancy of countries based off various factors such as GDP, schooling, infection rates etc
* Compare the accuracy of different models using metrics like R2 scores

##  Summary Statistics

|    | Country     |   Year | Status     |   Life expectancy |   Adult Mortality |   infant deaths |   Alcohol |   percentage expenditure |   Hepatitis B |   Measles |   BMI |   under-five deaths |   Polio |   Total expenditure |   Diphtheria |   HIV/AIDS |      GDP |       Population |   thinness 1-19 years |   thinness 5-9 years |   Income composition of resources |   Schooling |
|---:|:------------|-------:|:-----------|------------------:|------------------:|----------------:|----------:|-------------------------:|--------------:|----------:|------:|--------------------:|--------:|--------------------:|-------------:|-----------:|---------:|-----------------:|----------------------:|---------------------:|----------------------------------:|------------:|
|  0 | Afghanistan |   2015 | Developing |              65   |               263 |              62 |      0.01 |                 71.2796  |            65 |      1154 |  19.1 |                  83 |       6 |                8.16 |           65 |        0.1 | 584.259  |      3.37365e+07 |                  17.2 |                 17.3 |                             0.479 |        10.1 |
|  1 | Afghanistan |   2014 | Developing |              59.9 |               271 |              64 |      0.01 |                 73.5236  |            62 |       492 |  18.6 |                  86 |      58 |                8.18 |           62 |        0.1 | 612.697  | 327582           |                  17.5 |                 17.5 |                             0.476 |        10   |
|  2 | Afghanistan |   2013 | Developing |              59.9 |               268 |              66 |      0.01 |                 73.2192  |            64 |       430 |  18.1 |                  89 |      62 |                8.13 |           64 |        0.1 | 631.745  |      3.17317e+07 |                  17.7 |                 17.7 |                             0.47  |         9.9 |
|  3 | Afghanistan |   2012 | Developing |              59.5 |               272 |              69 |      0.01 |                 78.1842  |            67 |      2787 |  17.6 |                  93 |      67 |                8.52 |           67 |        0.1 | 669.959  |      3.69696e+06 |                  17.9 |                 18   |                             0.463 |         9.8 |
|  4 | Afghanistan |   2011 | Developing |              59.2 |               275 |              71 |      0.01 |                  7.09711 |            68 |      3013 |  17.2 |                  97 |      68 |                7.87 |           68 |        0.1 |  63.5372 |      2.9786e+06  |                  18.2 |                 18.2 |                             0.454 |         9.5 |

Our main variable of interest is 'Life expectancy', so here is an idea of how these values are distributed.

![histplot](https://user-images.githubusercontent.com/62131073/109147938-b7b9e300-77b9-11eb-8d70-4250fdb205e9.png)

Correlation heatmaps are also useful to see if there are any particularly strong correlations between pairs of variables.

![heatmap](https://user-images.githubusercontent.com/62131073/109148301-344cc180-77ba-11eb-85ab-31ac9f902d18.png)

Using the map, we can gauge the strength of certain correlations much more easily. It appears that some pairings have quite strong correlations, but thats definitely a result of having very similar definitions:
* Under five deaths vs infant deaths
* Adult mortality vs life expectancy
* Thinness vs BMI

On the other hand, it seems some of these have almost no correlation:
* BMI vs Hepatitis B
* Diphtheria vs Total expenditure

There are a few however, which aren't as intuitive but their correlations may actually be useful:
* Schooling vs life expectancy
* HIV/AIDS vs life expectancy

Below are four plots of some of these pairings, from these we can see that the top two plots have a much clearer correlation than the bottom two.

![scattersubplots](https://user-images.githubusercontent.com/62131073/109148619-9ad1df80-77ba-11eb-9810-933a9e48a513.png)

## Results
Here is a list of the regression models used:
* Linear Regression
* Ridge Regression
* Lasso Regression

We can compare how these models performed against each other by comparing their mean squared error and R2 scores.

|    | Model   |   Mean squared error |   R2 score |
|---:|:--------|---------------------:|-----------:|
|  0 | Linear  |              3.70192 |   0.95864  |
|  1 | Ridge   |              3.78034 |   0.957735 |
|  2 | Lasso   |              3.86608 |   0.956459 |

They all performed pretty well! Having an R2 score of ~0.95 gives our regression models a lot of validity.

## Improvements
If there is one thing to change, it would likely be the inclusion of the 'Country' variable. The name of countries alone have a large impact on the predicted life expectancy, possibly too much. There is likely not much practical use of a model that is mostly based off this. Below are some of the larger coefficients included in the model.


|     | Variable                         |   Coefficient |
|----:|:---------------------------------|--------------:|
|  22 | Country_Angola                   |      -16.45   |
|  49 | Country_Canada                   |       13.0033 |
|  50 | Country_Central African Republic |      -15.4159 |
|  51 | Country_Chad                     |      -14.2207 |
|  63 | Country_Côte d'Ivoire            |      -15.1723 |
|  78 | Country_Finland                  |       12.5063 |
|  79 | Country_France                   |       14.1176 |
|  85 | Country_Greece                   |       13.1851 |
| 100 | Country_Israel                   |       12.9033 |
| 156 | Country_Republic of Korea        |       12.2766 |
| 171 | Country_Sierra Leone             |      -20.4855 |
| 176 | Country_Somalia                  |      -12.9676 |