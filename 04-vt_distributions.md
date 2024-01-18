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
# Visualization Techniques: Distributions

## General Guidelines for EDA
<!-- LW: Maybe transfer this part under "Understanding the Data Structure?-->

It is difficult to say, what the best process is in Exploratory Data Analysis (EDA). I just provided a number of analyses and possible visualizations. You find many alternative suggestions, and I provide one of them:

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


(Understanding-the-Data-Structure)=
## Understanding the Data Structure 

<!-- Useful Ressources:
https://bookdown.org/ronsarafian/IntrotoDS/eda.html#summary-statistics
https://www.hcbravo.org/IntroDataSci/bookdown-notes/exploratory-data-analysis-summary-statistics.html
https://bookdown.org/BaktiSiregar/data-science-for-beginners/EDA.html
https://biosakshat.github.io/data-visualization.html
https://www.wekaleamstudios.co.uk/exploratory-data-analysis/
https://bolt.mph.ufl.edu/6050-6052/unit-1/
https://www.epa.gov/caddis-vol4/exploratory-data-analysis
https://medium.com/swlh/effective-visualization-of-multi-dimensional-data-a-hands-on-approach-b48f36a56ee8
-->

<!--NEXT TERM: CHANGE THE ORDERING: mean, distribution, variability - ask for both datasets questions, check if for the first part the second data set is more appropriate, and the other way around (or leave out outlier of the flight dataset) -->

In this section, we focus on understanding the structure of our data by employing Exploratory Data Analysis (EDA). EDA is an approach to analyzing data sets to summarize their main characteristics by using data visualizations. In 1970 John Tukey {cite}`Tukey1977eda` introduced EDA with this seminal book on this topic. He was an extraordinary <!-- KG name disciplinary background instead of appraisal--> scientist who had a profound impact on statistics and computer science[^2]. Much of what we cover in EDA today is based on his work. Part of EDA is the so-called initial data analysis (IDA) [](https://towardsdatascience.com/a-basic-guide-to-initial-and-exploratory-data-analysis-6d2577dfc242). IDA focuses on identifying data inconsistencies (e.g., missing values) and the description of the data properties; thus, EDA encompasses IDA. 

Explorative Data Analysis allows the data analysts to achieve a richer qualitative understanding by ''looking at data to see what it seems to say'' <!-- KG: source? -->. EDA should be understood as an iterative process that supports the following:
* the search for answers by visualizing, transforming, and modeling your data,
* the generation of hypotheses about what might be happening in a data set, and
* the refining of your analysis goals or the generation of additional goals.

This step should not be underestimated since data analysts spend much of their time (sometimes 80% or more) cleaning and formatting data to make it suitable for analysis, then actually carrying out the analysis.

EDA is based on three principles: (1) Continuous openness and re-expression, (2) Initial skepticism, and (3) Exploratory versus confirmatory. Rather than immediately imposing a model on the data that may obscure important details, EDA analysts try to find patterns in the data and describe them with simple summary statistics (descriptive statistics). It may take several iterations for the analyst to reach a satisfactory summary or ''smoothing'' of the data[^3] Re-expressions or transformations of the data are essential for smoothing because they help the analyst identify new patterns.
Because EDA analysts assume that there is no uniquely correct numerical summary of a data set, they are very skeptical of initial numerical summaries. Numerical summaries and smoothings are constantly tested against the raw data to ensure that they adequately represent the data. To identify patterns and look for data points that do not fit the smooth part (outliers), EDA analysts rely heavily on visualization. 
By supporting data exploration, EDA helps researchers generate hypotheses. These hypotheses can later be tested with formal confirmatory procedures using inferential statistics.

<!-- ### Recap: Exploration vs. Confirmation -->
<!-- Erkläre mit den Wikipedia Artikel und dem Buch [@Christopher2017Statistics] -->

In summary, your goal during the EDA is to develop an understanding of your data. The easiest way to accomplish this is to use questions to guide your investigation. When you ask a question, the question focuses your attention on a particular part of your data set and helps you decide which graphs, models, or transformations to make.

<!-- Text von [@WickhamGrolemund2017Rfordatascience] -->
EDA is a creative process {cite}`WickhamGrolemund2017Rfordatascience`, thus, the key to asking meaningful questions is to generate a large number of questions <!-- KG: explain in what way this is considered "creative" - or replace "thus" with "i.e.". and expand on it.-->. Of course, it is very challenging to generate these questions at the beginning because you are not familiar with the dataset. On the other hand, each new question you ask will expose you to a new aspect of your data and increase your chance of discovery <!-- KG: of what? Meaningful insights? Expand on "discovery" and "interesting", which is referred to in the next sentence -->. You can quickly break down the most interesting parts of your data - and develop a thought-provoking set of questions - if you follow each question with a new question based on your findings. This challenge has already been formulated by Tukey:

> Far better an approximate answer to the right question, which is often vague, than an exact answer to the wrong question, 
> which can always be made precise. 
> --- John Tukey (The future of data analysis. Annals of Mathematical Statistics 33 (1), (1962), page 13)

There is no rule about what questions you should ask to guide your research. However, two types of questions will always be useful for making discoveries in your data. You can phrase these questions loosely as (1) What kind of variation occurs within my variables? and (2) What kind of co-variation occurs between my variables?

### Using Python for Data Exploration

In the following, we address these two questions based on the example of Héctor Corrada Bravo from the EDA chapter of his course on [''Introduction to Data Science''](http://www.hcbravo.org/IntroDataSci/bookdown-notes/exploratory-data-analysis-visualization.html) from the Center for Bioinformatics and Computational Biology from the Univ. of Maryland, but using Python instead of R.

We will use Python in combination with the libraries Pandas and Altair. However, you can follow these steps with any programming language at hand. I would like to provide you an methodological understanding of how to explore data, rather than provide an introduction into Python. 

[Pandas](https://pandas.pydata.org/) is a library vor data analysis and therefore very well suited for evaluating and preparing your data to visualize them afterwards. [Here](https://pandas.pydata.org/docs/user_guide/10min.html#min) you can find a short introduction to Pandas.

[Vega-Altair](https://altair-viz.github.io/) is a declarative statistical visualization library for Python. With Vega-Altair you can transform your data in various kinds of visualizations. [Here](https://altair-viz.github.io/getting_started/overview.html) you can get a short overview of Vega-Altair.


<!-- REWRITE FOR PYTHON:

In the following, we address these two questions based on the example of Héctor Corrada Bravo from the EDA chapter of his course on [''Introduction to Data Science''](http://www.hcbravo.org/IntroDataSci/bookdown-notes/exploratory-data-analysis-visualization.html) from the Center for Bioinformatics and Computational Biology from the Univ. of Maryland. 

We employ the GNU R which is a widespread tool for statistical analysis. However, you can follow these steps with any programming language at hand. I would like to provide you an methodological understanding of how to explore data, rather than provide an introduction into R (http://www.r-project.org/) which is a GNU project, thus, R is Free Software under the terms of GPL. There are over 2,000 user-contributed packages available at R CRAN (https://cran.r-project.org/) with packages for specific functions or specific areas of study. It has an excellent integration with DBs (MySQL, SQLite) and automation based on scripts is easy. Furthermore, the graphical user interface RStudio (https://www.rstudio.com/) makes its usage very convenient. R is an interpreted language. It supports procedural programming with functions and, for some functions, object-oriented programming with generic functions. A generic function acts differently depending on the type of arguments passed to it, for example, R has a generic print() function that can print almost every type of object in R with a simple ''print(objectname)'' syntax. A Base R Cheat Sheet can be found [here](https://www.povertyactionlab.org/sites/default/files/r-cheat-sheet.pdf).
-->

### Visualizing Data

In the following, we use the on-time data for all flights that departed NYC, i.e., JFK, LGA or EWR, in 2013. The Bureau of transportation statistics has released these data, and it was included into Python. Let's get an overview about this dataset.

```{code-cell} 
from nycflights13 import flights

# Show the internal structure of the data frame (= flights)
flights.info()

```

The first line shows the dimension of your data frame[^4], and then each of the columns (attributes) and show with their respective datatype.

Understanding the structure of the dataset is quite useful, since it allows you to get an overview on the available data types. A good understanding of the different data types is an important prerequisite for EDA, because you can use certain statistical measurements only for certain data types. You also need to know which data type you are dealing with in order to choose the right visualization method. Think of data types as a way to categorize different types of variables. We already discussed different types of variables in {numref}`variabletype`.

For setting up the pipeline it makes sense to work with a subset only, thus, we sample from the available data 10 percent. Furthermore, I decided to include only those observations that are complete. However, this decision should not be made carelessly. 

<!-- L: Explains why to use .copy() https://stackoverflow.com/questions/65926892/misleading-settingwithcopywarning-when-assigning-on-result-of-dataframe-dropna-->

```{code-cell} 
from nycflights13 import flights
import pandas as pd

# Select a sample from the whole data set
flights = pd.DataFrame(flights)
# takes a sample of 10 per cent, with copy() it is specified, that changes to flights_sample doesn't effect flights, else you will get a SettingWithCopyWarning
flights_sample = flights.head(int(len(flights)*0.1)).copy() 

# dimensions of the data set
flights_sample.shape

```

```{code-cell} 
from nycflights13 import flights

# remove all observations that are not complete (missing a value)
# axis=0: Drop incomplete rows, how='any' if any value is missing drop, inplace=True: modify DataFrame instead of creating new one
flights_sample.dropna(axis = 0, how = 'any', inplace = True) 

# dimensions of the data set
flights_sample.shape

```

```{code-cell} 
# show first 10 rows
flights.head(10)

```

### Scatterplot

The next step is to get a first overview about the data, and for this, we can use a visualization already. For this I use a simple scatterplot.

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Scatterplot of delay times.
    name: scatterplot1
---
import altair as alt

alt.data_transformers.disable_max_rows() # Disables the max rows restriction on handling data
fly_viz1 = flights_sample
fly_viz1 = fly_viz1.reset_index() # reset_index copies the data frame index into the new index column

# Visualize Data 1 - Scatterplot
alt.Chart(fly_viz1).mark_circle(size=40).encode( 
    x=alt.X('index', title='Flight ID'),
    y=alt.Y('dep_delay', title='Departure delay (in min)'),
    tooltip=['flight', 'year', 'dep_time', 'dep_delay'] # when you hover over the points, these data will be shown
).properties( # you can set the size of the chart with properties
    width=550,
    height=400
    ).interactive()

```
This is not very informative because this plot is not structured. However, let us reflect about the visualization for a moment. A scatterplot encodes two quantitative variables using both the vertical and horizontal spatial position channels., and the mark type is necessarily a point. They are highly effective for judging the correlation between two attributes. Scatterplots are often augmented with color coding to show an additional attribute. We talk about these characteristics in detail again.

Table: Characteristics of a scatterplot {cite}`munzner2014visualization`

Idiom       | Scatterplot  
-------     | -------------  
What: Data  | Table: two quantitative value attributes.
How: Encode | Express values with horizontal and vertical spatial position and point marks
Why: Task   | Find trends, outliers, distribution, correlation; locate clusters.  
Scale       | Items: hundreds


Let's sort the values and change the graphical representation to make it easier to see.


```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Scatterplot of delay times.
    name: scatterplot2
---
# Visualize Data - Scatterplot with ordered values
# with copy() it is specified, that changes to flights_sample doesn't effect flights, else you will get a SettingWithCopyWarning
fly_viz2 = flights_sample.copy() 
# 'sort_values' sorts a variable, here dep_delay, in descending order
# we have to ignore the previous index, otherwise the data frame index will not be reset
fly_viz2 = fly_viz2.sort_values(by=['dep_delay'], ignore_index=True) 
# limit data to dep_delay<800
fly_viz2 = fly_viz2[fly_viz2.dep_delay<800]

# create new column 'index' with row numbers from column data
fly_viz2 = fly_viz2.reset_index()

alt.Chart(fly_viz2).mark_circle(size=40).encode(  
    x=alt.X('index', title='Ordered Flight ID'),
    y=alt.Y('dep_delay', title='Departure delay (in min)'),
    tooltip=['flight', 'year', 'dep_time', 'dep_delay']
).properties( 
    width=550,
    height=400
    ).interactive()

```

What do you think of this chart? What can you say about flight delay times now? In the following, we focus on the delays only, since many flights seems to be one time.

```{code-cell} 
# Remove all flights up to max dep_delay 800
flights_sample = flights_sample[flights_sample.dep_delay<=800]

# dimensions of the data set
flights_sample.shape

```

### Histogram

Let's now create a graphical summary of these variables. Let's start with a histogram. It divides the range of the dep_delay attribute into equal-sized bins and then plots the number of observations within each bin. What additional information does this new visualization give us about this variable?

The idiom of histograms shows the distribution of elements within an attribute. In the example, you can see a histogram of the weight distribution for all cats in a neighborhood, binned into 5-pound ranges. 

The visual coding of a histogram is very similar to bar charts, with a line marker. One difference is that histograms are sometimes displayed with no space between bars to visually imply continuity, while bar charts conversely have spaces between bars to imply discretization. Despite their visual similarity, histograms are very different from bar charts. They do not show the original data but aggregate it.

The number of bins in the histogram can be chosen independently of the number of elements in the data set. The choice of bin size is crucial and tricky: a histogram can look very different depending on the discretization chosen. One possible solution to the problem is to calculate the number of bins based on the features of the data set; another is to provide controls for the user to interactively change the number of bins and see how the histogram changes.

Table: Characteristics of a histogram {cite}`munzner2014visualization` 

Idiom         | Histogram  
-------       | -------------  
What: Data    | Table: one quantitative value attribute.
What: Derived | Derived table: one derived ordered key attribute (bin), one derived quantitative value attribute (item count per bin).
How: Encode   | Rectilinear Layout. Line mark with aligned position to express derived value attribute. Position: key attribute.


```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Histogram of delay times.
    name: histogram1
---
fly_viz3 = flights_sample[flights_sample.dep_delay<=100]

alt.Chart(fly_viz3).mark_bar().encode(
  x=alt.X('dep_delay', title='Departure delay (in min)'),
  y=alt.Y('count()', title='Number of Flights')
).properties( 
    width=550,
    height=400
    )

```

In the standard function the number of bins are 30, but of course, you can change them easily. The choice of binwidth significantly affects the resulting plot. Smaller binwidths can make the plot cluttered, but larger binwidths may obscure nuances in the data.


```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Histogram of delay times.
    name: histogram2
---

s1 = alt.Chart(flights_sample).mark_bar().encode(
  x=alt.X('dep_delay', title='Departure delay (in min)', bin=alt.Bin(extent=[-20, 100], step=1)),
  y=alt.Y('count()', title='Number of Flights')
).properties( 
    width=200,
    height=150
    )

s5 = alt.Chart(flights_sample).mark_bar().encode(
  x=alt.X('dep_delay', title='Departure delay (in min)', bin=alt.Bin(extent=[-20, 100], step=5)),
  y=alt.Y('count()', title='Number of Flights')
).properties( 
    width=200,
    height=150
    )



s10 = alt.Chart(flights_sample).mark_bar().encode(
  x=alt.X('dep_delay', title='Departure delay (in min)', bin=alt.Bin(extent=[-20, 100], step=10)),
  y=alt.Y('count()', title='Number of Flights')
).properties( 
    width=200,
    height=150
    )

s15 = alt.Chart(flights_sample).mark_bar().encode(
  x=alt.X('dep_delay', title='Departure delay (in min)', bin=alt.Bin(extent=[-20, 100], step=15)),
  y=alt.Y('count()', title='Number of Flights')
).properties( 
    width=200,
    height=150
    )

alt.vconcat((s1 | s5), (s10 | s15))

```


### Density Plot

A Density Plot is a smoothed, continuous version of a histogram that visualizes the underlying probability distribution of the data by a continuous curve^[An excellent introduction in the usefulness of this method is given by Claus Wilke, check out  https://clauswilke.com/dataviz/histograms-density-plots.html]. The peaks of a Density Plot help display where values are concentrated over the interval. The most common form of estimation is known as [kernel density estimation](https://en.wikipedia.org/wiki/Kernel_density_estimation). In this method, a continuous curve (the kernel) is drawn at every individual data point and all of these curves are then added together to make a single smooth density estimation. The kernel most often used is a Gaussian (which produces a Gaussian bell curve at each data point). 

<!--A good explanation, how the density estimation works in general is given on [Wikipedia](https://en.wikipedia.org/wiki/Kernel_density_estimation#Example). -->

Just as is in the case with histograms, the exact visual appearance of a density plot depends on the kernel and bandwidth choices. In addition, the choice of the kernel affects the shape of the density curve.

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Density Plot of delay times.
    name: densityPlot1
---
# Visualize Data - Density Plot
alt.Chart(fly_viz3).transform_density(
  'dep_delay',
  as_=['Departure delay (in min)', 'density'],
).mark_area().encode(
  x="Departure delay (in min):Q",
  y='density:Q'
).properties( 
    width=550,
    height=400
    )
```

### Boxplot

Another alternative to display the distribution of a continuous variable broken down by a categorical variable is the Boxplot. The boxplot is an idiom presenting summary statistics for the distribution of a quantitative attribute, using five derived values {numref}`boxplot-fig`.

```{figure} ./images/boxplot.png
---
width: 100%
name: boxplot-fig
align: center
---
Properties of a Boxplot
```

A box that extends from the *25th percentile* (lower quartile, Q1) of the distribution to the *75th percentile* (higher quartile, Q3), a distance called the *interquartile range* (IQR). In the center of the box is a line indicating the *median*, or 50th percentile, of the distribution. These three lines give you an idea of the spread of the distribution and whether the distribution is symmetrical about the median or skewed to one side. Furthermore, a line (or whisker) extending from each end of the box to the furthest non-outlier point (Q1-1.5 x IRQ and Q3+1.5 x IRQ) in the distribution which indicates the *range*. Visual points indicating observations that fall more than 1.5 times the IQR from each edge of the box. These outer points are unusual, so they are plotted individually. 

Boxplots are useful when we want to visualize many distributions at once and/or if we are primarily interested in overall shifts among the distributions.

Table: Characteristics of a boxplot {cite}`munzner2014visualization` 

Idiom        | Boxplot  
------       | -----------------  
What: Data   | Table: many quantitative value attributes.
What: Derived | Five quantitative attributes for each original attribute, representing its distribution.
Why: Task    | Characterize distribution; find others, extremes, averages; identify skew.  
How: Encode  | One glyph per original attribute expressing derived attribute values using vertical spatial position, with 1D list alignment of glyphs into separated with horizontal spatial position.
How: Reduce  | Item aggregation.
Scale       | Items: unlimited. Attributes: dozens.

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Box Plot of delay times.
    name: boxplot
---
# Visualize Data - Box Plot 
fly_viz2['x'] = ""
alt.Chart(fly_viz2, width=200).mark_boxplot().encode( # control the size of the chart with hight/width
  alt.X('x'),
  alt.Y('dep_delay:Q').scale(zero=False)
).properties( 
    width=550,
    height=400
    )
```
```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Box Plot of delay times (log scale).
    name: boxplot2
---
import numpy as np # is needed to calculate the logarithm

# find the minimum of dep_delay
min_delay = fly_viz2['dep_delay'].min() 
# substract the min_delay from dep_delay in each row
fly_viz4 = fly_viz2.copy()
fly_viz4["dep_delay_min"] = fly_viz2.dep_delay - min_delay
fly_viz4 = fly_viz4[fly_viz4.dep_delay_min!=0] # to avoid loc(0) in the following example

# create a new column that contains the logarithm of the previously subtracted dep_delay
fly_viz4['log_dep_delay'] = np.log(fly_viz4['dep_delay_min'])

# Visualize Data - Box Plot with log scale
alt.Chart(fly_viz4, width=200).mark_boxplot().encode( 
  alt.Y('log_dep_delay:Q').scale(zero=False)
).properties( 
    width=550,
    height=400
    )
```
### Compare Distributions

Now we can start looking at the relationship between pairs of attributes. That is, how are each of the distributional properties we care about (central trend, spread and skew) of the values of an attribute changing based on the value of a different attribute. Suppose we want to see the relationship between departure delay time (a numeric variable), and the airport origin (a categorical variable).


```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Box Plot of delay times.
    name: boxplot_groups
---
# Visualize Data - Box Plot in groups
alt.Chart(fly_viz4, width=200).mark_boxplot().encode(
  alt.X('origin:N'),
  alt.Y('log_dep_delay:Q').scale(zero=False)
).properties( 
    width=550,
    height=400
    )
```
<!-- ToDo: rename legend labels, is there another way?-->

### Visualizing Multiple Distributions at Once

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival delays at NYC airport: Overlapping Histogram.
    name: hist_overlap
---
# limit arrival delay time to -60 - 120
fly_viz3 = fly_viz3[fly_viz3.arr_delay<120]
fly_viz3 = fly_viz3[fly_viz3.arr_delay>-60]

# rename used carriers
# Legend of carrier names: https://nycflights13.tidyverse.org/reference/airlines.html

fly_viz3 = fly_viz3.replace('UA', 'United Air Lines Inc.')
fly_viz3 = fly_viz3.replace('B6', 'JetBlue Airways')
fly_viz3 = fly_viz3.replace('EV', 'ExpressJet Airlines Inc.')
fly_viz3 = fly_viz3.replace('DL', 'Delta Air Lines Inc.')
fly_viz3 = fly_viz3.replace('AA', 'American Airlines Inc.')

# Visualize overlapping colors of arrival delays 
a1 = alt.Chart(fly_viz3).mark_bar(opacity=0.3).encode(
    x=alt.X('arr_delay', title='Arrival delay (in min)', bin=alt.Bin(step=5)),
    y=alt.Y('count()', title='Number of Flights'),
    color=alt.Color('carrier:N', title='Airlines')
).transform_filter(
    alt.FieldEqualPredicate(field='carrier', equal='United Air Lines Inc.')
).properties( 
    width=550,
    height=400
    )

a2 = alt.Chart(fly_viz3).mark_bar(opacity=0.3).encode(
    x=alt.X('arr_delay', title='Arrival delay (in min)', bin=alt.Bin(step=5)),
    y=alt.Y('count()', title='Number of Flights'),
    color=alt.Color('carrier:N', title='Airlines')
).transform_filter(
    alt.FieldEqualPredicate(field='carrier', equal='JetBlue Airways')
).properties( 
    width=550,
    height=400
    )

a3  = alt.Chart(fly_viz3).mark_bar(opacity=0.3).encode(
    x=alt.X('arr_delay', title='Arrival delay (in min)', bin=alt.Bin(step=5)),
    y=alt.Y('count()', title='Number of Flights'),
    color=alt.Color('carrier:N', title='Airlines')
).transform_filter(
    alt.FieldEqualPredicate(field='carrier', equal='ExpressJet Airlines Inc.')
).properties( 
    width=550,
    height=400
    )

a4 = alt.Chart(fly_viz3).mark_bar(opacity=0.3).encode(
    x=alt.X('arr_delay', title='Arrival delay (in min)', bin=alt.Bin(step=5)),
    y=alt.Y('count()', title='Number of Flights'),
    color=alt.Color('carrier:N', title='Airlines')
).transform_filter(
    alt.FieldEqualPredicate(field='carrier', equal='Delta Air Lines Inc.')
).properties( 
    width=550,
    height=400
    )

a5 = alt.Chart(fly_viz3).mark_bar(opacity=0.3).encode(
    x=alt.X('arr_delay', title='Arrival delay (in min)', bin=alt.Bin(step=5)),
    y=alt.Y('count()', title='Number of Flights'),
    color=alt.Color('carrier:N', title='Airlines')
).transform_filter(
    alt.FieldEqualPredicate(field='carrier', equal='American Airlines Inc.')
).properties( 
    width=550,
    height=400
    )


a1 + a2 + a3 + a4 + a5

```

```{code-cell} 
# Reusable Matplotlib/Seaborn plot formatting
def plot_formatting():
    # Plot formatting
    plt.legend(bbox_to_anchor=(1.02, 1), loc='upper left', borderaxespad=0, frameon=False)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    plt.style.use('seaborn-v0_8-whitegrid')
    plt.show()
``````
<!-- ToDo: Fix, that everything is in one chart-->
```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival delays at NYC airport: Side-by-Side Histogram.
    name: hist_side-by-side
---
import matplotlib.pyplot as plt

fig, ax = plt.subplots()

# Make a separate list for each airline
x1 = list(fly_viz3[fly_viz3['carrier'] == 'United Air Lines Inc.']['arr_delay'])
x2 = list(fly_viz3[fly_viz3['carrier'] == 'JetBlue Airways']['arr_delay'])
x3 = list(fly_viz3[fly_viz3['carrier'] == 'ExpressJet Airlines Inc.']['arr_delay'])
x4 = list(fly_viz3[fly_viz3['carrier'] == 'Delta Air Lines Inc.']['arr_delay'])
x5 = list(fly_viz3[fly_viz3['carrier'] == 'American Airlines Inc.']['arr_delay'])
x6 = list(fly_viz3[fly_viz3['carrier'] == 'American Airlines Inc.']['arr_delay'])

# Assign colors for each airline and the names
colors = ['#E69F00', '#56B4E9', '#F0E442', '#009E73', '#D55E00']
names = ['United Air Lines Inc.', 'JetBlue Airways', 'ExpressJet Airlines Inc.',
         'Delta Air Lines Inc.', 'American Airlines Inc.']
         
# Make the histogram using a list of lists
# Normalize the flights and assign colors and names
plt.hist([x1, x2, x3, x4, x5], bins = int(180/15),
         color = colors, label=names, density=True)

# Plot formatting
plt.xlabel('Delay (min)')
    # Density = True:
plt.ylabel('Normalized Flights')
plt.title('Side-by-Side Histogram with Multiple Airlines')
plot_formatting()
```

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival delays at NYC airport: Stacked Histogram.
    name: hist_stacked
---
# Make the histogram using a list of lists
# Normalize the flights and assign colors and names
plt.hist([x1, x2, x3, x4, x5], bins = int(180/15),
         color = colors, label=names, density=True, stacked=True)

# Plot formatting
plt.xlabel('Delay (min)')
plt.ylabel('Normalized Flights')
plot_formatting()
```

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival delays at NYC airport: Density Plot with Multiple Airlines.
    name: density_multiple
---
# transform_density gives a density plot
alt.Chart(fly_viz3).transform_density(
  'arr_delay',
  as_=['Arrival delay (in min)', 'Density'],
  groupby=['carrier']
# you can choose how you want to visualize the density plot (here line)
).mark_line(  
).encode(
  x="Arrival delay (in min):Q",
  y='Density:Q',
  color=alt.Color('carrier:N', title='Airlines')
).transform_filter(
    alt.FieldOneOfPredicate(field='carrier', oneOf=['United Air Lines Inc.', 'JetBlue Airways', 'ExpressJet Airlines Inc.', 'Delta Air Lines Inc.', 'American Airlines'])
).configure_range(
    category=alt.RangeScheme(colors)
).properties( 
    width=550,
    height=400
    )
```

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival delays at NYC airport: Shaded Density Plot.
    name: density_shaded
---

fly_viz3 = fly_viz3[fly_viz3.arr_delay<150]
fly_viz3 = fly_viz3[fly_viz3.arr_delay>-70]

fly_viz3 = fly_viz3.replace('AS', 'Alaska Airlines Inc.')

al1 = alt.Chart(fly_viz3).transform_density(
  'arr_delay',
  as_=['Arrival delay (in min)', 'density'],
  groupby=['carrier']
).mark_area(opacity=0.4  
).encode(
  x='Arrival delay (in min):Q',
  y='density:Q',
  color=alt.Color('carrier:N', title='Airlines')
).transform_filter(
    alt.FieldEqualPredicate(field='carrier', equal='United Air Lines Inc.')
).properties( 
    width=550,
    height=400
    )


al2 = alt.Chart(fly_viz3).transform_density(
  'arr_delay',
  as_=['Arrival delay (in min)', 'density'],
  groupby=['carrier']
).mark_area(opacity=0.4  
).encode(
  x='Arrival delay (in min):Q',
  y='density:Q',
  color=alt.Color('carrier:N', title='Airlines')
).transform_filter(
    alt.FieldEqualPredicate(field='carrier', equal='Alaska Airlines Inc.')
).properties( 
    width=550,
    height=400
    )

al1 + al2
```

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival delays at NYC airport: Shaded Density Plot 2.
    name: density_shaded2
---

import seaborn as sns
fig, ax = plt.subplots(figsize=(7,5), dpi=120)
options = ['United Air Lines Inc.', 'Alaska Airlines Inc.']
fly_filtered = fly_viz3[fly_viz3['carrier'].isin(options)]

sns.kdeplot(data=fly_filtered, x='arr_delay', hue='carrier', multiple='layer', fill=True)

plt.xlabel('Airlines')
plt.ylabel('Arrival Delay (min)')
plt.show()
```

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival delay of Alaska Airlines Inc. at NYC airport: Rug Plot.
    name: rug_plot
---
import seaborn as sns
# Subset to Alaska Airlines
subset = fly_viz3[fly_viz3['carrier'] == 'Alaska Airlines Inc.']

# Density Plot with Rug Plot
sns.displot(subset['arr_delay'], 
    rug = True,
    kind="kde",
    height=4.5,
    aspect=1.5,
    color = 'darkblue', 
    rug_kws={'color': 'black'})

# Plot formatting
# Plot formatting
ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)
plt.style.use('seaborn-v0_8-whitegrid')
plt.show()
```

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival Delays of Alaska Airlines: Empirical Cumulative Distribution Functions.
    name: ecdf_plot
---
# Density Plot with Rug Plot
sns.displot(subset['arr_delay'],
            kind="ecdf")

# Plot formatting
plt.xlabel('Delay (min)')

plot_formatting()
```

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival Delays: Highly Skewed Distributions
    name: skewed_plots
---
flights_s = flights.head(int(len(flights)*0.1)).copy() 
flights_s.dropna(axis = 0, how = 'any', inplace = True) 

# limit arrival delay time to -60 - 120
flights_s = flights_s[flights_s.arr_delay>0]

fig, ax = plt.subplots(1,2, figsize=(7,4), dpi=120)

# Density Plot with Rug Plot
sns.kdeplot(flights_s['arr_delay'], ax=ax[0])

sns.ecdfplot(data=flights_s, x=flights_s['arr_delay'], ax=ax[1])

# Plot formatting
plt.xlabel('Arrival Delay (min)')

plt.show()
```


```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival Delays of Alaska Airlines: Empirical Cumulative Distribution Functions Plot next to Density Plot.
    name: ecdf_density_plots
---
# Define 2 columns
fig, ax = plt.subplots(1,2, figsize=(7,4), dpi=120)

# Density Plot
sns.kdeplot(fly_viz3['arr_delay'],
            ax=ax[0])

# ECDF Plot
sns.ecdfplot(data=fly_viz3, x=fly_viz3['arr_delay'], ax=ax[1])

plt.xlabel('Arrival Delay (min)')
plt.show()
```

```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival Delays: Box Plot.
    name: box_plot3
---
fig, ax = plt.subplots(figsize=(7,5), dpi=120)
options = ['United Air Lines Inc.', 'JetBlue Airways', 'ExpressJet Airlines Inc.', 'Delta Air Lines Inc.', 'American Airlines Inc.']
fly_filtered = fly_viz3[fly_viz3['carrier'].isin(options)]
sns.boxplot(data=fly_filtered, x='carrier', y='arr_delay', whis=(0, 100))

plt.xlabel('Airlines')
plt.ylabel('Arrival Delay (min)')
plt.show()
```
```{code-cell} 
---
mystnb:
  figure:
    caption: |
      Arrival Delays: Violin Plot.
    name: violin_plot
---
fig, ax = plt.subplots(figsize=(7,5), dpi=120)
options = ['United Air Lines Inc.', 'JetBlue Airways', 'ExpressJet Airlines Inc.', 'Delta Air Lines Inc.', 'American Airlines Inc.']
fly_filtered = fly_viz3[fly_viz3['carrier'].isin(options)]
sns.violinplot(data=fly_filtered, x='carrier', y='arr_delay')

plt.xlabel('Airlines')
plt.ylabel('Arrival Delay (min)')
plt.show()
```







