# Getting Data

Whether we use Python or Google Sheets, the first step of our project is to import data. For the purpose of this experiment, we will use a `CSV` version of a City of Ottawa dataset {cite}`openottawa` listing the building, demolition, and pool enclosure permits delivered in 2021. The `CSV` file is [available here](https://raw.githubusercontent.com/jsmarier/course-datasets/main/ottawa-building-permits-2021.csv).

## Importing the Data

To import the `CSV` into a Jupyter Notebook with Python, we need to run the code below in a code cell. We will name our dataset `permits`. This code will also display the first five rows thanks to `.head()`.

```python
import pandas as pd

permits = pd.read_csv('https://raw.githubusercontent.com/jsmarier/course-datasets/main/ottawa-building-permits-2021.csv')

permits.head()
```

```{figure} images/2022-12-11_ass-8_head-permits-dataset.png
---
width: 700px
name: head-of-permits-dataset
---
Screen capture of the first five rows of the permits dataset after importation.
```

The screen capture shown in {numref}`head-of-permits-dataset` shows the output of the `Python` code. 

```{note}
Since this page was created in the Markdown (.md) format, the code above is static. However, we will run the same code in our Understanding Data: VIMO Analysis and Delivering Data Jupyter Notebooks.
```

Let's now see what we need to do to complete the same steps in Google Sheets. The easiest way of importing a `CSV` file with Google Sheets is to use the IMPORTDATA function. For our current dataset, it would look like this:

```
=IMPORTDATA("https://raw.githubusercontent.com/jsmarier/course-datasets/main/ottawa-building-permits-2021.csv")
```

However, this function does not work with larger files. In this case, we need to first download the `CSV` to our hard drive. Then, in Google Sheets, we click on File > Import. When the "Import file" window appears, we select "Upload." Then, we upload our CSV, making sure to select the appropriate value separator. Here's what the dataset looks like in Google Sheets right after importation.

```{figure} images/2022-12-11_ass-8_importation-into-google-sheets.png
---
width: 700px
name: importation-into-google-sheets
---
Screen capture of the dataset right after being imported into Google Sheets.
```

## Obtaining Summary Information About the Dataset

We can easily get more information about the different columns in our dataset by running the following Python code:

```python
permits.info()
```

```{figure} images/2022-12-11_ass-8_permits-info.png
---
width: 700px
name: permits-info
---
Screen capture of the summary table showing, among other things, the number of non-null values.
```

As seen in {numref}`permits-info`, the `.info() function` returned a table showing the number of non-null values in each column, as well as the type of variable of each column.

```{margin} This needs some cleaning...
We have yet to clean this dataset. Among other things, the VALUE column needs to be converted from object to int64.
```

We can obtain similar information about a column in Google Sheets by using the "Column stats" tool found under Data > Column stats. The contextual window on the right will show, among other things, the total number of rows, as well as the number of empty cells in the column.

```{figure} images/2022-12-11_ass-8_column-stats-empty-cells.png
---
width: 700px
name: column-stats-empty-cells
---
Screen capture of the column stats window showing that there are two empty cells under the FT2 column.
```

:::{admonition} Who's the winner?
:class: tip, dropdown
As we just saw here, Google Sheets is perhaps a little bit easier to use. However, Python can handle much larger files.
:::