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

# Understanding your Data

By building on the Nested odel of Munzner {cite}`munzner2014visualization`, we have realized how important it is to understand the context of the data origin and the data at hand. In this chapter, we focus on the data, because many data viz project start with so-called “found data”. These are data sets that are openly available on the internet, data sets in which creating you were not involved. The increasing use of data everywhere requires to think about data literacy, inclusion, and fairness to ensure that data creates value {cite}`KoestenSimperl2021_dataUX`. However, data is often reused, thus, we need to reflect on where data has been created. Koesten & Simperl {cite}`KoestenSimperl2021_dataUX` differentiate three main activities to interact with data: inspecting, engaging with the data, and placing data in context. 

Thus, in order to understand, whether data are valuable for your research question and which questions you can really tackle with these data, you need an understanding of its origin (the context of creation) and an understanding of its structure.   

## Understanding the Data Context

People's perception of what constitutes good-quality data changed as they engaged with the data. Koesten & Simperl {cite}`KoestenSimperl2021_dataUX` highlight the importance of engagement around datasets, including discussions, feedback, reviews, ratings, and means to contact data creators. User communities and peer support can complement documentation efforts and make dataset maintenance sustainable. They, furthermore, propose the three activities:

1. Explore the environment of the dataset's creation (e.g., a study setup or the conditions surrounding data collection, with timeframes, geospatial boundaries, or configurations of collection devices).
2. Explore the norms of the discipline in which the data was collected, including methods of analysis and validation, as well as limitations (e.g., common margins of error). 
3. Connect data with the world, gauging how representative it is and reflecting on assumptions about how much it mirrors reality (includes also the question of what might be missing from the data.

Gebru et al. {cite}`Gebruetal2018datasheets` propose “datasheets” inspired by more robust documentation standards in the electronics industry. Datasheets are meant to improve transparency and accountability of datasets and to be useful to both dataset creators and dataset consumers. 
For consumer of datasets, datasheets should encourage reflection on the process of creating, distributing, and maintaining a dataset (including benefits and harms). For dataset creators it helps also to reflect on the data and to make more informed decisions about its use. The authors offer guiding questions towards creating datasheets for datasets:

* Motivations: Describe the motivations for creating the dataset, including funding, any specific tasks the authors had in mind, and who the authors are.
* Composition: Describe the composition of the dataset, like what kinds of data are in it, how it was collected, whether labels are associated with the data, and whether the dataset contains sensitive information.
* Collection Process: Describe the data collection process, like how the data was collected, where or who is was collected from, who was involved in the collection process, and, if people are involved, if consent was given for the data to be collected.
* Processing: Whether the data was process or labelled and how it was done.
* Uses: The tasks the dataset is intended to be used for, how it has already been used, and limitations of use.
Distribution: How the dataset will be distributed and to who, and any restrictions on distribution.
* Maintenance: Who and how the dataset will be maintained, and if and how others will be able to build on it.

Building on this idea Holland et al. {cite}`Hollandetal2018DatasetNutritionLabel` proposed the [dataset nutrition label](https://datanutrition.org/). An example is given in {numref}`dataset-nutrition-fig`

```{figure} ./images/dataset_nutrion_label.png
---
width: 100%
name: dataset-nutrition-fig
align: center
---
Example of the Dataset Nutrition Label (first generation). Taken from https://datanutrition.org/
```
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

In this section, we focus on understanding the structure of our data by employing the Exploratory Data Analysis (EDA). EDA is an approach of analyzing data sets to summarize their main characteristics by using data visualizations. In 1970 John Tukey {cite}`Tukey1977eda` introduced EDA with this seminal book on this topic. He was an extraordinary scientist who had a profound impact on statistics and computer science[^2]. Much of what we cover in EDA today is based on his work. Part of EDA is the so-called initial data analysis (IDA) [](https://towardsdatascience.com/a-basic-guide-to-initial-and-exploratory-data-analysis-6d2577dfc242). IDA focuses on identifying data inconsistencies (e.g., missing values) and the description of the data properties; thus, EDA encompasses IDA. 

EDA allows the data analysts to achieve a richer qualitative understanding by ''looking at data to see what it seems to say''. Explorative Data Analysis should be understood as an iterative process that supports:
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
EDA is a creative process {cite}`WickhamGrolemund2017Rfordatascience`, thus the key to asking meaningful questions is to generate a large number of questions. Of course, it is very challenging to generate these questions at the beginning because you are not familiar with the dataset. On the other hand, each new question you ask will expose you to a new aspect of your data and increase your chance of discovery. You can quickly break down the most interesting parts of your data - and develop a thought-provoking set of questions - if you follow each question with a new question based on your findings. This challenge has been already formulated by Tukey:

> Far better an approximate answer to the right question, which is often vague, than an exact answer to the wrong question, 
> which can always be made precise. 
> --- John Tukey (The future of data analysis. Annals of Mathematical Statistics 33 (1), (1962), page 13)

There is no rule about what questions you should ask to guide your research. However, two types of questions will always be useful for making discoveries in your data. You can phrase these questions loosely as (1) What kind of variation occurs within my variables? and (2) What kind of co-variation occurs between my variables?

### Using Python for Data Exploration

In the following, we address these two questions based on the example of Héctor Corrada Bravo from the EDA chapter of his course on [“Introduction to Data Science”](http://www.hcbravo.org/IntroDataSci/bookdown-notes/exploratory-data-analysis-visualization.html) from the Center for Bioinformatics and Computational Biology from the Univ. of Maryland. 

We employ Python with Pandas and Altair which is a widespread tool for statistical analysis. However, you can follow these steps with any programming language at hand. I would like to provide you an methodological understanding of how to explore data, rather than provide an introduction into Python.


### Visualizing Data

In the following, we use the on-time data for all flights that departed NYC, i.e., JFK, LGA or EWR, in 2013. The Bureau of transportation statistics has released these data, and it was included into Python. Let's get an overview about this dataset.

```{code-cell} 
from nycflights13 import flights

# Show the internal structure of the data frame (= flights)
flights.info()

```

The first line shows the dimension of your data frame[^4], and then each of the columns (attributes) and show with their respective datatype.

Understanding the structure of the dataset is quite useful, since it allows you to get an overview on the available data types. A good understanding of the different data types is an important prerequisite for EDA, because you can use certain statistical measurements only for certain data types. You also need to know which data type you are dealing with in order to choose the right visualization method. Think of data types as a way to categorize different types of variables. We already discussed different types of variables in Section \@ref(sec:variabletype).

For setting up the pipeline it makes sense to work with a subset only, thus, we sample from the available data 10 percent. Furthermore, I decided to include only those observations that are complete. However, this decision should not be made carelessly. 

```{code-cell} 
from nycflights13 import flights
import pandas as pd

# Select a sample from the whole data set
flights = pd.DataFrame(flights)
flights_sample = flights.head(int(len(flights)*0.1)) # takes a sample of 10 per cent

# dimensions of the data set
flights_sample.shape

```
% Fix this code cell: warning SettingWithCopyWarning: A value is trying to be set on a copy of a slice from a DataFrame
```{code-cell} 
from nycflights13 import flights

# remove all observations that are not complete (missing a value)
flights_sample.dropna(axis = 0, how = 'any', inplace = True) # takes a sample of the first 10 rows

# dimensions of the data set
flights_sample.shape

```

### Scatterplot

The next step is to get a first overview about the data, and for this, we can use a visualization already. For this I use a simple scatterplot.

```{code-cell} 
import altair as alt

alt.data_transformers.disable_max_rows() # Disables the max rows restriction on handling data

fly_viz1 = flights_sample.reset_index()

# Visualize Data 1 - Scatterplot
alt.Chart(fly_viz1).mark_circle(size=60).encode(  # reset.index() creates a column with the row index
    x=alt.X('index', title='Flight ID'),
    y=alt.Y('dep_delay', title='Departure delay (in min)'),
    tooltip=['flight', 'year', 'dep_time', 'dep_delay']
).interactive()

```

This is not very informative because this plot is not structured. However, let us reflect about the visualization for a moment. A scatterplot encodes two quantitative variables using both the vertical and horizontal spatial position channels., and the mark type is necessarily a point. They are highly effective for judging the correlation between two attributes. Scatterplots are often augmented with color coding to show an additional attribute. We talk about these characteristics in detail again.

Table: Characteristics of a scatterplot [@munzner2014visualization]

Idiom       | Scatterplot  
-------     | -------------  
What: Data  | Table: two quantitative value attributes.
How: Encode | Express values with horizontal and vertical spatial position and point marks
Why: Task   | Find trends, outliers, distribution, correlation; locate clusters.  
Scale       | Items: hundreds


Let's sort the values and change the graphical representation to make it easier to see.

% Fix this code by sorting 
```{code-cell} 
# Visualize Data - Scatterplot with ordered values

# 'sort_values' sorts a variable, here dep_delay, in descending order
# we have to ignore the previous index, otherwise the data frame index will not be reset
fly_viz2 = flights_sample.sort_values(by=['dep_delay'], ignore_index=True) 

# create new column 'index' with row numbers from column data
fly_viz2 = fly_viz2.reset_index()

alt.Chart(fly_viz2).mark_circle(size=60).encode(  
    x=alt.X('index', title='Ordered Flight ID'),
    y=alt.Y('dep_delay', title='Departure delay (in min)'),
    tooltip=['flight', 'year', 'dep_time', 'dep_delay']
).interactive()

```

What do you think of this chart? What can you say about flight delay times now? In the following, we focus on the delays only, since many flights seems to be one time.

```{code-cell} 
# Remove all flights with no delay
flights_sample = flights_sample[flights_sample.dep_delay <= 0]

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


```

[^2]: I highly recommend reading more about him, for example in [](https://www.stat.berkeley.edu/~brill/Papers/life.pdf).
[^3]: The so-called "smooth part of a data set" is the variability that the analyst has accounted for so far, while the "rough" part is the variability that remains unexplained.
[^4]: A dataframe is a list, with each component of that list being a equal length vector. Thus, intuitively, a dataframe is like a matrix with a rows-and-comlumns-structure. However, it differs from a matrix, since each column can having different mode (data type) {cite}`Matloff2011ArtofRProgramming`.
