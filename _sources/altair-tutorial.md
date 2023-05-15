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

**Data Visualization course - winter semester 20/21 - FU Berlin**

*Tutorials adapted from the [Information Visualization](https://infovis.fh-potsdam.de/tutorials/) course at the FH Potsdam*

# Tutorial 4: Geovisualization

In this installment of the information visualization tutorials we will be analyzing and visualizing geographic data; i.e., data that refers to geospatial entities. Geospatial entities can, for example, be particular places such as schools and libraries or political boundaries of cities or countries. Of course, this tutorial only scratches the surface. Consider this as a teaser into geovisualization, which in itself has become a branch of research and practice at the intersection of geography and visualization. We will only touch on a few basic steps to get your feet wet and hands dirty.

+++ {"tags": ["prepare"]}

## 🛒 1. Prepare 

As you come to expect by now we first assemble our tools and then prepare the data. 

```{seealso}
:class: dropdown
[Altair documentation](https://altair-viz.github.io/user_guide/generated/toplevel/altair.Chart.html) 
<br/>
[Pandas documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.info.html)
```

```{code-cell}
import altair as alt
import pandas as pd
from vega_datasets import data
```
### Load Data

As usual, we need to get ou data into our notebook first:

```{code-cell}
# First, allow unverified SSL connections, in case the certificate can not be verified
import ssl
ssl._create_default_https_context = ssl._create_unverified_context
```

```{code-cell}
covid_data = pd.read_csv("https://covid.ourworldindata.org/data/owid-covid-data.csv")
```
Additionally to our usual dataset we are going to use another dataset which contains a mapping of different country ISO codes and the avergae coordinates of each country.

```{code-cell}
code_lookup = pd.read_csv("country_lookup.csv")
```

```{code-cell}
code_lookup.info()
```
Finally we also need data which tells us how countries actually look like in order to visualize them properly. This information is encoded in TopoJSON, an extension of GEOJSON, which is able to encode topology in the often used JSON serialization format.

```{code-cell}
countries = alt.topo_feature(data.world_110m.url, 'countries')
countries
```
## 2. Present
### Simple map projection

```{code-cell}
alt.Chart(countries).mark_geoshape(
    stroke='white',
    fill='#A9A9A9'
).project(
    type='mercator'
)
```

```{code-cell}
map = alt.Chart(countries).mark_geoshape(
    stroke='white',
    fill='#A9A9A9'
).project(
    type='mercator',
    scale=250,
    center=[20,55],
    clipExtent= [[0,0], [400, 300]]
)
map
```
### Graduated Symbols

```{code-cell}
country_infections = covid_data[['iso_code', 'total_cases_per_million']].groupby('iso_code').max().reset_index()
country_infections.info()
```

```{code-cell}
merged_lookup_data = country_infections.merge(code_lookup, left_on='iso_code', right_on='Alpha-3 code').rename(columns={'Numeric code': 'id'})
merged_lookup_data
```

```{code-cell}
symbols = alt.Chart(merged_lookup_data).mark_circle().encode(
    longitude='Longitude (average)',
    latitude='Latitude (average)',
    size=alt.Size('total_cases_per_million', legend=None),
    tooltip=['Country', 'total_cases_per_million'],
).project(
    type='mercator',
    scale=250,
    center=[20,55],
    clipExtent= [[0,0], [400, 300]]
)

map + symbols
```
### Choropleth Map

For the first time we need to encode our data manually since we use the ```transform_lookup``` function and Altair cannot infer the types of the variable therefore.
The following encodings are possible:

|   Data Type  | Shorthand Code |            Description            |
|:------------:|:--------------:|:---------------------------------:|
| quantitative |        Q       | a continuous real-valued quantity |
| ordinal      |        O       | a discrete ordered quantity       |
| nominal      |        N       | a discrete unordered category     |
| temporal     |        T       | a time or date value              |
| geojson      |        G       | a geographic shape                |

```{code-cell}
alt.Chart(countries).mark_geoshape(
    stroke='white'
).encode(
    color='total_cases_per_million:Q',
    tooltip=['Country:N','total_cases_per_million:Q']
).transform_lookup(
    lookup='id',
    from_=alt.LookupData(data=merged_lookup_data, key='id', fields=['total_cases_per_million', 'Country'])
).project(
    type='mercator',
    scale=250,
    center=[20,55],
    clipExtent= [[0,0], [400, 300]]
)
```
