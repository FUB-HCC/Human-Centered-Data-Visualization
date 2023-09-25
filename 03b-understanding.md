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

### Summary Statistics
Let's continue our discussion of exploratory data analysis. In the previous section, we saw ways to visualize attributes (variables) using graphs to begin understanding the properties of the data distribution, an essential and preliminary step in data analysis. In this section, we begin discussing statistical or numerical summaries of data to quantify properties we have observed using visual summaries and plots. Remember that one purpose of EDA is to identify problems in data and understand variable properties. We also want to use EDA to understand the relationship between pairs of variables, such as their correlation or covariance.

We differentiate measures of central tendency, i.e., measures of location that describe a tendency of data to center about certain numerical value. Here we have mode, median, and mean. Then we have measures of variability, i.e., dispersion that describe the spread of the data across possible values. To this group the range, interquartile range, variance, and standard deviation belong to. Finally we have measures of shape that relate to the form of the distribution, its skewness. 

<!-- https://bookdown.org/yih_huynh/Guide-to-R-Book/diamonds.html -->

In this chapter, we use the diamond data set, that contains the prices, carat, color and other attributes of almost 54,000 diamonds. 

```{code-cell} 
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
### Central Tendency

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

### Median, and IQR

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
# mean vs. median

```

```{code-cell} 
# mean vs. median

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

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Distribution of Depth in the Diamonds Data Set after removing outliers.
    name: outlier-filter
---
# Outliers (based on IQR)

# filter out the outliers and create a diamonds subset with the remaining rows
filter = (df >= q1 - 1.5 * iqr) & (df <= q2 + 1.5 * iqr)
diamonds_subset = diamonds.loc[filter]

# dimensions of the data set after filtering out outliers 
alt.Chart(diamonds_subset).mark_bar().encode(
  x=alt.X('depth', bin=alt.Bin(maxbins=100)), 
  y='count()'
).properties( 
    width=350,
    height=250
    )

```

When does it make sense to remove outliers?
<!-- taken from https://statisticsbyjim.com/basics/remove-outliers/ -->

Well, it depends. As you can see in this visualization, removing outliers can distort your analyses by removing important information from the dataset. However, you have to make an informed decision what to do with them because removing outliers is legitimate only for specific reasons. Outliers can provide very interesting information about the subject-area and data collection process. It’s essential to understand how outliers occur and whether they might happen again as a normal part of the process or study area. You might be tempted to simply  remove outliers to decrease the variability in your data and therefore the increases statistical power, which makes your results to become statistically significant. These temptation might be a reason for the reproducibility crisis in psychology and other disciplines.
<!-- hypothesis! please check out -->

### Skewness

One final thought. Although there are formal ways to define this precisely, the five-number summary can be used to understand if data are biased. How? 

If one of these differences is larger than the other, then it suggests that this data set may be skewed, meaning that the range of data on one side of the median is longer (or shorter) than the range of data on the other side of the median. Do you think our diamond depth data set is biased?

```{code-cell} 
# Summary statistics

# Skewness

```
The skewness of the data is negative, thus, we can conclude that the data are close to bell shape but slightly skewed to the left. 


For pairs of continuous variables, the most useful visualization is the scatter plot. This gives an idea of how a variable varies (in terms of central trend, variance and skewness) depending on another variable. A scatter plot can be used to show relationship between `price` and `carrat`.

```{code-cell} 
# Visualize Data - Scatterplot

```

As we expected, there seem to be a relationsship between price and carrat, which brings us to the next question. 

### Covariance and Correlation
<!-- https://bookdown.org/ronsarafian/IntrotoDS/eda.html#summary-statistics 
http://lipas.uwasa.fi/~sjp/Teaching/Bs/Lectures/BasicStatistics.html -->

As you have learned, the scatterplot is a visual method for observing relationships between pairs of variables. 

```{code-cell} 
# Covariance and correlation

```
However, how do we quantitatively summarize the relationship between two variables. We need to extend our notion of scatter (or variation of data around the mean) to the notion of covariation: do pairs of variables vary around the mean in the same way or more precisly, does x~i vary in the same direction and on the same scale away from its mean as y~i? 

This leads to covariance:
$cov(x,y) =\frac{1}{n}\sum_{i=1}^{n}(x_i - \bar{x})(y_i -\bar{y})$

Correlation (formally, Pearson’s correlation coefficient) summarizes the same relationship in a unit-less way:

$cor(x,y)=\frac{cov(x,y)}{sd(x)sd(y)}$ 

Correlation evaluates the direction as well as strength of a relationship between continuous variables. The correlation coefficient can range from -1 to +1, which signifies strong negative to strong positive relation between the variables. 

You can think of the correlation as the covariance between x and y after transforming each to the unitless scale of z-scores. Just to recall, a z-score of a sample x is defined as the mean-centered, scale normalized observations: $z_i(x)=\frac{x_i-\bar{x}}{sd(x)}$, thus $r(x,y)=cov(z(x),z(y))$. 

### Correlation Matrix
<!--https://rkabacoff.github.io/datavis/Models.html
https://www.displayr.com/what-is-a-correlation-matrix/ 
https://bookdown.org/ronsarafian/IntrotoDS/eda.html#summary-statistics-->

The covariance is a simple summary of association between two variables, but it certainly may not capture the whole “story” when dealing with more than two variables. The most common summary of multivariate relation, is the covariance matrix, but we warn that only the simplest multivariate relations are fully summarized by this matrix.

```{code-cell} 
# Correlation Matrix (less meaningful example - just a showcase)

# Print mcor and round to 2 digits

# Load visualization from package
```

## General Guidelines for EDA



It is difficult to say, what the best process is in EDA. I just provided a number of analyses and possible visualizations. You find many alternative suggestions, and I provide one of them:

* Begin with a discussion of the “center” of the data, generally based on mean.
* Describes how data are distributed. 
* Follow with a discussion of variability (and of skew if appropriate).
* End with a summary evaluation which may have a subjective component (numbers must be interpreted, they don’t speak for themselves).
* Make sure to use numbers in a description wisely – not too few or too many.

However, each dataset is very special, thus, as often it stays to be an individualized process. Therefore, reproducibility is very important during EDA. Computational notebooks such as R Markdown (used here), but also Jupyter notebooks (used in our exercise), Observable (google product) support readability and understandability of your exploration process. This supports [Knuth’s vision of literate programming](https://en.wikipedia.org/wiki/Literate_programming).

## Tools and Libraries for Data Exploration

Besides GNY R there are many tools and libraries that support the process of data exploration. In this section, I provide a selection. 

<!-- create table with tools -->

Wrangler provides data-transformation scripts within a visual, direct manipulation interface augmented by predictive models {cite}`kandel2011wrangler`. Wrangler is an interactive system for creating data transformations. It uses semantic data types, such as geographic locations, dates, classification  codes to support the validation of data and the type conversion. Interactive histories support review, refinement, and annotation of transformation scripts. The researchers provide a WebApp but also a [commercial product](https://www.trifacta.com/start-wrangling/). 

A similar approach is realized by [Open Refine](https://openrefine.org/). This tool was formerly developed by Google but it is now maintained by the open source community. It allows you to clean data, transform it from one format into another, or extend you data by additional data from an API. 

Besides DataWrangler, I would like to mention the tool Voyager {cite}`wongsuphasawat2015voyager`. The Voyager system is specifically suitable for exploratory visual analysis. You can again test it via a [WebApp](https://vega.github.io/voyager/) and the source code is available on [Github](https://github.com/vega/voyager). And for the sake of completeness, there is also a commercial software [Tableau](https://www.tableau.com/), which can be freely used in the educational context.

Both, Data Wrangler and Voyager are using a formal language - the Vega-Lite visualization grammar. Vega-Lite is a high-level grammar of interactive graphics that provides a concise, declarative JSON syntax to create diagrams for data analysis and presentation. Vega-Lite specifications describe visualizations as ``encoding mappings'' from data to properties of graphical marks (e.g., points or bars). 

The Vega-Lite compiler automatically produces visualization components including axes, legends, and scales. Vega-Lite supports both data transformations (e.g., aggregation, binning, filtering, sorting) and visual transformations (e.g., stacking and faceting). Moreover, Vega-Lite specifications can be composed into layered and multi-view displays, and made interactive with selections as you can see in the example. 

Vega-Lite is being used in another interesting library. On top of the Vega-Lite JSON specification a simple API was built: Altair. It is a declarative statistical visualization library for Python. [Source code](https://github.com/altair-viz/altair) and a comprehensive [documentation](https://altair-viz.github.io/) <!--as well as [Tutorial Notebooks](github.com/altair-viz/altair_notebooks)--> are available on Github.







<!--  In der Wahrscheinlichkeitstheorie betrachten wir einen zugrundeliegenden Prozess, der eine gewisse Zufälligkeit oder Unsicherheit aufweist, die durch Zufallsvariablen modelliert wird, und wir finden heraus, was passiert. 

In der Statistik beobachten wir etwas, das passiert ist, und versuchen herauszufinden, welcher zugrunde liegende Prozess diese Beobachtungen erklären würde.

Statistik ist eng mit der Wahrscheinlichkeitstheorie verbunden. Mit Hilfe der Statistik können Sie die Wahrscheinlichkeit, die Chance, dass ein bestimmtes Ereignis eintritt, ausrechnen: Wenn Sie wissen wollen, wie hoch die Wahrscheinlichkeit ist, dass Ihr Ferienflugzeug abstürzt, denken Sie daran, wie viele Flugzeuge in der Regel innerhalb eines Jahres abstürzen. Da diese Zahl sehr klein ist, folgern Sie, dass die Wahrscheinlichkeit, dass Ihr Flugzeug abstürzt, ebenfalls gering ist. Sie haben eine sehr einfache statistische Analyse der Daten über Flugzeugabstürze durchgeführt und daraus eine Wahrscheinlichkeit berechnet.

Aber die Dinge funktionieren auch umgekehrt: Sie können abstrakte Wahrscheinlichkeiten verwenden, um Ihnen bei Ihren Statistiken zu helfen. Sagen Sie zum Beispiel, Sie wollen testen, ob ein Würfel, der in einem Casino verwendet wird, fair ist. Dazu werfen Sie den Würfel sehr oft und zeichnen die Ergebnisse auf. Dann argumentieren Sie wie folgt: Wenn der Würfel fair ist, dann sollte jede Zahl gleich wahrscheinlich sein. Es gibt sechs Zahlen, also sollte jede Zahl in 1/6 der Fälle auftauchen. Sie vergleichen den tatsächlichen Würfel mit einem idealen Würfel: Wenn Ihr Casinowürfel Ihnen in etwa 1/6 aller Würfe jede Zahl liefert, entscheiden Sie, dass es fair ist.

Die Wahrscheinlichkeitstheorie ist wichtig, wenn es um die Auswertung von Statistiken geht. Wenn Sie in einer Meinungsumfrage feststellen, dass 80% der Befragten den derzeitigen Premierminister mögen, ist die Versuchung groß, daraus zu schließen, dass der Premierminister sehr beliebt ist. Aber woher wissen Sie, dass Ihr Ergebnis nicht nur zufällig zustande gekommen ist? Nun, Sie verwenden die Wahrscheinlichkeitstheorie, um die Wahrscheinlichkeit zu berechnen, dass Ihr Ergebnis zufällig zustande gekommen ist - wenn diese Wahrscheinlichkeit sehr gering ist, dann sollten Sie zu dem Schluss kommen, dass der Premierminister sehr beliebt ist.

Statistics is the branch of mathematics that transforms data into useful information for decision makers

Statistics is the art of understanding and learning from data

Involves
Collecting data
Presenting and describing data
Analyzing and interpreting data

Data are facts that we consider worth collecting, summarizing, analyzing, and interpreting

Data sets are data collected for a particular study or analysis

Unit of analysis is a person, thing, transaction, or event that can be separately and uniquely identified and about which we want to collect data
Person (student, customer, programmer, ...)
Thing (education, power plant, ...)
Transaction (sale, cost of a software license, monthly rent, ...)
Event (application, election)

Variable is a characteristic, an attribute, or an occurrence observed for each unit of analysis

Examples
Unit of analysis: a computer science student
Variables: gender, age, studentID

-->

[^2]: I highly recommend reading more about him, for example, in [](https://www.stat.berkeley.edu/~brill/Papers/life.pdf).
[^3]: The so-called "smooth part of a data set" is the variability that the analyst has accounted for so far, while the "rough" part is the variability that remains unexplained.
[^4]: A dataframe is a list, with each component of that list being a equal length vector. Thus, intuitively, a dataframe is like a matrix with a rows-and-comlumns-structure. However, it differs from a matrix, since each column can having different mode (data type) {cite}`Matloff2011ArtofRProgramming`.
