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

# Visualizing Tabular Data

```{admonition} PLEASE NOTE
:class: warning
These lecture notes are neither for distribution nor for reference. It is just a first draft and many resources may not be referenced yet, furthermore, images are largely missing. I update these lecture notes throughout the course. If you spot any major mistakes, let me know.
```
Now you learnt about the general process of creating data visualizations and we have also discussed certain restrictions that exist in human visual and spatial cognition. These foundations help us to dive deeper into the topic of visualizations. In the next three chapters, we explore various visualizations and their characteristics. This helps you to make an informed decision when selecting for a certain visual encoding.

The majority of "found" data is available in a tabular format, since it is very convenient for understanding and working with the data. In this chapter, thus, we focus on this data type.
<!-- https://medium.com/transparent-data-eng/5-levels-of-data-openness-a-long-road-from-pdf-to-lod-e10cf36b41c9 -->

Tabular data {cite}`munzner2014visualization` consists of key (often the header) and value attributes. A key is an independent attribute that can be used as a unique index to look up items in a table. It can be a categorical or ordinal variable. A value is a dependent attribute: the value of a cell in a table. Values can be categorical, ordinal, or quantitative attributes. What are our possibilities for transferring tabular data into a certain visual encoding? Our decision depends on the semantics of the table's attributes, i.e., how many keys and how many values our table has. In case of two value attributes that are quantitative, we can use a scatterplot, with one key (categorical) and one value attribute (quantitative), a bar chart is appropriate, and heatmaps show two keys (categorial) and one value (quantitative). In the following sections, we explore possible visual encodings in more detail by focusing on four aspects {cite}`munzner2014visualization`:

- Visual Encoding for Numerical Data
- Visual Encoding for Categorical Data
- Spatial Axis Orientation
- Spatial Layout Density

## Visual Encoding for Numerical Data

As you already know, quantitative attributes, i.e., numerical data, can visually be encoded by representing them over the spatial position channel. The most simple representation is to encode a single quantitative attribute along an axis by encoding each element of the attribute with a marker.  When you have two quantitative attributes you use the **scatterplot** by encoding the values on the vertical and horizontal spatial position channels, respectively. The mark type is necessarily a point and additional attributes can be encoded with other non-spatial channels such as color and size. Size-coded scatterplots are sometimes referred to as **bubble charts**. As discussed in the EDA Chapter \@ref(Understanding-the-Data-Structure) scatter plots are useful for characterizing distributions, especially for finding outliers and extreme values. They are also very effective for assessing the correlation between two attributes. 

However, besides the encoding of the data, scatterplots have so-called non-data components, such as axes and legends. These components are often just as important as the data itself since they provide contextual information for interpreting the data {cite}`Talbotetal2010ticklabels`. The labeling of the axis, for example, allows the viewer to lookup values, to mentally compute ranges, or to estimate the slope. Over the years, many researchers of thought of approaches to algorithmically create ''nice'' labels (such as ). Discussing these approaches is beyond the scope of this lecture but I want to highlight one research work by Talbot et al. {cite}`Talbotetal2010ticklabels`. They compared different approaches in this sphere and recommended a new algorithm for finding an optimal labeling for a given dataset. They made the following recommendations - the labeling should

1. be simple, i.e., the numbers of the tick marks should be multiples of 10, 5, 2 
2. cover the complete axis, i.e., there should be tick marks close to the ends of the data 
3. balance density, i.e., there should not too many, nor too few tick marks. 
4. be legibel, i.e., the formatting of the label (e.g., 5M vs. 5,000,000), font size (e.g., for avoiding overlapping labels), and orientation (e.g., o handle extremely dense axis) should be considered. 

However, axis labeling is just one component to think of in graphic design. Another important component is the layout of an entire plot, including the placement of titles, axis titles, legends, data labels, or aspect ratio. We talk about the latter in more detail in Section \@ref(Visual-Encoding-for-Categorical-Data). 

The issue of axis scaling is also essential to consider. One question that is often discussed is whether scaling to zero is necessary. On the one hand ''zooming in'' helps to understanding the differences in the data, but on the other hand, it can be misleading. The decision depend on the visual encoding of the data. Bar charts, for example, use position (end of bar) and size (length and area) to encode numeric values. When ''zooming in'' bar chats, the length of a bar encodes meaningless information. In any case, when you use a **non zero-based scale**, make sure that your inform the reader clearly about this design decision. 

<!-- http://www.sthda.com/english/wiki/ggplot2-axis-scales-and-transformations -->
Another challenge occurs if the data is very unevenly distributed. Imagine you have data where the majority of data is very close together but there is one outlier. Because of this outlier, the majority of data is compressed and individual differences are challenging to be caught. What can you do? Well, the easiest the most straightforward approach might be to skip the outlier, however, in many cases such data manipulation is not appropriate. There are two additional approaches that can help to overcome this issue of outliers: the use of a scale break and the transformation of the data (by using a logarithmic scale). 

A **scale breaks** should be designed with care. Conventional scale breaks consists of two short parallel lines intersecting the axis. Such scale breaks should be avoided since often the viewer of the graph may overlook this important information. However, there is also the so-called full scale break which divides the graph into two panels, each with a full frame and its own scale {cite}`Cleveland1984fullscalebreaks`. The visual discontinuity discourages pattern or continuity perception across the break. 

A more frequently applied strategy is data transformation by using a log scale. Both approaches increase the visual resolution of the data. The scale break makes it difficult to compare the data, since you have to cognitively and not perceptually consume the data. As opposed to the **log scale**, where you can directly compare all data.

A logarithmic transformation of data has many advantages, since you can address data skew, for example, when having a long tail or outliers. It enables the viewer the comparison within and across multiple orders of magnitude. A logarithmic scale shows the rate of change, i.e., the same distance along a logarithmic scale equals the same percentage or ratio {cite}`Few2004Showmethenumbers`. This supports the usage of a logarithmic scale in cases, where data to be shown are ratios, for example number of people in a city district, divided by the median number of people across the city (see {cite}`Wilke2019dataviz`).

However, in two cases you should avoid using a log scale: when you have negative non-zero values or when you audience is potentially not familiar with this type of scale transformation (which is rather the rule rather than the exception). In the latter case, if you cannot avoid it, make sure that you need to educate the viewer. Include something like (interactive) annotations to ensure that your viewer can understand the visualization. Usually, the logarithmic scale use a base of 10, but the base 2 is useful as well. A base-2 logarithmic scale allows to show rate of change in terms of doubling {cite}`Few2004Showmethenumbers`.

(Visual-Encoding-for-Categorical-Data)=
## Visual Encoding for Categorical Data 

The use of space to encode categorical attributes is a bit more complex, since categorical attributes have often a disordered semantic. Remember, the principle of expressiveness is violated if categorical attributes are encoded using spatial position {cite}`munzner2014visualization`.

Drawing all of the items with the same values for a categorical attribute within the same region uses spatial proximity to encode the information about their similarity. The regions themselves must be given spatial positions on the plane in order to draw any specific picture. The separation should be done according to an attribute that is categorical, whereas alignment and ordering should be done by some other attribute that can be ordered.

We already talked about the (simple) **bar chart** that are suitable if your tabular data consist of one numerical and one categorical attribute. You use line marks to express the value numerical attribute with aligned vertical position and you separate the key categorical attribute with horizontal position. Bar chart support the lookup of values or their comparison. They scale well up to dozens to hundreds of key attributes.

Another often used bar chart tye is the **grouped bar chart** if you have one numerical and a number of categorical attributes.

What we often see are **stacked bar charts** {cite}`munzner2014visualization`. The scalability of stacked bar charts is similar to that of standard bar charts in terms of the number of categories in the key attribute distributed across the major axis, but is limited for the key used to stack. This idiom works well with multiple categories, with an upper limit of about a dozen. A normalized stacked bar chart stretches each of these bars to the maximum possible length and shows percentages rather than absolute values. Only the lowest subbar in a stacked bar chart is aligned with the others in its category, so that the most accurate position channel can be used. The other subbars use an unaligned position, a channel that is less accurate than the aligned position. If used stacked bar charts should allow the viewer to interactively change the order.

Both, the simple, grouped, and stacked bar chart can often be replaced by a **dot chart**. This chart has a number of advantages compared to other more widely used bar charts {cite}`soenning2016dotplot`. The dot plot was introduced by Cleveland {cite}`ClevelandMcGill1984graphicalperception`. The horizontal scale encodes a quantitative variable and the vertical scale a categorical variable. Furthermore, light horizontal lines connect the data points with their labels.

Another often used diagram you already know of are **line charts**. A line chart has one quantitative attribute and one ordered attribute. Line charts often emphasize trend relationships. Zacks and Tversky {cite}`ZacksTversky1999linechartbarchart`, for example, studied how people answered questions concerning the meaning provided in line and bar charts. Line graphs for quantitative data provided appropriate trend-related answers, such as "height increases with age." Bar charts for quantitative data yielded equally appropriate discrete comparison responses, such as "Twelve-year-olds are taller than ten-year-olds." However, line graphs for categorical data yielded inappropriate trend responses such as "The more male a person is, the taller he is." This experiment emphasize the importance of well-chosen visual encodings.

However, the same data can look very different in a line chart depending on its aspect ratio. But what is the perfect shape for a chart? The ratio between the width and height of a rectangle is called the aspect ratio. It is typically expressed as a fraction with two numbers, where the width is divided by the height. An aspect ratio of 1:1 describes a square, while 4:3 (or 1.33:1) is a landscape rectangle and 16:9 is a much wider landscape rectangle. While width is usually greater than height in film and photography, there is no reason for this to be the case in visualization. What do you do? Short answer is: ''It depends on the data.''. However, Cleveland et al. {cite}`ClevelandMcGill1984graphicalperception` proposed that the average line slope in a line chart should be $45^{\circ}$. This was called banking to $45^{\circ}$ and has become one of the common rules in visualization design to determine the ideal aspect ratio. In other words, a rule of thumb is that the average line inclination in a line chart should be 45 degrees. Heer and Agrawala {cite}`HeerAgrawala2006banking` extended this approach, by analyzing data for trends at various frequency scales and then generates a banked chart for each of these scales. 

The aforementioned visualization are suitable for less complex data sets, but what do you do, if this is not the case. Two visualizations that you should take in mind a the heatmap and the scatterplot matrix. 

A **heatmap** is used to encode two categorical and one quantitative attribute {cite}`munzner2014visualization`. It is suitable for finding cluster, outliers, and to summarize data. The advantage of heat maps is that the visual coding of quantitative data with color using small area markers is very compact, making them well suited for overviews with high information density. An extension is the **cluster heat map**, it is the side-by-side combination of a heat map and two dendrograms that display the derived data from the cluster hierarchies used in the matrix reordering. The goal of this reordering is to group similar cells together to look for patterns between the two attributes.

A **scatterplot matrix** (SPLOM) is a matrix where each cell contains an entire scatterplot diagram {cite}`munzner2014visualization`. A SPLOM shows all possible pairwise combinations of attributes, using the original attributes as rows and columns. Unlike the simple heatmap matrix where each cell displays an attribute value, an SPLOM is an example of a more complex matrix. SPLOMs are heavily used for the abstract tasks of finding correlations, trends, and outliers, according to the use of their constituent scatter plot components.

## Spatial Axis Orientation

In a rectilinear layout, regions or elements are distributed along two orthogonal axes, the horizontal and vertical spatial positions, ranging from a minimum value on one side of the axis to a maximum value on the other. Rectilinear layouts are heavily used in vis design and appear in many common statistical charts. All examples discussed so far used rectilinear layouts. However, the spatial axes alignment is another design option in visualization design, thus, you can use besides a rectilinear, also a parallel or a radial layout {cite}`munzner2014visualization`. 

An example for the parallel layout are **parallel coordinates**. It is an approach for visualizing many quantitative attributes at once using spatial position. As the name suggests, the axes are placed parallel to each other, rather than orthogonal at right angles.
In parallel coordinates a single item is represented by a jagged line that zigzags through the parallel axes, crossing each axis exactly once at the location of the item’s value for the associated attribute. Parallel coordinates scale to show hundreds of elements, but not thousands. If too many lines are overdrawn, the resulting occlusion provides very little information. The original motivation of parallel coordinates was that they are used to check for correlations between attributes. When two adjacent axes have a high positive correlation, the line segments are mostly parallel.  When two axes have a high negative correlation, the line segments usually cross at a point between the axes. The pattern between uncorrelated axes is a mixture of crossing angles. In practice, however, SPLOMs are typically easier to use to find a correlation. Parallel coordinates are used to get an overview of all attributes, to classify the range of values of attributes, to select a range of elements or to detect outliers. 

In a radial spatial layout, elements are distributed around a circle using the angular channel in addition to one or more linear spatial channels. The natural coordinate system in radial layouts is **polar coordinates**, where one dimension is measured as an angle from a starting line and the other as a distance from a center point. Radial layouts can be more effective than rectilinear in representing the periodicity of patterns, however, encoding non-periodic data with the periodic channel of the angle can be misleading. Radial layouts imply an asymmetry of meaning between the two attributes and it would be inappropriate if the two attributes have the same meaning.

The most commonly used radial statistical graph is the **pie chart**. It encodes a single attribute with area markers and the angle channel. Despite their popularity, pie charts are problematic. Angle judgments at area markers are less accurate than length judgments at line markers. Wedges vary in width along the radial axis, from narrow near the center to wide near the outside, making area judgments particularly difficult. The most useful property of pie charts is that they show the relative contribution of parts to a whole. The sum of the wedge angles must add up to $360^{\circ}$ of a full circle and match normalized data, such as percentages where the parts must add up to 100%. However, this property is not only important for pie charts; a single bar in a normalized stacked bar chart can also be used to indicate this property with the more accurate length assessment channel. 

## Spatial Layout Density

Another design choice with spatial visual coding ideas is whether a layout is dense or sparse. 

A dense (pixel oriented) layout uses small and densely packed marks to provide an overview of as many items as possible with very high information density. A maximally dense layout has point marks that are only a single pixel in size and line marks that are only a single pixel in width. The small size of the marks implies that only the planar position and color channels can be used in visual encoding.

A space-filling layout has the property that it fills all available space in the view, as the name implies. Space-filling layouts typically use area marks for items or containment marks for relationships, rather than line or connection marks, or point marks. An advantage of space-filling approaches is that they maximize the space available for color markings. On the other hand, a disadvantage of space-filling views is that the designer cannot use white space in the layout. Many graphic design guidelines refer to the careful use of white space for many reasons, including legibility, emphasis, relative importance, and visual balance. Space-filling layouts usually strive for a high density of information. However, the characteristic that a layout fills space is by no means a guarantee of efficient use of space. Technically, the definition of space filling is that the total area used by the layout is equal to the total area available in the view. An example of a space-filling layout are **treemaps** which are discussed in the next chapter.