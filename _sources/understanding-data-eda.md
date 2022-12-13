# Understanding Data: Exploratory Data Analysis (EDA)

The summary statistics and frequency distribution charts we just created help us have a better understanding of the data we are dealing with. In this section, I will compare my exploratory data analysis (EDA) process with Python and Google Sheets.

## .groupby VS a Pivot Table

A very useful tool offered by the Pandas library is the `.groupy` function. It looks something like this:

```python
permits_grouped = permits.groupby("WARD").count()

permits_grouped
```

The code above generates a new table featuring the number of non=null (non empty) cells for each column, grouped by wards.

```{figure} images/2022-12-11_ass-8_groupby-ward-pandas.png
---
width: 700px
name: groupby-ward-pandas
---
Screen capture of the permits dataset grouped by wards.
```

{numref}`groupby-ward-pandas` shows the first 10 rows of the table.

```{margin} As previously mentioned, this dataset requires some cleaning, which falls outside the scope of this assignment. Therefore, the figures presented here include duplicate rows and are only shown as a demonstration of my current skills.
```

Given the previously mentioned "parsing" error, I am unable to group my variables by other columns, such as VALUE, BLG TYPE (building type), etc. This would be useful, for example, to calculate the number of projects involving each building type (single family home, retail, industrial, rowhouse, etc.) in each ward.

This is actually something rather easy to do with Google Sheets's Pivot Table tool. Simply select the entire dataset and click on Insert > Pivot table. Then, put `WARD` under the rows, `BLG TYPE` under the columns, and `BLG TYPE`, summarized by COUNTA, under values.

```{figure} images/2022-12-11_ass-8_pivot-table.png
---
width: 700px
name: pivot-table
---
Screen capture of the pivot table in Google Sheets, showing the number of projects involving each type of building in each ward.
```

:::{admonition} Who's the winner?
:class: tip, dropdown
In theory, Python is much more powerful than Google Sheets. However, as we saw here, while the .groupby function is quite useful, solving "parsing" errors can require hours of work. I find the "what-you-see-is-what-you-get" approach embodied by Google Sheets a bit simpler.
:::

## Exploratory Charts

As we saw in the previous section, creating charts with `Altair` requires only a few lines of code. As a reminder, the code below can quickly and efficiently generate a frequency table (bar chart) of the number of projects per ward:

```python
import altair as alt
alt.data_transformers.disable_max_rows()

alt.Chart(permits, width=500, height=400).mark_bar().encode(
    x=alt.X("WARD:N", sort="y", title="Ward"),
    y=alt.Y('count()', title="Number of Projects"))
```

```{figure} images/2022-12-11_ass-8_pandas-frequency-table.png
---
width: 700px
name: pandas-frequency-table
---
Screen capture of the bar chart created with the code above.
```

The bar chart seen in {numref}`pandas-frequency-table` was generated using the `Python` code above.

In comparison, creating a similar chart with Google Sheets requires the following steps:

1. Select D column
1. Click on Insert > Chart
1. Click on "Aggregate" under X-axis in the chart editor
1. Click on "Customize" in the top right corner
1. Under "Chart & axis titles," select "Horizontal axis title" with the drop down menu
1. Type "Ward" under "Title text"
1. Select "Vertical axis title"
1. Type "Number of Projects" under "Title text"

And here's the result:

```{figure} images/2022-12-11_ass-8_google-sheets-chart.png
---
width: 700px
name: google-sheets-chart
---
Screen capture of the bar chart created with Google Sheets.
```

The level of difficulty here is similar to Altair's. Moreover, both tools allow us to download a PNG or SVP copy of the chart by clicking on the three little dots in the top right corner.

:::{admonition} Who's the winner?
:class: tip, dropdown
Here, I will call a tie between Altair and Google Sheets. In the first case, creating an exploratory chart takes only a few lines of code. Likewise, we can create a similar chart with Google Sheets in under 10 clicks.
:::