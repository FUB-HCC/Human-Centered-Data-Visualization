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
  name: python3
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

## Understanding the Data Structure {#Understanding-the-Data-Structure}

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


[^2]: I highly recommend reading more about him, for example in [](https://www.stat.berkeley.edu/~brill/Papers/life.pdf).
[^3]: The so-called "smooth part of a data set" is the variability that the analyst has accounted for so far, while the "rough" part is the variability that remains unexplained.

