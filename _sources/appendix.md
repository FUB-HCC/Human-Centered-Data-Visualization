---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python
---
# Appendix

## Summary Statistics
Let's continue our discussion of exploratory data analysis. In the previous section, we saw ways to visualize attributes (variables) using graphs to begin understanding the properties of the data distribution, an essential and preliminary step in data analysis. In this section, we begin discussing statistical or numerical summaries of data to quantify properties we have observed using visual summaries and plots. Remember that one purpose of EDA is to identify problems in data and understand variable properties. We also want to use EDA to understand the relationship between pairs of variables, such as their correlation or covariance.

We differentiate measures of central tendency, i.e., measures of location that describe a tendency of data to center about certain numerical value. Here we have mode, median, and mean. Then we have measures of variability, i.e., dispersion that describe the spread of the data across possible values. To this group the range, interquartile range, variance, and standard deviation belong to. Finally we have measures of shape that relate to the form of the distribution, its skewness. 

<!-- https://bookdown.org/yih_huynh/Guide-to-R-Book/diamonds.html -->

In this chapter, we use the diamond data set, that contains the prices, carat, color and other attributes of almost 54,000 diamonds. 

```{code-cell} 
import altair as alt
import pandas as pd
#Library with datasets
import seaborn as sns 

# load dataset and show structure
diamonds = sns.load_dataset('diamonds', cache=True, data_home=None)

# show attributes 
diamonds.info()

```

```{code-cell} 
# count frequencies
diamonds['cut'].value_counts()
```

```{code-cell} 
# counts proportions
diamonds['cut'].value_counts(normalize=True)

```
<!-- Might be a better example: https://r4ds.had.co.nz/exploratory-data-analysis.html#patterns-and-models -->

Part of our goal is to understand how the variables are distributed in a given data set. Again, note that we are not using distribution in a formal mathematical (or probabilistic) sense. All the statements we make here are based on the data at hand, so we might call this an empirical distribution of data. Empirical is used here in the sense that it is data resulting from an experiment. Let's take a data set on the properties of diamonds as an example.

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Distribution of Depth in the Diamonds Data Set.
    name: dist_depth
---
# disable max rows (5000)
alt.data_transformers.disable_max_rows()

# dimensions of the data set
alt.Chart(diamonds).mark_bar().encode(
  x=alt.X('depth', bin=alt.Bin(maxbins=100)), # with Bin parameter maxbins the number of maxbins can be specified 
  y='count()'
).properties( 
    width=350,
    height=250
    )

```
## Central Tendency

Now that we know the area over which the data is distributed, we can figure out an initial summary of the data over that area. Let's start with the center of the data: 

The median is a statistic defined such that half of the data has a smaller value. We can use the notation `x(n/2)` (a rank statistic) to represent the median. 

Note that we can use an algorithm based on the quicksort partition scheme to compute the median in linear time (on average).

$\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_{i}$.

Where is the mean in our example dataset?

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Show Mean in Distribution of Depth in the Diamonds Data Set.
    name: median
---
# determine median

dimensions = alt.Chart(diamonds).mark_bar().encode(
  x=alt.X('depth', bin=alt.Bin(maxbins=100)),
  y='count()'
).properties( 
    width=350,
    height=250
    )

# create chart with median of depth
median = alt.Chart(diamonds).mark_rule(color='red').encode( #set color of mark_rule
  x=alt.X('median(depth)'),size=alt.value(2) # set size of line with size=alt.value()
).properties( 
    width=350,
    height=250
    )

# combine charts
dimensions + median
```
Now that we have a measure of the center, we can now discuss how the data is distributed around that center.

## Median, and IQR

Median is better measure of central tendency than the mean when we have outliers or/and skewed distribution, e.g., income, housing prices, waiting time. It is the middle observation when data is sorted in the order of magnitude. Thus (about) 50 % of observations are smaller and (about) 50 % are larger than the median. In our dataset:

```{code-cell} 
# min and max value
from tabulate import tabulate

# data structure to use for the table
table = [
    ["Min", "Max"], 
    [min(diamonds.depth), max(diamonds.depth)]
]
print(tabulate(table)) # use tabulate to create a table format

```

```{code-cell} 
# mean vs. median
import numpy as np
# data structure to use for the table
table_mean = [
    ["Mean", "Median"], 
    [np.round(diamonds['depth'].mean(), 1), diamonds['depth'].median()]
]
print(tabulate(table_mean)) 
```

For the mean, we have a convenient way to describe this: the average distance (using the squared difference) from the mean. We call this the variance of the data. vhe Variance is a commonly used statistic for dispersion, but it has the disadvantage that its units are not easily conceptualized (e.g., squared diamond depth).

$sd(x) = \frac{1}{n} \sum_{i-1}^n (x_i-\bar{x})^2$

A scatter statistic that is in the same units as the data is the standard deviation, which is just the square root of the variance:

$var(x) = \sqrt{\frac{1}{n} \sum_{i-1}^n (x_i-\bar{x})^2}$

We can also use standard deviations as an interpretable unit for how far a particular data point is from the mean. This is often use in tables. 

Just like we saw how the median is a rank statistic used to describe central tendency, we can also use rank statistics to describe spread. 
For this we use two more rank statistics: the first and third quartiles, x(n/4) and x(3n/4) respectively. We know this already, it is the interquartile range. Also called midspread and is the difference between third and first quartiles (spread in the middle 50%).
It is not affected by extreme values.
<!-- L: Find Python equivalent to R range() to get min and max values of the column -->

```{code-cell} 
# Range
print(f"{min(diamonds.depth)} to {max(diamonds.depth)}")
```

```{code-cell} 
# Variance
diamonds['depth'].var()
```

```{code-cell} 
#standard deviation
diamonds['depth'].std()
```

### Outliers

There is no precise way to define and identify outliers. Instead, a subject matter expert must interpret the raw observations and decide whether or not a value is an outlier. 

```{code-cell} 
# Determine outlier 

df = diamonds['depth']

q1 = df.quantile(0.25)
q2 = df.quantile(0.75)
# calculate IQR 
iqr = q2 - q1 

# detect outliers based on the formula above
outliers = df[((df < (q1 - 1.5 * iqr)) | (df > (q2 + 1.5 * iqr)))]
outliers

```

However, we can use estimates of dispersion to identify outlier values in a data set. If we make an estimate of dispersion based on the techniques we have just seen, we can identify values that are unusually far from the center of the distribution. Although this method works relatively well in practice, it presents a fundamental problem. Severe outliers can significantly affect standard deviation-based spread estimates. In particular, the spread estimates are inflated in the presence of severe outliers. To circumvent this problem, we use rank-based spread estimates to identify outliers as such:
$outliers_{sd}(x)= \{x_i||x_j|>\bar{x}+k \times sd(x)\}$

To mitigate the effect of severe outliers you can use rank-based estimates of spread to identify outliers as:

$\mbox{outliers}_{IQR}(x)= \{x_j|x_j < x_{(1/4)} - k \times IQR(x) \mbox{ or } x_j > x_{(3/4)} + k \times IQR(x) \}$

This is usually referred to as the Tukey outlier rule, where the multiplier k plays the same role as before. We use IQR here because it is less prone to inflating due to severe outliers in the data set. It also works better for skewed data than the standard deviation based method.



When does it make sense to remove outliers?
<!-- taken from https://statisticsbyjim.com/basics/remove-outliers/ -->

Well, it depends. As you can see in this visualization, removing outliers can distort your analyses by removing important information from the dataset. However, you have to make an informed decision what to do with them because removing outliers is legitimate only for specific reasons. Outliers can provide very interesting information about the subject-area and data collection process. It’s essential to understand how outliers occur and whether they might happen again as a normal part of the process or study area. You might be tempted to simply  remove outliers to decrease the variability in your data and therefore the increases statistical power, which makes your results to become statistically significant. These temptation might be a reason for the reproducibility crisis in psychology and other disciplines.
<!-- hypothesis! please check out -->

## Skewness

One final thought. Although there are formal ways to define this precisely, the five-number summary can be used to understand if data are biased. How? 

If one of these differences is larger than the other, then it suggests that this data set may be skewed, meaning that the range of data on one side of the median is longer (or shorter) than the range of data on the other side of the median. Do you think our diamond depth data set is biased?

```{code-cell} 
# Summary statistics
diamonds.depth.describe()
```

```{code-cell} 
# Skewness
diamonds.depth.skew()
```
The skewness of the data is negative, thus, we can conclude that the data are close to bell shape but slightly skewed to the left. 


For pairs of continuous variables, the most useful visualization is the scatter plot. This gives an idea of how a variable varies (in terms of central trend, variance and skewness) depending on another variable. A scatter plot can be used to show relationship between `price` and `carrat`.

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Scatterplot of Price Depending On Carat
    name: sp_price-carat
---
# Visualize Data - Scatterplot
alt.Chart(diamonds).mark_circle(size=60).encode(
  x='price', 
  y='carat'
).properties( 
    width=350,
    height=250
    )
```

As we expected, there seem to be a relationsship between price and carrat, which brings us to the next question. 

## Covariance and Correlation
<!-- https://bookdown.org/ronsarafian/IntrotoDS/eda.html#summary-statistics 
http://lipas.uwasa.fi/~sjp/Teaching/Bs/Lectures/BasicStatistics.html -->

As you have learned, the scatterplot is a visual method for observing relationships between pairs of variables. 

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Covariance and correlation.
    name: sp_covariance
---
# Covariance and correlation
# create a scatterplot with x = carat and y = price
sp = alt.Chart(diamonds).mark_circle(size=60).encode(
  x='carat', 
  y='price'
).properties( 
    width=350,
    height=250
    )

# create the mean of carat
mean_carat = alt.Chart(diamonds).mark_rule(color='blue', strokeDash=[8,8]).encode( #set color of mark_rule
  x=alt.X('mean(carat)'), size=alt.value(2) # set size of line with size=alt.value()
).properties( 
    width=350,
    height=250
    )


mean_price = alt.Chart(diamonds).mark_rule(color='blue', strokeDash=[8,8]).encode( #set color of mark_rule
  y=alt.Y('mean(price)'), size=alt.value(2) # set size of line with size=alt.value()
).properties( 
    width=350,
    height=250
    )


# combine the scatterplot with the mean lines of price and carat
sp + mean_carat + mean_price

```
However, how do we quantitatively summarize the relationship between two variables. We need to extend our notion of scatter (or variation of data around the mean) to the notion of covariation: do pairs of variables vary around the mean in the same way or more precisly, does x~i vary in the same direction and on the same scale away from its mean as y~i? 

This leads to covariance:
$cov(x,y) =\frac{1}{n}\sum_{i=1}^{n}(x_i - \bar{x})(y_i -\bar{y})$

Correlation (formally, Pearson’s correlation coefficient) summarizes the same relationship in a unit-less way:

$cor(x,y)=\frac{cov(x,y)}{sd(x)sd(y)}$ 

Correlation evaluates the direction as well as strength of a relationship between continuous variables. The correlation coefficient can range from -1 to +1, which signifies strong negative to strong positive relation between the variables. 

You can think of the correlation as the covariance between x and y after transforming each to the unitless scale of z-scores. Just to recall, a z-score of a sample x is defined as the mean-centered, scale normalized observations: $z_i(x)=\frac{x_i-\bar{x}}{sd(x)}$, thus $r(x,y)=cov(z(x),z(y))$. 

## Correlation Matrix
<!--https://rkabacoff.github.io/datavis/Models.html
https://www.displayr.com/what-is-a-correlation-matrix/ 
https://bookdown.org/ronsarafian/IntrotoDS/eda.html#summary-statistics-->

The covariance is a simple summary of association between two variables, but it certainly may not capture the whole “story” when dealing with more than two variables. The most common summary of multivariate relation, is the covariance matrix, but we warn that only the simplest multivariate relations are fully summarized by this matrix.

```{code-cell} 
# Correlation Matrix (less meaningful example - just a showcase)
# Print mcor and round to 2 digits

diamonds[['carat', 'depth', 'table', 'price']].corr().round(2)

# Load visualization from package
```

<!-- Source: https://github.com/altair-viz/altair/pull/1945 -->
```{code-cell} 
# Load visualization from package
corrMatrix = diamonds[['carat', 'depth', 'table', 'price']].corr().reset_index().melt('index')
corrMatrix.columns = ['var1', 'var2', 'corr']

chart = alt.Chart(corrMatrix).mark_rect().encode(
    x='var1',
    y='var2',
    color=alt.Color('corr'),
).properties(
    width=350,
    height=250
)

chart += chart.mark_text(size=25).encode(
    text=alt.Text('corr', format=".2f"),
    color=alt.condition(
        "datum.corr > 0.5",
        alt.value('white'),
        alt.value('black')
    )
)

chart
```